

Bosh OpenStack 镜像包下载地址
https://bosh.cloudfoundry.org/stemcells/bosh-openstack-kvm-ubuntu-trusty-go_agent


cf-release 镜像包下载
https://bosh.io/releases/github.com/cloudfoundry/cf-release?all=1

这里使用231版本
https://bosh.io/d/github.com/cloudfoundry/cf-release?v=231


bosh deploy参考链接： https://bosh.io/docs/init-openstack/



**1. 准备运行环境**

* 1.1.准备一台ubuntu 16.04的执行机，用以安装bosh cli和cloudfoundry cli执行部署cf的命令，以及后面部署cf成功后调用cf命令在cf上部署应用，登录这台执行机进行1.2步骤的操作


* 1.2.使用terraform创建安装bosh需要的公有云资源

  terraform模板参考：https://github.com/cloudfoundry-incubator/bosh-openstack-environment-templates/tree/master/bosh-init-tf

  该模板在公有云上会创建的资源如下：

  VPC（1个）：用作整个 Bosh 和 Cloud Foundry 的网络运行环境

  Security Group（1个）：为网络环境设置访问权限

  EIP（1个）：与bosh director绑定，提供公网 IP，用于登录bosh director进行后续cf的部署

  ::
  

    $ git clone https://github.com/cloudfoundry-incubator/bosh-openstack-environment-templates
    $ cd bosh-openstack-environment-templates/bosh-init-tf/
    $ ./generate_ssh_keypair.sh                           //生成bosh.pem秘钥
    $ cp terraform.tfvars.template terraform.tfvars   
    $ vi terraform.tfvars                                 //修改配置文件中的值为自己公有云上的配置
    auth_url = "https://iam.eu-de.otc.t-systems.com/v3"
    domain_name = "domain_name"
    user_name = "openstack_user"
    password = "openstack_password"
    tenant_name = "eu-de"                             //也就是project的名称
    region_name = "eu-de"                       
    availability_zone = "eu-de-02"

    ext_net_name = "admin_external_net"                   //在huawei公有云上该值为固定值
    ext_net_id = "0a2228f2-7f8a-45f1-8e09-9039e1d09975"   //在huawei公有云上该值为固定值
    
    # in case your OpenStack needs custom nameservers
    # dns_nameservers = 8.8.8.8，100.125.4.25（your_own_system_private_ip） //如果后续cf的出口要用私有域名，那么这里
                                                          //的dns服务器地址一定要配置成私有dns服务器对应的dns ip，
                                                          //否则后面的私有域名无法解析，也就无法被访问，也就会导致登录不上cf。
                                                          //**添加链接**

    $ wget https://releases.hashicorp.com/terraform/0.10.7/terraform_0.10.7_linux_amd64.zip
    $ unzip terraform_0.10.7_linux_amd64.zip
    $ ./terraform init                                     //初始化terraform配置  
    $ ./terraform apply                                    //使用terraform创建资源
    ...
    Apply complete! Resources: 11 added, 0 changed, 0 destroyed.

    Outputs:

    default_key_name = bosh
    default_security_groups = [bosh]
    external_ip = 160.44.206.37
    internal_cidr = 10.0.1.0/24
    internal_gw = 10.0.1.1
    internal_ip = 10.0.1.10
    net_dns = [8.8.8.8]
    net_id = a95cd147-689c-483a-90ca-dae8c2ed938a
    router_id = bdc24a70-6a56-485e-a733-15612925759b

  创建成功以后要记录好回显的信息，作为后面的bosh director的创建的参数输入

  - 如果配置有问题，或者想清理已经创建的数据可以使用如下命令进行清理
  ::

    $./terraform destroy

  - 如果terraform创建资源的过程中发现有问题，可以设置如下的全局变量在/tmp/log_otc中查看terraform日志信息
  ::

    export TF_LOG=DEBUG
    export OS_DEBUG=1
    export TF_LOG_PATH=/tmp/log_otc

  - 也可以指定如下信息设置公有云的全局变量信息
  ::

    export OS_USERNAME=user_name
    export OS_PASSWORD=openstack_password
    export OS_TENANT_NAME=project_name
    export OS_AUTH_URL="https://iam.eu-de.otc.t-systems.com/v3"
    export OS_IDENTITY_API_VERSION=3
    export OS_USER_DOMAIN_NAME=domain_name
    export OS_PROJECT_DOMAIN_NAME=project_domain_name



**2.安装bosh director**

2.1登录到第一步创建的ubuntu执行机器上
::

  $ apt-get update
  $ apt-get sudo apt-get install -y build-essential zlibc zlib1g-dev ruby ruby-dev openssl libxslt-dev libxml2-dev libssl-dev libreadline6 libreadline6-dev libyaml-dev libsqlite3-dev sqlite3
  $ ruby -v
  ruby 2.2.3p173 (2015-08-18 revision 51636) [x86_64-darwin14]

2.2安装bosh cli
::

  $ wget https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-3.0.1-linux-amd64
  $ chmod +x bosh-cli-3.0.1-linux-amd64
  $ sudo mv ~/bosh-cli-3.0.1-linux-amd64 /usr/local/bin/bosh
  $ bosh -v
  version 3.0.1-712bfd7-2018-03-13T23:26:43Z

  Succeeded


2.3创建director
::

  $ cd /root
  $ mkdir bosh-1 && cd bosh-1
  $ git clone https://github.com/cloudfoundry/bosh-deployment
  $ vi bosh-deployment/openstack/cpi.yml                        //修改虚拟机flavor类型为公有云支持的类型
  - type: replace
    path: /resource_pools/name=vms/cloud_properties?
    value:
      instance_type: **s2.large.2**
      availability_zone: ((az))
  $ vi bosh-deployment/openstack/cloud-config.yml
  vm_types:
  - name: default
    cloud_properties:
      instance_type: **s2.large.2**
  - name: large
    cloud_properties:
      instance_type: **s2.large.8**

  $ bosh create-env bosh-deployment/bosh.yml \
      --state=state.json \
      --vars-store=creds.yml \
      -o bosh-deployment/openstack/cpi.yml \
      -o bosh-deployment/external-ip-with-registry-not-recommended.yml \
      -v director_name=bosh-1 \
      -v internal_cidr=10.0.1.0/24 \
      -v internal_gw=10.0.1.1 \
      -v internal_ip=10.0.1.10 \
      -v external_ip=160.44.206.37 \
      -v auth_url=https://iam.eu-de.otc.t-systems.com/v3 \
      -v az=eu-de-02 \
      -v default_key_name=bosh \
      -v default_security_groups=[bosh] \
      -v net_id=a95cd147-689c-483a-90ca-dae8c2ed938a \
      -v openstack_password=password \
      -v openstack_username=cloud_user \
      -v openstack_domain=cloud_domamin \
      -v openstack_project=project_name \
      -v openstack_state_timeout=30000 \
      -v state_timeout=30000 \
      -v private_key=./bosh.pem \
      -v openstack_flavor=s2.large.2 \
      -v availability_zone=eu-de-02 \
      -v region=eu-de

  $export BOSH_ENVIRONMENT=160.44.206.37
  # Configure local alias
  $ bosh alias-env bosh-1 -e 119.3.21.3 --ca-cert <(bosh int ./creds.yml --path /director_ssl/ca)

  # Log in to the Director
  $ export BOSH_CLIENT=admin
  $ export BOSH_CLIENT_SECRET=`bosh int ./creds.yml --path /admin_password`
  $ bosh -e bosh-1 l                           //登录bosh director
  Using environment '119.3.21.3'

  Using environment '119.3.21.3' as client 'admin'

  Logged in to '119.3.21.3'

  Succeeded
  $ bosh envs


**3.安装cloudfoundry**

**注意**

  老方法 `cf-release <https://bosh.io/releases/github.com/cloudfoundry/cf-release?all=1>`_ 的最后一个版本是v287，后续被 `cf-deployment <https://github.com/cloudfoundry/cf-deployment.git>`_ 替代，也可以使用 `cf-deployment-transition <https://github.com/cloudfoundry/cf-deployment-transition>`_ ，将cf-release工程迁移到cf-deployment

Notice: cf-release is now end-of-life. The final version of cf-release is v287.
cf-deployment 历史版本参考链接： https://github.com/cloudfoundry/cf-deployment/releases

**老方法使用cf-release进行部署**

* 3.1.修改 `cf-deployment.yml <https://github.com/zhongjun2/docs/blob/master/cloudfoundry/cf-deployment.yml>`_

  - 3.1.1修改director uuid
  - 3.1.2修改net_id名称为创建director时所配置的子网id
  - 3.1.3修改域名example.com为自己配置的域名
  - 3.1.4修改security group安全组为创建director时候的安全组

* 3.2上传部署cf的时候需要用到的stemcell和release包

  **注意**
  注意release的版本一定要与stemcell匹配，不然可能会导致服务cf起不来，比如下面的release使用说明中就会看到对应的release包需要哪个版本的stemcell
  https://bosh.io/releases/github.com/cloudfoundry/cf-release?version=250#usage

  上传release包可以将路径配置配置到cf-deployment.yml文件中，也可以将通过upload-release命令上传到director中，
  ::

    bosh upload-release --sha1 456a52f8a03728708252910eef90dc490bcb76a3 \
    https://bosh.io/d/github.com/cloudfoundry/cf-release?v=231

  上传镜像，用于后续创建cf所需虚拟机使用
  ::

    wget https://s3.amazonaws.com/bosh-core-stemcells/openstack/bosh-stemcell-3312.12-openstack-kvm-ubuntu-trusty-go_agent.tgz
    bosh upload-stemcell bosh-stemcell-3312.12-openstack-kvm-ubuntu-trusty-go_agent.tgz

* 3.3执行如下命令，使用 `cf-deployment.yml <https://github.com/zhongjun2/docs/blob/master/cloudfoundry/cf-deployment.yml>`_ 的配置进行部署名叫openstack-cf的cloudfoundry环境
::

  bosh -e bosh-1 -d openstack-cf deploy cf-deployment.yml

* 3.4登录cf环境，用户名为admin，密码为admin
::

  # cf login -a https://api.example.com --skip-ssl-validation
  API endpoint: https://api.example.com

  Email> admin

  Password>
  Authenticating...
  OK

  Targeted org mycloud



  API endpoint:   https://api.example.com (API version: 2.51.0)
  User:           admin
  Org:            mycloud
  Space:          No space targeted, use 'cf target -s SPACE'

**新方法使用cf-deployment进行部署**

* 3.1.再次使用terraform创建安装cf的时候需要的共有云资源
将 `terraform工程 <https://github.com/cloudfoundry-incubator/bosh-openstack-environment-templates/tree/master/cf-deployment-tf>`_下载到执行机上面，配置好terraform全局变量，运行如下命令创建cf所需资源
::

  $ terraform init <cloned-repo-path>/cf-deployment-tf
  $ terraform apply <cloned-repo-path>/cf-deployment-tf

创建完成后注意查看回显信息，回显信息中有下面步骤中所需要的网络信息，包括在同一个VPC下创建的三个不同网段的子网信息。


bosh -e bosh-1 -d openstack-cf deploy cf-deployment/cf-deployment.yml \
--vars-store cf-vars.yml \
-v system_domain=cloudfoundry.com \
-v haproxy_private_ip=192.168.10.51  \
-o cf-deployment/operations/openstack.yml \
-o cf-deployment/operations/use-haproxy.yml


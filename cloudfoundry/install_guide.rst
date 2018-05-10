

Bosh OpenStack 镜像包下载地址
https://bosh.cloudfoundry.org/stemcells/bosh-openstack-kvm-ubuntu-trusty-go_agent


cf-release 镜像包下载
https://bosh.io/releases/github.com/cloudfoundry/cf-release?all=1

这里使用231版本
https://bosh.io/d/github.com/cloudfoundry/cf-release?v=231


bosh deploy参考链接： https://bosh.io/docs/init-openstack/


**1. 准备运行环境**

从安全性考虑，本文所设计的网络环境是 VPC。为了方便部署 Bosh，首先需要准备一台带有公网 IP 跳板机作为部署命令的执行机器。因此，本节需要准备如下资源：

* 1.1.使用terraform创建安装bosh需要的公有云资源

  terraform模板参考：https://github.com/cloudfoundry-incubator/bosh-openstack-environment-templates/tree/master/bosh-init-tf

  该模板在公有云上会创建的资源如下：

  VPC（1个）：用作整个 Bosh 和 Cloud Foundry 的网络运行环境

  Security Group（1个）：为网络环境设置访问权限

  EIP（1个）：与bosh director绑定，提供公网 IP，用于登录bosh director进行后续cf的部署

  ::
  

    $ git clone https://github.com/cloudfoundry-incubator/bosh-openstack-environment-templates
    Cloning into 'bosh-openstack-environment-templates'...
    remote: Counting objects: 167, done.
    remote: Total 167 (delta 0), reused 0 (delta 0), pack-reused 167
    Receiving objects: 100% (167/167), 29.61 KiB | 47.00 KiB/s, done.
    Resolving deltas: 100% (96/96), done.
    Checking connectivity... done.
    $ cd bosh-openstack-environment-templates/bosh-init-tf/
    $ ./generate_ssh_keypair.sh                           //生成bosh.pem秘钥
    $ cp terraform.tfvars.template terraform.tfvars   
    $ vi terraform.tfvars                                 //修改配置文件中的值为自己公有云上的配置
    auth_url = "https://iam.cn-east-2.myhwclouds.com/v3"
    domain_name = "domain_name"
    user_name = "openstack_user"
    password = "openstack_password"
    tenant_name = "cn-east-2"                             //也就是project的名称
    region_name = "cn-east-2"                       
    availability_zone = "cn-east-2a"

    ext_net_name = "admin_external_net"                   //在huawei公有云上该值为固定值
    ext_net_id = "0a2228f2-7f8a-45f1-8e09-9039e1d09975"   //在huawei公有云上该值为固定值

    $ wget https://releases.hashicorp.com/terraform/0.10.7/terraform_0.10.7_linux_amd64.zip
    $ unzip terraform_0.10.7_linux_amd64.zip
    $ ./terraform init                                     //初始化terraform配置  
    $ ./terraform apply                                    //使用terraform创建资源


* 1.2.准备一台ubuntu 16.04的执行机，用以安装bosh cli和cloudfoundry cli执行部署cf的命令，以及后面部署cf成功后调用cf命令在cf上部署应用

**2.安装bosh director**

2.1登录到第一步创建的ubuntu机器上



**3.安装cloudfoundry**

3.1.再次使用terraform创建安装cf的时候需要的共有云资源
将 `terraform工程 <https://github.com/cloudfoundry-incubator/bosh-openstack-environment-templates/tree/master/cf-deployment-tf>`_下载到执行机上面，配置好terraform全局变量，运行如下命令创建cf所需资源
::

  $ terraform init <cloned-repo-path>/cf-deployment-tf
  $ terraform apply <cloned-repo-path>/cf-deployment-tf

创建完成后注意查看回显信息，回显信息中有下面步骤中所需要的网络信息，包括在同一个VPC下创建的三个不同网段的子网信息。

3.2.


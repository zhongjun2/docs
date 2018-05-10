

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


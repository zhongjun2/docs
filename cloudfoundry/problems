
使用bosh在公有云上面部署Cloudfoundry时遇到的问题
============================================

1.创建bosh director的时候当你的包下载不下来的时候，可以将包传到本地,并修改url路径为本地路径
::

  # vi bosh-deployment/openstack/cpi.yml
  ---
  - type: replace
    path: /releases/-
    value:
      name: bosh-openstack-cpi
      version: "38"
      url: file://bosh-openstack-cpi-release-38.tgz
      sha1: 9e149e64612f8a705eb9c069fd4ebf268af5ae46

  - type: replace
    path: /resource_pools/name=vms/stemcell?
    value:
      url: file://bosh-stemcell-3541.10-openstack-kvm-ubuntu-trusty-go_agent.tgz
      sha1: bcce3d6cef5e3882c214c078873793fd477db60d

How to debug manila service
===========================

* Restart manila api service

::

  sudo apache2ctl -k restart
  sudo service apache2 restart

* Restart manila service

::

  systemctl restart devstack@m-sch.service
  systemctl restart devstack@m-shr.service

* Change manila service status

::

  systemctl status devstack@m-shr.service
  sudo systemctl enable devstack@m-sch.service

*  查看所有服务
::

  systemctl list-units

*  查看日志

  manila share服务日志：
  
  ::
  
  journalctl -u devstack@m-shr.service -f | ccze
  
  manila schedule服务日志：
  
  ::
  
  journalctl -u devstack@m-sch.service -f | ccze
  
  
  nova cpu服务日志：
  
  ::
  journalctl -u devstack@n-cpu.service -f | ccze
  https://docs.openstack.org/devstack/latest/systemd.html
  
*  manila api log日志查看
::

  sudo tail -f /var/log/apache2/manila_api.log | sed -u 's/\\x1b/\o033/g'


* 修改python-manilaclient代码后如何生效，进入到python-manilaclient目录运行如下命令
::

  python setup.py install

* 检查格式问题
::

  tox -epep8 -vv
  
* 跑单元测试
::
 
  tox -epy27
  //运行一个单独的test
  tox -e py27 -- test_file_name_here.py:TestClassName.test_method_name
  stestr run manila.tests.share.test_manager
  
* 跑tempest test

https://github.com/openstack/manila/blob/master/doc/source/contributor/tempest_tests.rst

  ::

  tempest run -r manila_tempest_tests.tests.api.admin.test_admin_actions.AdminActionsTest.test_reset_share_state


* 跑API文档测试
::

  tox -e api-ref

* 跑python-manilclient的function test
::

  $ tox -e genconfig
  This will create file 'etc/manilaclient/manilaclient.conf.sample' with all available config opts. Then rename it removing   ".sample" and set values for opts there. After it, tests can be run using following tox job:

  $ tox -e functional

https://github.com/openstack/python-manilaclient/blob/master/doc/source/contributor/index.rst

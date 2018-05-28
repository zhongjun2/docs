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
::

  journalctl -u devstack@m-shr.service -f | ccze
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
 
  tox -epy27  -- -n manila.tests.share.test_access.ShareInstanceAccessDatabaseMixinTestCase
 

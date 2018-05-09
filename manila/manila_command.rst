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

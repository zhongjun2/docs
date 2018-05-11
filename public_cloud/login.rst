
* 登录公有云虚拟机
::

  # chmod 400 KeyPair-test.pem
  # ssh -i KeyPair-test.pem cloud@your_own_elastic_ip
  Permission denied (publickey).                           //如果提示该错误有可能是用户名错误，修改用户名后重新执行
  

  # ssh -i KeyPair-test.pem ubuntu@your_own_elastic_ip
  Welcome to Ubuntu 16.04.4 LTS (GNU/Linux 4.4.0-116-generic x86_64)

   * Documentation:  https://help.ubuntu.com
   * Management:     https://landscape.canonical.com
   * Support:        https://ubuntu.com/advantage

    Get cloud support with Ubuntu Advantage Cloud Guest:
      http://www.ubuntu.com/business/services/cloud

  0 packages can be updated.
  0 updates are security updates.



  The programs included with the Ubuntu system are free software;
  the exact distribution terms for each program are described in the
  individual files in /usr/share/doc/*/copyright.

  Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
  applicable law.

  To run a command as administrator (user "root"), use "sudo <command>".
  See "man sudo_root" for details.

登录成功

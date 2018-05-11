
* 登录公有云虚拟机
::

  # chmod 400 KeyPair-test.pem
  # ssh -i KeyPair-test.pem ubuntu@your_own_elastic_ip

* 登录失败可能遇到Permission denied错误
::

  # ssh -i KeyPair-test.pem cloud@your_own_elastic_ip
  Permission denied (publickey).

如果提示该错误有可能是用户名错误，修改用户名后重新执行

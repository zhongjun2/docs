

在cf上部署应用
=============


* 1.创建并指定空间
::

  $ cf create-space development
  Creating space development in org mycloud as admin...
  OK
  Assigning role RoleSpaceManager to user admin in org mycloud / space development as admin...
  OK
  Assigning role RoleSpaceDeveloper to user admin in org mycloud / space development as admin...
  OK

  TIP: Use 'cf target -o "mycloud" -s "development"' to target new space

::

  $ cf target -o "mycloud" -s "development"
  api endpoint:   https://api.example.com
  api version:    2.51.0
  user:           admin
  org:            mycloud
  space:          development


* 2.下载示例应用demo
::

  $ git clone https://github.com/cloudfoundry-samples/cf-php-demo

* 3.修改 manifest.yml文件中的域名为自己的域名，与部署cf时填写的域名一致，这里为example.com
::

  $ cd cf-php-demo-master/
  $ vi manifest.yml
  ---
  applications:
  - name: cf-php-demo
    memory: 128M
    instances: 1
    host: cf-php-demo
    domain: example.com
    path: .
    buildpack: https://github.com/dmikusa-pivotal/cf-php-apache-buildpack.git

* 4.推送应用
::

  cf push myapp -b php_buildpack

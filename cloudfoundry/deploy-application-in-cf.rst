

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

  $ cf push myapp -b php_buildpack

注： -m 1G 参数选择应用存储空间大小

* 查看app状态
::

  $ cf apps
  Getting apps in org mycloud / space development as admin...
  OK

  name     requested state   instances   memory   disk   urls
  myapp    started           1/1         128M     1G     cf-php-demo.example.com

* 重启app
::

  $ cf restart myapp
  Restarting app myapp in org mycloud / space development as admin...

  Stopping app...

  Waiting for app to start...

  name:              myapp
  requested state:   started
  instances:         1/1
  usage:             128M x 1 instances
  routes:            cf-php-demo.example.com:0
  last uploaded:     Tue 15 May 03:39:05 UTC 2018
  stack:             cflinuxfs2
  buildpack:         php_buildpack
  start command:     $HOME/.bp/bin/start

       state     since                  cpu    memory          disk           details
  #0   running   2018-05-15T07:24:17Z   0.3%   62.9M of 128M   125.1M of 1G
  
  
* 扩容
::

  cf scale APP_NAME [-i INSTANCES] [-k DISK] [-m MEMORY] [-f]
  
  OPTIONS
  -f
  Force restart of app without prompt

  -i
  Number of instances

  -k
  Disk limit (e.g. 256M, 1024M, 1G)

  -m
  Memory limit (e.g. 256M, 1024M, 1G)
  
  https://cli.cloudfoundry.org/en-US/cf/scale.html


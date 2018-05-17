

在cf上部署应用
=============

* 1.登录cloud foundry，其中“example.com”根据实际域名替换（前面配置的DNS就是example.com，因此不用更改），默认用户名为admin，默认密码为admin。登录后显示如下
# cf login -a https://api.example.com --skip-ssl-validation
API endpoint: https://api.example.com

Email> admin

Password>
Authenticating...
OK

Targeted org mycloud



API endpoint:   https://api.example.com (API version: 2.51.0)
User:           admin
Org:            mycloud
Space:          No space targeted, use 'cf target -s SPACE'

* 2.创建并指定空间，默认创建名为mycloud的组织org，以及名为development的space空间，一个org组织下可以包含多个空间，每个空间下可以部署多个应用
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


* 3.下载示例应用demo
::

  $ git clone https://github.com/cloudfoundry-samples/cf-php-demo

* 3.修改 manifest.yml文件中的域名为自己的域名，与部署cf时填写的域名一致，这里为example.com
::

  $ cd cf-php-demo/
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

应用推送成功后即可通过curl： https://cf-php-demo.example.com 访问该应用。你也可以为一个应用配置多个urls访问该应用


* 部署第二个应用wordpress


# 下载 wordpress 并解压
::

  $ wget https://wordpress.org/latest.zip
  $ unzip latest.zip && cd wordpress

# 创建应用空间，由于在第一条中以及创建好了名为mycloud的org组织，因此这里在该组织下又创建了一个新的名为wordpress的空间
::

  $ cf create-space wordpress -o mycloud
    
# 指定目标组织
::

  $ cf target -o "mycloud" -s "wordpress"
    
# 查看已经存在的应用空间，包括development和wordpress两个
::

  $ cf spaces
  Getting spaces in org mycloud as admin...

  name
  development
  wordpress

    
# 发布 wordpress
::

  $ cf push wordpress -b php_buildpack


应用相关操作
================

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
  
  
  


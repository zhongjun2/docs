  
::

  # cf scale wordpress -i 2
  Scaling app wordpress in org mycloud / space wordpress as admin...
  OK
  root@ecs-zhongjun:~/bosh-1# cf apps
  Getting apps in org mycloud / space wordpress as admin...
  OK

  name        requested state   instances   memory   disk   urls
  wordpress   started           2/2         1G       1G     wordpress.example.com
  root@ecs-zhongjun:~/bosh-1# cf scale wordpress -k 3G

  This will cause the app to restart. Are you sure you want to scale wordpress?> yes

  Scaling app wordpress in org mycloud / space wordpress as admin...
  FAILED
  Server error, status code: 400, error code: 100001, message: The app is invalid: disk_quota too much disk requested (must be less than 2048)
  root@ecs-zhongjun:~/bosh-1# cf scale wordpress -k 3
  FAILED
  Invalid disk quota: 3
  Byte quantity must be an integer with a unit of measurement like M, MB, G, or GB
  root@ecs-zhongjun:~/bosh-1# cf scale wordpress -k 3G

  This will cause the app to restart. Are you sure you want to scale wordpress?> y

  Scaling app wordpress in org mycloud / space wordpress as admin...
  FAILED
  Server error, status code: 400, error code: 100001, message: The app is invalid: disk_quota too much disk requested (must be less than 2048)
  root@ecs-zhongjun:~/bosh-1# cf scale wordpress -k 2G

  This will cause the app to restart. Are you sure you want to scale wordpress?> y

  Scaling app wordpress in org mycloud / space wordpress as admin...
  OK
  Stopping app wordpress in org mycloud / space wordpress as admin...
  OK

  Starting app wordpress in org mycloud / space wordpress as admin...

  0 of 2 instances running, 2 starting
  2 of 2 instances running

  App started


  OK

  App wordpress was started using this command `$HOME/.bp/bin/start`

  Showing health and status for app wordpress in org mycloud / space wordpress as admin...
  OK

  requested state: started
  instances: 2/2
  usage: 1G x 2 instances
  urls: wordpress.example.com
  last uploaded: Tue May 15 07:58:03 UTC 2018
  stack: cflinuxfs2
  buildpack: php_buildpack

       state     since                    cpu    memory      disk           details
  #0   running   2018-05-15 10:06:03 AM   0.2%   70M of 1G   153.8M of 2G
  #1   running   2018-05-15 10:06:03 AM   0.2%   70M of 1G   153.8M of 2G

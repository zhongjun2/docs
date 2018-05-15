::

  # cf app wordpress
  Showing health and status for app wordpress in org mycloud / space wordpress as admin...

  name:              wordpress
  requested state:   started
  instances:         2/2
  usage:             1G x 2 instances
  routes:            wordpress.example.com:0
  last uploaded:     Tue 15 May 07:58:03 UTC 2018
  stack:             cflinuxfs2
  buildpack:         php_buildpack

       state     since                  cpu    memory      disk           details
  #0   running   2018-05-15T10:06:03Z   0.2%   70M of 1G   153.8M of 2G
  #1   running   2018-05-15T10:06:03Z   0.2%   70M of 1G   153.8M of 2G
  root@ecs-zhongjun:~/bosh-1# cf apps
  Getting apps in org mycloud / space wordpress as admin...
  OK

  name        requested state   instances   memory   disk   urls
  wordpress   started           2/2         1G       2G     wordpress.example.com

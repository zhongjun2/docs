

::

  $ cf push myapp -b php_buildpack
    Pushing from manifest to org mycloud / space development as admin...
    Using manifest file /root/bosh-1/cf-php-demo/manifest.yml


    Deprecation warning: Route component attributes 'domain', 'domains', 'host', 'hosts' and 'no-hostname' are deprecated. Found: domain, host.
    Please see http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#deprecated for the currently supported syntax and other app manifest deprecations. This feature will be removed in the future.


    Using manifest file /root/bosh-1/cf-php-demo/manifest.yml

    Updating app myapp in org mycloud / space development as admin...
    OK

    Creating route cf-php-demo-zj.example.com...
    OK

    Binding cf-php-demo-zj.example.com to myapp...
    OK

    Uploading myapp...
    Uploading app files from: /root/bosh-1/cf-php-demo
    Uploading 50.4K, 13 files
    Done uploading
    OK

    Stopping app myapp in org mycloud / space development as admin...
    OK

    Starting app myapp in org mycloud / space development as admin...
    -----> Downloaded app package (88K)
    -----> Downloaded app buildpack cache (4.0K)
    -------> Buildpack version 4.3.5
    Installing HTTPD
    Downloaded [file:///var/vcap/data/dea_next/admin_buildpacks/39af28f6-40da-46ef-b094-37b51bb28f1c_4e7dbfdd1804fa0c052fb19dc5e349c3852180ca/dependencies/https___pivotal-buildpacks.s3.amazonaws.com_concourse-binaries_httpd_httpd-2.4.18-linux-x64.tgz] to [/tmp]
    Installing PHP
    PHP 5.5.32
    Downloaded [file:///var/vcap/data/dea_next/admin_buildpacks/39af28f6-40da-46ef-b094-37b51bb28f1c_4e7dbfdd1804fa0c052fb19dc5e349c3852180ca/dependencies/https___pivotal-buildpacks.s3.amazonaws.com_concourse-binaries_php_php-5.5.32-linux-x64-1455291679.tgz] to [/tmp]
    Finished: [2018-05-15 07:28:18.621247]

    -----> Uploading droplet (45M)

    Could not fetch instance count: Server error, status code: 500, error code: 10001, message: An unknown error occurred.
    1 of 1 instances running

    App started


    OK

    App myapp was started using this command `$HOME/.bp/bin/start`

    Showing health and status for app myapp in org mycloud / space development as admin...
    OK

    requested state: started
    instances: 1/1
    usage: 128M x 1 instances
    urls: cf-php-demo.example.com, cf-php-demo-zj.example.com
    last uploaded: Tue May 15 07:28:07 UTC 2018
    stack: cflinuxfs2
    buildpack: php_buildpack

         state     since                    cpu    memory          disk           details
    #0   running   2018-05-15 07:28:40 AM   0.3%   61.5M of 128M   125.1M of 1G



::

  # cf push wordpress -b php_buildpack
  Pushing app wordpress to org mycloud / space wordpress as admin...
  Getting app info...
  Creating app with these attributes...
  + name:        wordpress
    path:        /root/bosh-1/wordpress
  + buildpack:   php_buildpack
    routes:
  +   wordpress.example.com

  Creating app wordpress...
  Mapping routes...
  Comparing local files to remote cache...
  Packaging files to upload...
  Uploading files...
   8.91 MiB / 8.91 MiB [=============================================================================================================================================================================] 100.00% 1s

  Waiting for API to complete processing files...

  Staging app and tracing logs...
     -----> Uploading droplet (53M)

  Waiting for app to start...

  name:              wordpress
  requested state:   started
  instances:         1/1
  usage:             1G x 1 instances
  routes:            wordpress.example.com:0
  last uploaded:     Tue 15 May 07:58:03 UTC 2018
  stack:             cflinuxfs2
  buildpack:         php_buildpack
  start command:     $HOME/.bp/bin/start

       state     since                  cpu    memory      disk           details
  #0   running   2018-05-15T07:58:27Z   0.0%   72M of 1G   153.8M of 1G



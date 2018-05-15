

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


::

  # bosh -e bosh-1 -d openstack-cf deploy cf-deployment.yml
  Using environment '160.44.202.46' as client 'admin'

  Using deployment 'openstack-cf'

  + resource_pools:
  + - cloud_properties:
  +     instance_type: s2.large.2
  +   env:
  +     bosh:
  +       password: "<redacted>"
  +   name: small_z1
  +   network: cf1
  +   stemcell:
  +     name: bosh-openstack-kvm-ubuntu-trusty-go_agent
  +     version: '3312.12'
  + - cloud_properties:
  +     instance_type: s2.large.2
  +   env:
  +     bosh:
  +       password: "<redacted>"
  +   name: small_z2
  +   network: cf2
  +   stemcell:
  +     name: bosh-openstack-kvm-ubuntu-trusty-go_agent
  +     version: '3312.12'
  + - cloud_properties:
  +     instance_type: s2.large.2
  +   env:
  +     bosh:
  +       password: "<redacted>"
  +   name: medium_z1
  +   network: cf1
  +   stemcell:
  +     name: bosh-openstack-kvm-ubuntu-trusty-go_agent
  +     version: '3312.12'
  + - cloud_properties:
  +     instance_type: s2.large.2
  +   env:
  +     bosh:
  +       password: "<redacted>"
  +   name: medium_z2
  +   network: cf2
  +   stemcell:
  +     name: bosh-openstack-kvm-ubuntu-trusty-go_agent
  +     version: '3312.12'
  + - cloud_properties:
  +     instance_type: s2.large.2
  +   env:
  +     bosh:
  +       password: "<redacted>"
  +   name: large_z1
  +   network: cf1
  +   stemcell:
  +     name: bosh-openstack-kvm-ubuntu-trusty-go_agent
  +     version: '3312.12'
  + - cloud_properties:
  +     instance_type: s2.large.2
  +   env:
  +     bosh:
  +       password: "<redacted>"
  +   name: large_z2
  +   network: cf2
  +   stemcell:
  +     name: bosh-openstack-kvm-ubuntu-trusty-go_agent
  +     version: '3312.12'
  + - cloud_properties:
  +     instance_type: s2.large.2
  +   env:
  +     bosh:
  +       password: "<redacted>"
  +   name: runner_z1
  +   network: cf1
  +   stemcell:
  +     name: bosh-openstack-kvm-ubuntu-trusty-go_agent
  +     version: '3312.12'
  + - cloud_properties:
  +     instance_type: s2.large.2
  +   env:
  +     bosh:
  +       password: "<redacted>"
  +   name: runner_z2
  +   network: cf2
  +   stemcell:
  +     name: bosh-openstack-kvm-ubuntu-trusty-go_agent
  +     version: '3312.12'
  + - cloud_properties:
  +     instance_type: s2.large.2
  +   env:
  +     bosh:
  +       password: "<redacted>"
  +   name: router_z1
  +   network: cf1
  +   stemcell:
  +     name: bosh-openstack-kvm-ubuntu-trusty-go_agent
  +     version: '3312.12'
  + - cloud_properties:
  +     instance_type: s2.large.2
  +   env:
  +     bosh:
  +       password: "<redacted>"
  +   name: router_z2
  +   network: cf2
  +   stemcell:
  +     name: bosh-openstack-kvm-ubuntu-trusty-go_agent
  +     version: '3312.12'
  + - cloud_properties:
  +     instance_type: s2.large.2
  +   env:
  +     bosh:
  +       password: "<redacted>"
  +   name: small_errand
  +   network: cf1
  +   stemcell:
  +     name: bosh-openstack-kvm-ubuntu-trusty-go_agent
  +     version: '3312.12'
  + - cloud_properties:
  +     instance_type: s2.large.2
  +   env:
  +     bosh:
  +       password: "<redacted>"
  +   name: xlarge_errand
  +   network: cf1
  +   stemcell:
  +     name: bosh-openstack-kvm-ubuntu-trusty-go_agent
  +     version: '3312.12'

  + compilation:
  +   cloud_properties:
  +     instance_type: s2.large.2
  +   network: cf1
  +   reuse_compilation_vms: true
  +   workers: 6

  + networks:
  + - cloud_properties:
  +     net_id: a95cd147-689c-483a-90ca-dae8c2ed938a
  +     security_groups:
  +     - bosh
  +   name: floating
  +   type: vip
  + - name: cf1
  +   subnets:
  +   - cloud_properties:
  +       net_id: a95cd147-689c-483a-90ca-dae8c2ed938a
  +       security_groups:
  +       - bosh
  +     dns:
  +     - 10.0.1.250
  +     gateway: 10.0.1.1
  +     range: 10.0.1.0/24
  +     reserved:
  +     - 10.0.1.2 - 10.0.1.100
  +     - 10.0.1.200 - 10.0.1.254
  +     static:
  +     - 10.0.1.130 - 10.0.1.175
  +   type: manual
  + - name: cf2
  +   subnets:
  +   - cloud_properties:
  +       net_id: a95cd147-689c-483a-90ca-dae8c2ed938a
  +       security_groups:
  +       - bosh
  +     dns:
  +     - 10.0.1.250
  +     gateway: 10.0.1.1
  +     range: 10.0.1.0/24
  +     reserved:
  +     - 10.0.1.2 - 10.0.1.100
  +     - 10.0.1.200 - 10.0.1.254
  +     static:
  +     - 10.0.1.130 - 10.0.1.175
  +   type: manual

  + releases:
  + - name: cf
  +   version: '231'

  + update:
  +   canaries: 1
  +   canary_watch_time: 30000-600000
  +   max_in_flight: 1
  +   serial: true
  +   update_watch_time: 5000-600000

  + jobs:
  + - instances: 1
  +   name: consul_z1
  +   networks:
  +   - name: cf1
  +     static_ips:
  +     - 10.0.1.142
  +   persistent_disk: 1024
  +   properties:
  +     consul:
  +       agent:
  +         mode: "<redacted>"
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: small_z1
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update:
  +     max_in_flight: 1
  +     serial: true
  + - instances: 0
  +   name: consul_z2
  +   networks:
  +   - name: cf2
  +     static_ips: []
  +   persistent_disk: 1024
  +   properties:
  +     consul:
  +       agent:
  +         mode: "<redacted>"
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: small_z2
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update:
  +     max_in_flight: 1
  +     serial: true
  + - default_networks:
  +   - name: cf1
  +     static_ips:
  +   instances: 1
  +   name: ha_proxy_z1
  +   networks:
  +   - name: floating
  +     static_ips:
  +     - 80.158.18.188
  +   - default:
  +     - dns
  +     - gateway
  +     name: cf1
  +     static_ips:
  +     - 10.0.1.130
  +   properties:
  +     ha_proxy:
  +       ssl_pem: "<redacted>"
  +     metron_agent:
  +       zone: "<redacted>"
  +     router:
  +       servers:
  +         z1:
  +         - "<redacted>"
  +         z2: []
  +   resource_pool: router_z1
  +   templates:
  +   - name: haproxy
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   - name: consul_agent
  +     release: cf
  +   update: {}
  + - instances: 1
  +   name: nats_z1
  +   networks:
  +   - name: cf1
  +     static_ips:
  +     - 10.0.1.132
  +   properties:
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: medium_z1
  +   templates:
  +   - name: nats
  +     release: cf
  +   - name: nats_stream_forwarder
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update: {}
  + - instances: 0
  +   name: nats_z2
  +   networks:
  +   - name: cf2
  +     static_ips: []
  +   properties:
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: medium_z2
  +   templates:
  +   - name: nats
  +     release: cf
  +   - name: nats_stream_forwarder
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update: {}
  + - instances: 1
  +   name: etcd_z1
  +   networks:
  +   - name: cf1
  +     static_ips:
  +     - 10.0.1.138
  +   persistent_disk: 10024
  +   properties:
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: medium_z1
  +   templates:
  +   - name: etcd
  +     release: cf
  +   - name: etcd_metrics_server
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update:
  +     max_in_flight: 1
  + - instances: 0
  +   name: etcd_z2
  +   networks:
  +   - name: cf2
  +     static_ips: []
  +   persistent_disk: 10024
  +   properties:
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: medium_z2
  +   templates:
  +   - name: etcd
  +     release: cf
  +   - name: etcd_metrics_server
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update:
  +     max_in_flight: 1
  + - instances: 1
  +   name: stats_z1
  +   networks:
  +   - name: cf1
  +   properties:
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: small_z1
  +   templates:
  +   - name: collector
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update: {}
  + - instances: 1
  +   name: nfs_z1
  +   networks:
  +   - name: cf1
  +     static_ips:
  +     - 10.0.1.133
  +   persistent_disk: 102400
  +   properties:
  +     consul:
  +       agent:
  +         services:
  +           blobstore: {}
  +     metron_agent:
  +       zone: "<redacted>"
  +     route_registrar:
  +       routes:
  +       - name: "<redacted>"
  +         port: "<redacted>"
  +         registration_interval: "<redacted>"
  +         tags:
  +           component: "<redacted>"
  +         uris:
  +         - "<redacted>"
  +   resource_pool: medium_z1
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: debian_nfs_server
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   - name: route_registrar
  +     release: cf
  +   update: {}
  + - instances: 0
  +   name: blobstore_z1
  +   networks:
  +   - name: cf1
  +     static_ips:
  +   persistent_disk: 102400
  +   properties:
  +     consul:
  +       agent:
  +         services:
  +           blobstore: {}
  +     metron_agent:
  +       zone: "<redacted>"
  +     route_registrar:
  +       routes:
  +       - name: "<redacted>"
  +         port: "<redacted>"
  +         registration_interval: "<redacted>"
  +         tags:
  +           component: "<redacted>"
  +         uris:
  +         - "<redacted>"
  +   resource_pool: medium_z1
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   - name: blobstore
  +     release: cf
  +   - name: route_registrar
  +     release: cf
  +   update: {}
  + - instances: 1
  +   name: postgres_z1
  +   networks:
  +   - name: cf1
  +     static_ips:
  +     - 10.0.1.134
  +   persistent_disk: 4096
  +   properties:
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: medium_z1
  +   templates:
  +   - name: postgres
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update: {}
  + - instances: 1
  +   name: uaa_z1
  +   networks:
  +   - name: cf1
  +   properties:
  +     consul:
  +       agent:
  +         services:
  +           uaa: {}
  +     metron_agent:
  +       zone: "<redacted>"
  +     route_registrar:
  +       routes:
  +       - name: "<redacted>"
  +         port: "<redacted>"
  +         registration_interval: "<redacted>"
  +         tags:
  +           component: "<redacted>"
  +         uris:
  +         - "<redacted>"
  +         - "<redacted>"
  +         - "<redacted>"
  +         - "<redacted>"
  +     uaa:
  +       proxy:
  +         servers:
  +         - "<redacted>"
  +   resource_pool: medium_z1
  +   templates:
  +   - name: uaa
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   - name: consul_agent
  +     release: cf
  +   - name: route_registrar
  +     release: cf
  +   - name: statsd-injector
  +     release: cf
  +   update: {}
  + - instances: 0
  +   name: uaa_z2
  +   networks:
  +   - name: cf2
  +   properties:
  +     consul:
  +       agent:
  +         services:
  +           uaa: {}
  +     metron_agent:
  +       zone: "<redacted>"
  +     route_registrar:
  +       routes:
  +       - name: "<redacted>"
  +         port: "<redacted>"
  +         registration_interval: "<redacted>"
  +         tags:
  +           component: "<redacted>"
  +         uris:
  +         - "<redacted>"
  +         - "<redacted>"
  +         - "<redacted>"
  +         - "<redacted>"
  +     uaa:
  +       proxy:
  +         servers:
  +         - "<redacted>"
  +   resource_pool: medium_z2
  +   templates:
  +   - name: uaa
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   - name: consul_agent
  +     release: cf
  +   - name: route_registrar
  +     release: cf
  +   - name: statsd-injector
  +     release: cf
  +   update: {}
  + - instances: 1
  +   name: api_z1
  +   networks:
  +   - name: cf1
  +   persistent_disk: 0
  +   properties:
  +     consul:
  +       agent:
  +         services:
  +           cloud_controller_ng: {}
  +     metron_agent:
  +       zone: "<redacted>"
  +     nfs_server:
  +       address: "<redacted>"
  +       allow_from_entries:
  +       - "<redacted>"
  +       - "<redacted>"
  +       share: "<redacted>"
  +     route_registrar:
  +       routes:
  +       - name: "<redacted>"
  +         port: "<redacted>"
  +         registration_interval: "<redacted>"
  +         tags:
  +           component: "<redacted>"
  +         uris:
  +         - "<redacted>"
  +   resource_pool: large_z1
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: go-buildpack
  +     release: cf
  +   - name: binary-buildpack
  +     release: cf
  +   - name: nodejs-buildpack
  +     release: cf
  +   - name: ruby-buildpack
  +     release: cf
  +   - name: php-buildpack
  +     release: cf
  +   - name: python-buildpack
  +     release: cf
  +   - name: staticfile-buildpack
  +     release: cf
  +   - name: cloud_controller_ng
  +     release: cf
  +   - name: cloud_controller_clock
  +     release: cf
  +   - name: cloud_controller_worker
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   - name: statsd-injector
  +     release: cf
  +   - name: nfs_mounter
  +     release: cf
  +   - name: route_registrar
  +     release: cf
  +   update: {}
  + - instances: 0
  +   name: api_z2
  +   networks:
  +   - name: cf2
  +   persistent_disk: 0
  +   properties:
  +     consul:
  +       agent:
  +         services:
  +           cloud_controller_ng: {}
  +     metron_agent:
  +       zone: "<redacted>"
  +     nfs_server:
  +       address: "<redacted>"
  +       allow_from_entries:
  +       - "<redacted>"
  +       - "<redacted>"
  +       share: "<redacted>"
  +     route_registrar:
  +       routes:
  +       - name: "<redacted>"
  +         port: "<redacted>"
  +         registration_interval: "<redacted>"
  +         tags:
  +           component: "<redacted>"
  +         uris:
  +         - "<redacted>"
  +   resource_pool: large_z2
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: go-buildpack
  +     release: cf
  +   - name: binary-buildpack
  +     release: cf
  +   - name: nodejs-buildpack
  +     release: cf
  +   - name: ruby-buildpack
  +     release: cf
  +   - name: php-buildpack
  +     release: cf
  +   - name: python-buildpack
  +     release: cf
  +   - name: staticfile-buildpack
  +     release: cf
  +   - name: cloud_controller_ng
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   - name: statsd-injector
  +     release: cf
  +   - name: nfs_mounter
  +     release: cf
  +   - name: route_registrar
  +     release: cf
  +   update: {}
  + - instances: 0
  +   name: clock_global
  +   networks:
  +   - name: cf1
  +   persistent_disk: 0
  +   properties:
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: medium_z1
  +   templates:
  +   - name: cloud_controller_clock
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update: {}
  + - instances: 0
  +   name: api_worker_z1
  +   networks:
  +   - name: cf1
  +   persistent_disk: 0
  +   properties:
  +     metron_agent:
  +       zone: "<redacted>"
  +     nfs_server:
  +       address: "<redacted>"
  +       allow_from_entries:
  +       - "<redacted>"
  +       - "<redacted>"
  +       share: "<redacted>"
  +   resource_pool: small_z1
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: nfs_mounter
  +     release: cf
  +   - name: cloud_controller_worker
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update: {}
  + - instances: 0
  +   name: api_worker_z2
  +   networks:
  +   - name: cf2
  +   persistent_disk: 0
  +   properties:
  +     metron_agent:
  +       zone: "<redacted>"
  +     nfs_server:
  +       address: "<redacted>"
  +       allow_from_entries:
  +       - "<redacted>"
  +       - "<redacted>"
  +       share: "<redacted>"
  +   resource_pool: small_z2
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: nfs_mounter
  +     release: cf
  +   - name: cloud_controller_worker
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update: {}
  + - instances: 1
  +   name: hm9000_z1
  +   networks:
  +   - name: cf1
  +   properties:
  +     consul:
  +       agent:
  +         services:
  +           hm9000: {}
  +     metron_agent:
  +       zone: "<redacted>"
  +     route_registrar:
  +       routes:
  +       - name: "<redacted>"
  +         port: "<redacted>"
  +         registration_interval: "<redacted>"
  +         tags:
  +           component: "<redacted>"
  +         uris:
  +         - "<redacted>"
  +   resource_pool: medium_z1
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: hm9000
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   - name: route_registrar
  +     release: cf
  +   update: {}
  + - instances: 0
  +   name: hm9000_z2
  +   networks:
  +   - name: cf2
  +   properties:
  +     consul:
  +       agent:
  +         services:
  +           hm9000: {}
  +     metron_agent:
  +       zone: "<redacted>"
  +     route_registrar:
  +       routes:
  +       - name: "<redacted>"
  +         port: "<redacted>"
  +         registration_interval: "<redacted>"
  +         tags:
  +           component: "<redacted>"
  +         uris:
  +         - "<redacted>"
  +   resource_pool: medium_z2
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: hm9000
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   - name: route_registrar
  +     release: cf
  +   update: {}
  + - instances: 1
  +   name: runner_z1
  +   networks:
  +   - name: cf1
  +     static_ips:
  +   properties:
  +     consul:
  +       agent:
  +         services:
  +           dea:
  +             check:
  +               interval: "<redacted>"
  +               name: "<redacted>"
  +               script: "<redacted>"
  +               status: "<redacted>"
  +     dea_next:
  +       zone: "<redacted>"
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: runner_z1
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: dea_next
  +     release: cf
  +   - name: dea_logging_agent
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update:
  +     max_in_flight: 1
  + - instances: 0
  +   name: runner_z2
  +   networks:
  +   - name: cf2
  +     static_ips:
  +   properties:
  +     consul:
  +       agent:
  +         services:
  +           dea:
  +             check:
  +               interval: "<redacted>"
  +               name: "<redacted>"
  +               script: "<redacted>"
  +               status: "<redacted>"
  +     dea_next:
  +       zone: "<redacted>"
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: runner_z2
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: dea_next
  +     release: cf
  +   - name: dea_logging_agent
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update:
  +     max_in_flight: 1
  + - instances: 0
  +   name: loggregator_z1
  +   networks:
  +   - name: cf1
  +   properties:
  +     doppler:
  +       zone: "<redacted>"
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: medium_z1
  +   templates:
  +   - name: doppler
  +     release: cf
  +   - name: syslog_drain_binder
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update: {}
  + - instances: 0
  +   name: loggregator_z2
  +   networks:
  +   - name: cf2
  +   properties:
  +     doppler:
  +       zone: "<redacted>"
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: medium_z2
  +   templates:
  +   - name: doppler
  +     release: cf
  +   - name: syslog_drain_binder
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update: {}
  + - instances: 1
  +   name: doppler_z1
  +   networks:
  +   - name: cf1
  +   properties:
  +     doppler:
  +       zone: "<redacted>"
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: medium_z1
  +   templates:
  +   - name: doppler
  +     release: cf
  +   - name: syslog_drain_binder
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update: {}
  + - instances: 0
  +   name: doppler_z2
  +   networks:
  +   - name: cf2
  +   properties:
  +     doppler:
  +       zone: "<redacted>"
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: medium_z2
  +   templates:
  +   - name: doppler
  +     release: cf
  +   - name: syslog_drain_binder
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update: {}
  + - instances: 1
  +   name: loggregator_trafficcontroller_z1
  +   networks:
  +   - name: cf1
  +   properties:
  +     metron_agent:
  +       zone: "<redacted>"
  +     route_registrar:
  +       routes:
  +       - name: "<redacted>"
  +         port: "<redacted>"
  +         registration_interval: "<redacted>"
  +         uris:
  +         - "<redacted>"
  +       - name: "<redacted>"
  +         port: "<redacted>"
  +         registration_interval: "<redacted>"
  +         uris:
  +         - "<redacted>"
  +     traffic_controller:
  +       zone: "<redacted>"
  +   resource_pool: small_z1
  +   templates:
  +   - name: loggregator_trafficcontroller
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   - name: route_registrar
  +     release: cf
  +   update: {}
  + - instances: 0
  +   name: loggregator_trafficcontroller_z2
  +   networks:
  +   - name: cf2
  +   properties:
  +     metron_agent:
  +       zone: "<redacted>"
  +     route_registrar:
  +       routes:
  +       - name: "<redacted>"
  +         port: "<redacted>"
  +         registration_interval: "<redacted>"
  +         uris:
  +         - "<redacted>"
  +       - name: "<redacted>"
  +         port: "<redacted>"
  +         registration_interval: "<redacted>"
  +         uris:
  +         - "<redacted>"
  +     traffic_controller:
  +       zone: "<redacted>"
  +   resource_pool: small_z2
  +   templates:
  +   - name: loggregator_trafficcontroller
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   - name: route_registrar
  +     release: cf
  +   update: {}
  + - default_networks:
  +   - name: cf1
  +     static_ips:
  +   instances: 1
  +   name: router_z1
  +   networks:
  +   - name: cf1
  +     static_ips:
  +     - 10.0.1.135
  +   properties:
  +     consul:
  +       agent:
  +         services:
  +           gorouter: {}
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: router_z1
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: gorouter
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update: {}
  + - default_networks:
  +   - name: cf2
  +     static_ips:
  +   instances: 0
  +   name: router_z2
  +   networks:
  +   - name: cf2
  +     static_ips: []
  +   properties:
  +     consul:
  +       agent:
  +         services:
  +           gorouter: {}
  +     metron_agent:
  +       zone: "<redacted>"
  +   resource_pool: router_z2
  +   templates:
  +   - name: consul_agent
  +     release: cf
  +   - name: gorouter
  +     release: cf
  +   - name: metron_agent
  +     release: cf
  +   update: {}
  + - instances: 1
  +   lifecycle: errand
  +   name: acceptance_tests
  +   networks:
  +   - name: cf1
  +   resource_pool: small_errand
  +   templates:
  +   - name: acceptance-tests
  +     release: cf
  + - instances: 0
  +   lifecycle: errand
  +   name: smoke_tests
  +   networks:
  +   - name: cf1
  +   properties: {}
  +   resource_pool: small_errand
  +   templates:
  +   - name: smoke-tests
  +     release: cf

  + director_uuid: 20bf6217-3630-4c53-8fbf-9229c7e61d4f

  + meta:
  +   environment: openstack-cf
  +   releases:
  +   - name: cf
  +     version: latest

  + name: openstack-cf

  + properties:
  +   acceptance_tests: "<redacted>"
  +   app_domains:
  +   - "<redacted>"
  +   app_ssh: "<redacted>"
  +   blobstore:
  +     admin_users:
  +     - password: "<redacted>"
  +       username: "<redacted>"
  +     port: "<redacted>"
  +     secure_link:
  +       secret: "<redacted>"
  +   cc:
  +     allow_app_ssh_access: "<redacted>"
  +     allowed_cors_domains: []
  +     app_events:
  +       cutoff_age_in_days: "<redacted>"
  +     app_usage_events:
  +       cutoff_age_in_days: "<redacted>"
  +     audit_events:
  +       cutoff_age_in_days: "<redacted>"
  +     broker_client_default_async_poll_interval_seconds: "<redacted>"
  +     broker_client_max_async_poll_duration_minutes: "<redacted>"
  +     broker_client_timeout_seconds: "<redacted>"
  +     buildpacks:
  +       blobstore_type: "<redacted>"
  +       buildpack_directory_key: "<redacted>"
  +       cdn: "<redacted>"
  +       fog_connection: "<redacted>"
  +       webdav_config:
  +         password: "<redacted>"
  +         private_endpoint: "<redacted>"
  +         public_endpoint: "<redacted>"
  +         secret: "<redacted>"
  +         username: "<redacted>"
  +     bulk_api_password: "<redacted>"
  +     client_max_body_size: "<redacted>"
  +     db_encryption_key: "<redacted>"
  +     db_logging_level: "<redacted>"
  +     default_app_disk_in_mb: "<redacted>"
  +     default_app_memory: "<redacted>"
  +     default_buildpacks:
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     default_health_check_timeout: "<redacted>"
  +     default_quota_definition: "<redacted>"
  +     default_running_security_groups:
  +     - "<redacted>"
  +     - "<redacted>"
  +     default_staging_security_groups:
  +     - "<redacted>"
  +     - "<redacted>"
  +     default_to_diego_backend: "<redacted>"
  +     development_mode: "<redacted>"
  +     directories: "<redacted>"
  +     disable_custom_buildpacks: "<redacted>"
  +     droplets:
  +       blobstore_type: "<redacted>"
  +       cdn: "<redacted>"
  +       droplet_directory_key: "<redacted>"
  +       fog_connection: "<redacted>"
  +       max_staged_droplets_stored: "<redacted>"
  +       webdav_config:
  +         password: "<redacted>"
  +         private_endpoint: "<redacted>"
  +         public_endpoint: "<redacted>"
  +         secret: "<redacted>"
  +         username: "<redacted>"
  +     external_host: "<redacted>"
  +     external_port: "<redacted>"
  +     external_protocol: "<redacted>"
  +     install_buildpacks:
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     internal_api_password: "<redacted>"
  +     internal_api_user: "<redacted>"
  +     jobs:
  +       app_bits_packer:
  +         timeout_in_seconds: "<redacted>"
  +       app_events_cleanup:
  +         timeout_in_seconds: "<redacted>"
  +       app_usage_events_cleanup:
  +         timeout_in_seconds: "<redacted>"
  +       blobstore_delete:
  +         timeout_in_seconds: "<redacted>"
  +       blobstore_upload:
  +         timeout_in_seconds: "<redacted>"
  +       droplet_deletion:
  +         timeout_in_seconds: "<redacted>"
  +       droplet_upload:
  +         timeout_in_seconds: "<redacted>"
  +       generic:
  +         number_of_workers: "<redacted>"
  +       global:
  +         timeout_in_seconds: "<redacted>"
  +       model_deletion:
  +         timeout_in_seconds: "<redacted>"
  +     logging_level: "<redacted>"
  +     maximum_app_disk_in_mb: "<redacted>"
  +     maximum_health_check_timeout: "<redacted>"
  +     min_cli_version: "<redacted>"
  +     min_recommended_cli_version: "<redacted>"
  +     newrelic:
  +       capture_params: "<redacted>"
  +       developer_mode: "<redacted>"
  +       environment_name: "<redacted>"
  +       license_key: "<redacted>"
  +       monitor_mode: "<redacted>"
  +       transaction_tracer:
  +         enabled: "<redacted>"
  +         record_sql: "<redacted>"
  +     packages:
  +       app_package_directory_key: "<redacted>"
  +       blobstore_type: "<redacted>"
  +       cdn: "<redacted>"
  +       fog_connection: "<redacted>"
  +       max_package_size: "<redacted>"
  +       max_valid_packages_stored: "<redacted>"
  +       webdav_config:
  +         password: "<redacted>"
  +         private_endpoint: "<redacted>"
  +         public_endpoint: "<redacted>"
  +         secret: "<redacted>"
  +         username: "<redacted>"
  +     quota_definitions:
  +       default:
  +         memory_limit: "<redacted>"
  +         non_basic_services_allowed: "<redacted>"
  +         total_routes: "<redacted>"
  +         total_services: "<redacted>"
  +     resource_pool:
  +       blobstore_type: "<redacted>"
  +       cdn: "<redacted>"
  +       fog_connection: "<redacted>"
  +       resource_directory_key: "<redacted>"
  +       webdav_config:
  +         password: "<redacted>"
  +         private_endpoint: "<redacted>"
  +         public_endpoint: "<redacted>"
  +         secret: "<redacted>"
  +         username: "<redacted>"
  +     security_group_definitions:
  +     - name: "<redacted>"
  +       rules:
  +       - destination: "<redacted>"
  +         protocol: "<redacted>"
  +       - destination: "<redacted>"
  +         protocol: "<redacted>"
  +       - destination: "<redacted>"
  +         protocol: "<redacted>"
  +       - destination: "<redacted>"
  +         protocol: "<redacted>"
  +       - destination: "<redacted>"
  +         protocol: "<redacted>"
  +     - name: "<redacted>"
  +       rules:
  +       - destination: "<redacted>"
  +         ports: "<redacted>"
  +         protocol: "<redacted>"
  +       - destination: "<redacted>"
  +         ports: "<redacted>"
  +         protocol: "<redacted>"
  +     service_usage_events:
  +       cutoff_age_in_days: "<redacted>"
  +     srv_api_uri: "<redacted>"
  +     stacks: "<redacted>"
  +     staging_upload_password: "<redacted>"
  +     staging_upload_user: "<redacted>"
  +     system_buildpacks:
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     - name: "<redacted>"
  +       package: "<redacted>"
  +     thresholds:
  +       api:
  +         alert_if_above_mb: "<redacted>"
  +         restart_if_above_mb: "<redacted>"
  +         restart_if_consistently_above_mb: "<redacted>"
  +       worker:
  +         alert_if_above_mb: "<redacted>"
  +         restart_if_above_mb: "<redacted>"
  +         restart_if_consistently_above_mb: "<redacted>"
  +     user_buildpacks: []
  +     users_can_select_backend: "<redacted>"
  +     webdav_config:
  +       password: "<redacted>"
  +       private_endpoint: "<redacted>"
  +       public_endpoint: "<redacted>"
  +       secret: "<redacted>"
  +       username: "<redacted>"
  +   ccdb:
  +     address: "<redacted>"
  +     databases:
  +     - name: "<redacted>"
  +       tag: "<redacted>"
  +     db_scheme: "<redacted>"
  +     port: "<redacted>"
  +     roles:
  +     - name: "<redacted>"
  +       password: "<redacted>"
  +       tag: "<redacted>"
  +   collector: "<redacted>"
  +   consul:
  +     agent:
  +       log_level: "<redacted>"
  +       servers:
  +         lan:
  +         - "<redacted>"
  +     agent_cert: "<redacted>"
  +     agent_key: "<redacted>"
  +     ca_cert: "<redacted>"
  +     encrypt_keys:
  +     - "<redacted>"
  +     require_ssl: "<redacted>"
  +     server_cert: "<redacted>"
  +     server_key: "<redacted>"
  +   databases:
  +     additional_config: "<redacted>"
  +     address: "<redacted>"
  +     collect_statement_statistics: "<redacted>"
  +     databases:
  +     - citext: "<redacted>"
  +       name: "<redacted>"
  +       tag: "<redacted>"
  +     - citext: "<redacted>"
  +       name: "<redacted>"
  +       tag: "<redacted>"
  +     db_scheme: "<redacted>"
  +     port: "<redacted>"
  +     roles:
  +     - name: "<redacted>"
  +       password: "<redacted>"
  +       tag: "<redacted>"
  +     - name: "<redacted>"
  +       password: "<redacted>"
  +       tag: "<redacted>"
  +   dea_next:
  +     advertise_interval_in_seconds: "<redacted>"
  +     allow_host_access: "<redacted>"
  +     allow_networks: "<redacted>"
  +     default_health_check_timeout: "<redacted>"
  +     deny_networks: "<redacted>"
  +     directory_server_protocol: "<redacted>"
  +     disk_mb: "<redacted>"
  +     disk_overcommit_factor: "<redacted>"
  +     evacuation_bail_out_time_in_seconds: "<redacted>"
  +     heartbeat_interval_in_seconds: "<redacted>"
  +     instance_bandwidth_limit: "<redacted>"
  +     instance_disk_inode_limit: "<redacted>"
  +     kernel_network_tuning_enabled: "<redacted>"
  +     logging_level: "<redacted>"
  +     memory_mb: "<redacted>"
  +     memory_overcommit_factor: "<redacted>"
  +     mtu: "<redacted>"
  +     post_setup_hook: "<redacted>"
  +     rlimit_core: "<redacted>"
  +     staging_bandwidth_limit: "<redacted>"
  +     staging_disk_inode_limit: "<redacted>"
  +     staging_disk_limit_mb: "<redacted>"
  +     staging_memory_limit_mb: "<redacted>"
  +   description: "<redacted>"
  +   disk_quota_enabled: "<redacted>"
  +   domain: "<redacted>"
  +   doppler:
  +     blacklisted_syslog_ranges: "<redacted>"
  +     debug: "<redacted>"
  +     maxRetainedLogMessages: "<redacted>"
  +     message_drain_buffer_size: "<redacted>"
  +     port: "<redacted>"
  +     tls:
  +       enable: "<redacted>"
  +       port: "<redacted>"
  +       server_cert: "<redacted>"
  +       server_key: "<redacted>"
  +     unmarshaller_count: "<redacted>"
  +     zone: "<redacted>"
  +   doppler_endpoint:
  +     shared_secret: "<redacted>"
  +   dropsonde:
  +     enabled: "<redacted>"
  +   etcd:
  +     machines:
  +     - "<redacted>"
  +     peer_require_ssl: "<redacted>"
  +     require_ssl: "<redacted>"
  +   etcd_metrics_server:
  +     nats:
  +       machines:
  +       - "<redacted>"
  +       password: "<redacted>"
  +       username: "<redacted>"
  +   ha_proxy: "<redacted>"
  +   hm9000:
  +     port: "<redacted>"
  +     url: "<redacted>"
  +   logger_endpoint:
  +     port: "<redacted>"
  +   loggregator:
  +     blacklisted_syslog_ranges: "<redacted>"
  +     debug: "<redacted>"
  +     etcd:
  +       machines:
  +       - "<redacted>"
  +     maxRetainedLogMessages: "<redacted>"
  +     outgoing_dropsonde_port: "<redacted>"
  +     tls:
  +       ca_cert: "<redacted>"
  +   loggregator_endpoint:
  +     shared_secret: "<redacted>"
  +   login:
  +     analytics:
  +       code: "<redacted>"
  +       domain: "<redacted>"
  +     asset_base_url: "<redacted>"
  +     brand: "<redacted>"
  +     catalina_opts: "<redacted>"
  +     enabled: "<redacted>"
  +     invitations_enabled: "<redacted>"
  +     links:
  +       passwd: "<redacted>"
  +       signup: "<redacted>"
  +     logout: "<redacted>"
  +     messages: "<redacted>"
  +     notifications:
  +       url: "<redacted>"
  +     protocol: "<redacted>"
  +     restricted_ips_regex: "<redacted>"
  +     saml: "<redacted>"
  +     self_service_links_enabled: "<redacted>"
  +     signups_enabled: "<redacted>"
  +     smtp:
  +       host: "<redacted>"
  +       password: "<redacted>"
  +       port: "<redacted>"
  +       user: "<redacted>"
  +     spring_profiles: "<redacted>"
  +     tiles: "<redacted>"
  +     uaa_base: "<redacted>"
  +     url: "<redacted>"
  +   metron_agent:
  +     buffer_size: "<redacted>"
  +     deployment: "<redacted>"
  +     enable_buffer: "<redacted>"
  +     preferred_protocol: "<redacted>"
  +     tls:
  +       client_cert: "<redacted>"
  +       client_key: "<redacted>"
  +   metron_endpoint:
  +     shared_secret: "<redacted>"
  +   nats:
  +     debug: "<redacted>"
  +     machines:
  +     - "<redacted>"
  +     monitor_port: "<redacted>"
  +     password: "<redacted>"
  +     port: "<redacted>"
  +     prof_port: "<redacted>"
  +     trace: "<redacted>"
  +     user: "<redacted>"
  +   nfs_server:
  +     address: "<redacted>"
  +     allow_from_entries:
  +     - "<redacted>"
  +     - "<redacted>"
  +     share: "<redacted>"
  +   request_timeout_in_seconds: "<redacted>"
  +   router:
  +     cipher_suites: "<redacted>"
  +     debug_addr: "<redacted>"
  +     drain_wait: "<redacted>"
  +     enable_routing_api: "<redacted>"
  +     enable_ssl: "<redacted>"
  +     extra_headers_to_log: "<redacted>"
  +     logrotate: "<redacted>"
  +     port: "<redacted>"
  +     requested_route_registration_interval_in_seconds: "<redacted>"
  +     route_services_recommend_https: "<redacted>"
  +     route_services_secret: "<redacted>"
  +     route_services_secret_decrypt_only: "<redacted>"
  +     route_services_timeout: "<redacted>"
  +     secure_cookies: "<redacted>"
  +     ssl_cert: "<redacted>"
  +     ssl_key: "<redacted>"
  +     ssl_skip_validation: "<redacted>"
  +     status:
  +       password: "<redacted>"
  +       port: "<redacted>"
  +       user: "<redacted>"
  +   smoke_tests: "<redacted>"
  +   ssl:
  +     skip_cert_verify: "<redacted>"
  +   support_address: "<redacted>"
  +   syslog_daemon_config: "<redacted>"
  +   system_domain: "<redacted>"
  +   system_domain_organization: "<redacted>"
  +   traffic_controller:
  +     disable_access_control: "<redacted>"
  +     outgoing_port: "<redacted>"
  +     zone: "<redacted>"
  +   uaa:
  +     admin:
  +       client_secret: "<redacted>"
  +     authentication:
  +       policy:
  +         countFailuresWithinSeconds: "<redacted>"
  +         lockoutAfterFailures: "<redacted>"
  +         lockoutPeriodSeconds: "<redacted>"
  +     catalina_opts: "<redacted>"
  +     cc:
  +       client_secret: "<redacted>"
  +     clients:
  +       cc_routing:
  +         authorities: "<redacted>"
  +         authorized-grant-types: "<redacted>"
  +         secret: "<redacted>"
  +       cf:
  +         access-token-validity: "<redacted>"
  +         authorities: "<redacted>"
  +         authorized-grant-types: "<redacted>"
  +         autoapprove: "<redacted>"
  +         override: "<redacted>"
  +         refresh-token-validity: "<redacted>"
  +         scope: "<redacted>"
  +       cloud_controller_username_lookup:
  +         authorities: "<redacted>"
  +         authorized-grant-types: "<redacted>"
  +         secret: "<redacted>"
  +       doppler:
  +         authorities: "<redacted>"
  +         override: "<redacted>"
  +         secret: "<redacted>"
  +       gorouter:
  +         authorities: "<redacted>"
  +         authorized-grant-types: "<redacted>"
  +         secret: "<redacted>"
  +       login:
  +         authorities: "<redacted>"
  +         authorized-grant-types: "<redacted>"
  +         autoapprove: "<redacted>"
  +         override: "<redacted>"
  +         redirect-uri: "<redacted>"
  +         scope: "<redacted>"
  +         secret: "<redacted>"
  +       notifications:
  +         authorities: "<redacted>"
  +         authorized-grant-types: "<redacted>"
  +         secret: "<redacted>"
  +       tcp_emitter:
  +         authorities: "<redacted>"
  +         authorized-grant-types: "<redacted>"
  +         secret: "<redacted>"
  +       tcp_router:
  +         authorities: "<redacted>"
  +         authorized-grant-types: "<redacted>"
  +         secret: "<redacted>"
  +     database: "<redacted>"
  +     issuer: "<redacted>"
  +     jwt:
  +       signing_key: "<redacted>"
  +       verification_key: "<redacted>"
  +     ldap: "<redacted>"
  +     login: "<redacted>"
  +     newrelic: "<redacted>"
  +     no_ssl: "<redacted>"
  +     port: "<redacted>"
  +     require_https: "<redacted>"
  +     restricted_ips_regex: "<redacted>"
  +     scim:
  +       external_groups: "<redacted>"
  +       groups: "<redacted>"
  +       userids_enabled: "<redacted>"
  +       users:
  +       - "<redacted>"
  +     spring_profiles: "<redacted>"
  +     ssl:
  +       port: "<redacted>"
  +     url: "<redacted>"
  +     user: "<redacted>"
  +     zones: "<redacted>"
  +   uaadb:
  +     address: "<redacted>"
  +     databases:
  +     - name: "<redacted>"
  +       tag: "<redacted>"
  +     db_scheme: "<redacted>"
  +     port: "<redacted>"
  +     roles:
  +     - name: "<redacted>"
  +       password: "<redacted>"
  +       tag: "<redacted>"

  Continue? [yN]: y

  Task 9

  Task 9 | 01:32:44 | Deprecation: Ignoring cloud config. Manifest contains 'networks' section.
  Task 9 | 01:32:44 | Preparing deployment: Preparing deployment (00:00:01)
  Task 9 | 01:32:48 | Preparing package compilation: Finding packages to compile (00:00:00)
  Task 9 | 01:32:48 | Creating missing vms: consul_z1/7fa46c6a-5c53-4c58-8178-74a6013b421b (0)
  Task 9 | 01:32:48 | Creating missing vms: api_z1/0cad15a6-c0e9-462b-bb12-92aaebae058c (0)
  Task 9 | 01:32:48 | Creating missing vms: nats_z1/9896cc89-51ff-4ce1-a83f-eae21787754b (0)
  Task 9 | 01:32:48 | Creating missing vms: stats_z1/34abbb8c-791e-4e7e-aacd-a5298358bebe (0)
  Task 9 | 01:32:48 | Creating missing vms: ha_proxy_z1/3ca70a7e-1963-4555-b1f0-4c6236c38a49 (0)
  Task 9 | 01:32:48 | Creating missing vms: runner_z1/69845d82-6174-4a73-a7b5-56809d964618 (0)
  Task 9 | 01:32:48 | Creating missing vms: uaa_z1/ec113438-ec21-4530-ac5e-c1a6f0986c94 (0)
  Task 9 | 01:32:48 | Creating missing vms: router_z1/a75fef70-252b-4597-b82f-c0198fd6a32d (0)
  Task 9 | 01:32:48 | Creating missing vms: nfs_z1/383fb134-0981-4e7c-896c-2deb4fef8d71 (0)
  Task 9 | 01:32:48 | Creating missing vms: loggregator_trafficcontroller_z1/42a4199f-17d4-4862-9e42-b8ec516b4065 (0)
  Task 9 | 01:32:48 | Creating missing vms: postgres_z1/b476716f-80d4-4ff4-83d9-7b35bd7eb7df (0)
  Task 9 | 01:32:48 | Creating missing vms: doppler_z1/c6e5155e-d93d-4603-b91a-c645b25c8ff3 (0)
  Task 9 | 01:32:48 | Creating missing vms: etcd_z1/6bea84ba-bcbd-4b1a-b90e-0390106683b3 (0)
  Task 9 | 01:32:48 | Creating missing vms: hm9000_z1/8cdbdd3b-0d70-43d2-914c-c249b279ae9e (0)
  Task 9 | 01:34:48 | Creating missing vms: ha_proxy_z1/3ca70a7e-1963-4555-b1f0-4c6236c38a49 (0) (00:02:00)
  Task 9 | 01:34:48 | Creating missing vms: nfs_z1/383fb134-0981-4e7c-896c-2deb4fef8d71 (0) (00:02:00)
  Task 9 | 01:34:48 | Creating missing vms: stats_z1/34abbb8c-791e-4e7e-aacd-a5298358bebe (0) (00:02:00)
  Task 9 | 01:34:49 | Creating missing vms: uaa_z1/ec113438-ec21-4530-ac5e-c1a6f0986c94 (0) (00:02:01)
  Task 9 | 01:34:49 | Creating missing vms: nats_z1/9896cc89-51ff-4ce1-a83f-eae21787754b (0) (00:02:01)
  Task 9 | 01:34:51 | Creating missing vms: doppler_z1/c6e5155e-d93d-4603-b91a-c645b25c8ff3 (0) (00:02:03)
  Task 9 | 01:34:54 | Creating missing vms: api_z1/0cad15a6-c0e9-462b-bb12-92aaebae058c (0) (00:02:06)
  Task 9 | 01:34:56 | Creating missing vms: runner_z1/69845d82-6174-4a73-a7b5-56809d964618 (0) (00:02:08)
  Task 9 | 01:34:56 | Creating missing vms: loggregator_trafficcontroller_z1/42a4199f-17d4-4862-9e42-b8ec516b4065 (0) (00:02:08)
  Task 9 | 01:34:56 | Creating missing vms: consul_z1/7fa46c6a-5c53-4c58-8178-74a6013b421b (0) (00:02:08)
  Task 9 | 01:34:56 | Creating missing vms: etcd_z1/6bea84ba-bcbd-4b1a-b90e-0390106683b3 (0) (00:02:08)
  Task 9 | 01:34:57 | Creating missing vms: router_z1/a75fef70-252b-4597-b82f-c0198fd6a32d (0) (00:02:09)
  Task 9 | 01:34:58 | Creating missing vms: hm9000_z1/8cdbdd3b-0d70-43d2-914c-c249b279ae9e (0) (00:02:10)
  Task 9 | 01:34:58 | Creating missing vms: postgres_z1/b476716f-80d4-4ff4-83d9-7b35bd7eb7df (0) (00:02:10)
  Task 9 | 01:34:59 | Updating instance consul_z1: consul_z1/7fa46c6a-5c53-4c58-8178-74a6013b421b (0) (canary) (00:01:22)
  Task 9 | 01:36:21 | Updating instance ha_proxy_z1: ha_proxy_z1/3ca70a7e-1963-4555-b1f0-4c6236c38a49 (0) (canary) (00:01:05)
  Task 9 | 01:37:26 | Updating instance nats_z1: nats_z1/9896cc89-51ff-4ce1-a83f-eae21787754b (0) (canary) (00:00:50)
  Task 9 | 01:38:16 | Updating instance etcd_z1: etcd_z1/6bea84ba-bcbd-4b1a-b90e-0390106683b3 (0) (canary) (00:01:28)
  Task 9 | 01:39:44 | Updating instance stats_z1: stats_z1/34abbb8c-791e-4e7e-aacd-a5298358bebe (0) (canary) (00:00:51)
  Task 9 | 01:40:35 | Updating instance nfs_z1: nfs_z1/383fb134-0981-4e7c-896c-2deb4fef8d71 (0) (canary) (00:01:46)
  Task 9 | 01:42:21 | Updating instance postgres_z1: postgres_z1/b476716f-80d4-4ff4-83d9-7b35bd7eb7df (0) (canary) (00:01:38)
  Task 9 | 01:43:59 | Updating instance uaa_z1: uaa_z1/ec113438-ec21-4530-ac5e-c1a6f0986c94 (0) (canary) (00:00:57)
  Task 9 | 01:44:56 | Updating instance api_z1: api_z1/0cad15a6-c0e9-462b-bb12-92aaebae058c (0) (canary) (00:02:33)
  Task 9 | 01:47:29 | Updating instance hm9000_z1: hm9000_z1/8cdbdd3b-0d70-43d2-914c-c249b279ae9e (0) (canary) (00:00:50)
  Task 9 | 01:48:19 | Updating instance runner_z1: runner_z1/69845d82-6174-4a73-a7b5-56809d964618 (0) (canary) (00:01:08)
  Task 9 | 01:49:27 | Updating instance doppler_z1: doppler_z1/c6e5155e-d93d-4603-b91a-c645b25c8ff3 (0) (canary) (00:00:46)
  Task 9 | 01:50:13 | Updating instance loggregator_trafficcontroller_z1: loggregator_trafficcontroller_z1/42a4199f-17d4-4862-9e42-b8ec516b4065 (0) (canary) (00:00:47)
  Task 9 | 01:51:01 | Updating instance router_z1: router_z1/a75fef70-252b-4597-b82f-c0198fd6a32d (0) (canary) (00:00:49)

  Task 9 Started  Tue May 15 01:32:44 UTC 2018
  Task 9 Finished Tue May 15 01:51:50 UTC 2018
  Task 9 Duration 00:19:06
  Task 9 done

  Succeeded

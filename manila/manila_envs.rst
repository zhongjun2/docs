
问题： 运行openstack命令的时候报错，提示缺少环境变量信息
::

  # manila list
  ERROR: You must provide a tenant_name, tenant_id, project_id or project_name (with project_domain_name or project_domain_id) via --os-tenant-name or env[OS_TENANT_NAME], --os-tenant-id or env[OS_TENANT_ID], --os-project-id or env[OS_PROJECT_ID], --os-project-name or env[OS_PROJECT_NAME], --os-project-domain-id or env[OS_PROJECT_DOMAIN_ID] and --os-project-domain-name or env[OS_PROJECT_DOMAIN_NAME].


解决方法：设置如下环境变量信息
::

  export OS_USERNAME=admin
  export OS_PASSWORD=nomoresecret
  export OS_TENANT_NAME=admin
  export OS_AUTH_URL="http://127.0.0.1/identity"
  export OS_IDENTITY_API_VERSION=3
  export OS_USER_DOMAIN_NAME=Default
  export OS_PROJECT_DOMAIN_NAME=Default

保存环境变量

* 方法1：想要设置成全局的可以保存在 ~/.bashrc中

* 方法2：也可以新建文档进行保存，比如新建manila_envs文档 
::

  # vi /root/manila_evns
  export OS_USERNAME=admin
  export OS_PASSWORD=nomoresecret
  export OS_TENANT_NAME=admin
  export OS_AUTH_URL="http://127.0.0.1/identity"
  export OS_IDENTITY_API_VERSION=3
  export OS_USER_DOMAIN_NAME=Default
  export OS_PROJECT_DOMAIN_NAME=Default

执行如下命令使环境变量生效
::

  # source /root/manila_evns

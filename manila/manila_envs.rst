
运行openstack命令的时候报错，提示缺少环境变量信息
::

  # manila list
  ERROR: You must provide a tenant_name, tenant_id, project_id or project_name (with project_domain_name or project_domain_id) via --os-tenant-name or env[OS_TENANT_NAME], --os-tenant-id or env[OS_TENANT_ID], --os-project-id or env[OS_PROJECT_ID], --os-project-name or env[OS_PROJECT_NAME], --os-project-domain-id or env[OS_PROJECT_DOMAIN_ID] and --os-project-domain-name or env[OS_PROJECT_DOMAIN_NAME].


设置如下环境变量信息
::

  export OS_USERNAME=admin
  export OS_PASSWORD=nomoresecret
  export OS_TENANT_NAME=admin
  export OS_AUTH_URL="http://127.0.0.1/identity"
  export OS_IDENTITY_API_VERSION=3
  export OS_USER_DOMAIN_NAME=Default
  export OS_PROJECT_DOMAIN_NAME=Default

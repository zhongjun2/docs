
如何修改manila db字段并调试
=========================

1.参考如下review代码例子修改manila/db相关代码新增db表或者table列等
https://review.openstack.org/#/c/457545/

2.替换到已修改代码后升级db到最新版本
::

  # manila-manage db sync
  2018-05-09 09:58:42.801 DEBUG manila.utils [-] backend <module 'manila.db.migrations.alembic.migration' from '/opt/stack/manila/manila/db/migrations/alembic/migration.py'> from (pid=103630) __get_backend /opt/stack/manila/manila/utils.py:245
  2018-05-09 09:58:42.828 DEBUG oslo_db.sqlalchemy.engines [-] MySQL server mode set to STRICT_TRANS_TABLES,STRICT_ALL_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,TRADITIONAL,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION from (pid=103630) _check_effective_sql_mode /usr/local/lib/python2.7/dist-packages/oslo_db/sqlalchemy/engines.py:308
  2018-05-09 09:58:42.831 INFO alembic.runtime.migration [-] Context impl MySQLImpl.
  2018-05-09 09:58:42.831 INFO alembic.runtime.migration [-] Will assume non-transactional DDL.
  2018-05-09 09:58:42.898 INFO alembic.runtime.migration [-] Running upgrade 4a482571410f -> 3650e2s75c45, add priority column for access
  2018-05-09 09:58:42.954 DEBUG alembic.runtime.migration [-] update 4a482571410f to 3650e2s75c45 from (pid=103630) update_to_step /usr/local/lib/python2.7/dist-packages/alembic/runtime/migration.py:539

回显中显示db已经从4a482571410f 版本升级到 3650e2s75c45  版本

3.（option）option）如果升级失败可以直接回退到原始版本
::

  # manila-manage db downgrade 4a482571410f

4.(Option)如果代码写的不好，数据表搞坏了，可以登录mysql直接删掉manila表格，重新创建，再同步到稳定的版本的db表
::

  # mysql -u root -p
  Enter password:
  Welcome to the MySQL monitor.  Commands end with ; or \g.
  Your MySQL connection id is 12101
  Server version: 5.7.21-0ubuntu0.16.04.1 (Ubuntu)

  Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.

  Oracle is a registered trademark of Oracle Corporation and/or its
  affiliates. Other names may be trademarks of their respective
  owners.

  Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

  mysql>drop database manila;
  mysql>create database manila;

* mysql 的密码默认为 stackdb，在devstack中的local.conf文件中配置

重新执行同步命令同步db到最新的稳定版本
::

# manila-manage db sync

5.完成db表升级后就可以 `重启manila服务 <https://github.com/zhongjun2/docs/blob/master/manila/manila_debug.rst>`_ 进行功能测试了


6.跑db测试用例，需要登录mysql后运行如下命令，创建跑db用例时的环境配置
To run database migration tests:
::

  $ mysql -u %username% -p %password%

  CREATE DATABASE openstack_citest;
  CREATE USER 'openstack_citest'@'localhost' IDENTIFIED BY 'openstack_citest';
  CREATE USER 'openstack_citest' IDENTIFIED BY 'openstack_citest';
  GRANT ALL PRIVILEGES ON *.* TO 'openstack_citest'@'localhost';
  GRANT ALL PRIVILEGES ON *.* TO 'openstack_citest';
  FLUSH PRIVILEGES;

使用tox命令调试运行db test相关用例
::

  $ tox -e debug -- manila.tests.db.migrations.alembic.test_migration


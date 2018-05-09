
如何修改manila db字段并调试
=========================

1.按照如下review代码实例修改代码

2.替换到已修改代码后升级db到最新版本
  可以从下面命令的回显看到db已经从4a482571410f 版本升级到 3650e2s75c45  版本
::

  # manila-manage db sync
  2018-05-09 09:58:42.801 DEBUG manila.utils [-] backend <module 'manila.db.migrations.alembic.migration' from '/opt/stack/manila/manila/db/migrations/alembic/migration.py'> from (pid=103630) __get_backend /opt/stack/manila/manila/utils.py:245
  2018-05-09 09:58:42.828 DEBUG oslo_db.sqlalchemy.engines [-] MySQL server mode set to STRICT_TRANS_TABLES,STRICT_ALL_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,TRADITIONAL,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION from (pid=103630) _check_effective_sql_mode /usr/local/lib/python2.7/dist-packages/oslo_db/sqlalchemy/engines.py:308
  2018-05-09 09:58:42.831 INFO alembic.runtime.migration [-] Context impl MySQLImpl.
  2018-05-09 09:58:42.831 INFO alembic.runtime.migration [-] Will assume non-transactional DDL.
  2018-05-09 09:58:42.898 INFO alembic.runtime.migration [-] Running upgrade 4a482571410f -> 3650e2s75c45, add priority column for access
  2018-05-09 09:58:42.954 DEBUG alembic.runtime.migration [-] update 4a482571410f to 3650e2s75c45 from (pid=103630) update_to_step /usr/local/lib/python2.7/dist-packages/alembic/runtime/migration.py:539


3.如果升级失败可以直接回退到原始版本
::

  # manila-manage db downgrade 4a482571410f

4.如果代码写的不好，数据表搞坏了，可以直接删掉manila表格，重新创建，再同步到稳定的版本的db表
::

  drop database manila;
  create database manila;
  manila-manage db sync；

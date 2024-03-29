# RDS for MySQL不支持MyISAM引擎表，迁移时MyISAM如何处理<a name="drs_04_0032"></a>

基于以下原因，RDS for MySQL目前不支持MyISAM引擎。

-   MyISAM引擎表不支持事务，仅支持表级别锁，导致读写操作相互冲突。
-   MyISAM对数据完整性的保护存在缺陷，且这些缺陷会导致数据库数据的损坏甚至丢失。
-   MyISAM在出现数据损害情况下，很多都需要手动修复，无法通过产品服务提供的恢复功能进行数据恢复。
-   MyISAM向InnoDB的迁移透明，大多数情况不需要改动建表的代码，云数据库自动转换InnoDB即可完成迁移。

DRS在迁移过程中，会自动将MyISAM转换为InnoDB。针对MyISAM引擎表不支持事务这一特点，为了确保MyISAM表的数据一致性， DRS会借助主键来实现最终数据的一致。如果需要迁移没有主键的MyISAM表，建议选择无业务期启动迁移任务，以确保数据的一致性。


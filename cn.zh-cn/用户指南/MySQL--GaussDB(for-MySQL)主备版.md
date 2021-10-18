# MySQL-\>GaussDB\(for MySQL\)主备版<a name="drs_04_0090"></a>

## 使用技巧（需要人为配合）<a name="section182303625619"></a>

-   如果您使用的是全量迁移模式（离线迁移），确保源和目标数据库无业务写入，保证迁移前后数据一致。

-   如果您使用的是全量+增量迁移模式（在线迁移），支持在源数据库有业务数据写入的情况下进行迁移，推荐**提前2-3天**启动任务，并配合如下使用技巧和对应场景的[操作要求](#section83714237916)，以确保顺利迁移。
    -   全量迁移

        基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行迁移任务，相对静态的数据，迁移时复杂度将会降低。如果迁移不可避免业务高峰期，推荐使用迁移限速功能，即“流速模式“选择“限速“。

        -   全量迁移会对源数据库有一定的访问压力。
        -   迁移无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
        -   正在迁移的数据被其他事务长时间锁死，可能导致读数据超时。
        -   由于MySQL固有特点限制，CPU资源紧张时，存储引擎为Tokudb的表，读取速度可能下降至10%。

    -   数据对比

        建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。


-   支持源库为GaussDB\(for MySQL\)实例，GaussDB\(for MySQL\)到GaussDB\(for MySQL\)可以使用此链路进行实时迁移。

## 操作要求<a name="section83714237916"></a>

针对一些无法预知或人为因素及环境突变导致迁移失败的情况，数据复制服务提供以下常见的操作限制，供您在迁移过程中参考。

**表 1**  操作要求

<a name="table10267016117"></a>
<table><thead align="left"><tr id="row17267020115"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p92620081116"><a name="p92620081116"></a><a name="p92620081116"></a><strong id="b9264011110"><a name="b9264011110"></a><a name="b9264011110"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p162620012115"><a name="p162620012115"></a><a name="p162620012115"></a><strong id="b226170141115"><a name="b226170141115"></a><a name="b226170141115"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row32610014111"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p16261508118"><a name="p16261508118"></a><a name="p16261508118"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul626803115"></a><a name="ul626803115"></a><ul id="ul626803115"><li><a href="#table1291601510111">表2</a>中的环境要求均不允许在迁移过程中修改，直至迁移结束。</li><li>支持数据库、表、视图、索引、约束、函数、存储过程、触发器（TRIGGER）和事件（EVENT）的迁移。</li><li>不支持系统库的迁移以及事件状态的迁移。</li><li>不支持迁移加密表。</li><li>不支持非MyISAM和非InnoDB表的迁移。</li><li>不支持外键级联操作。</li><li>源库为RDS for MySQL实例时，不支持带有TDE特性并建立具有加密功能表。</li></ul>
</td>
</tr>
<tr id="row15270091114"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p527406113"><a name="p527406113"></a><a name="p527406113"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul19274015119"></a><a name="ul19274015119"></a><ul id="ul19274015119"><li>在结束迁移任务时，将进行所选事件（EVENT）和触发器（TRIGGER）的迁移，请在结束任务时关注迁移日志上报的状态，确保数据库完整性。</li><li>迁移过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>迁移任务目标数据库可以设置“只读”和“读写”。<a name="ul188501347195919"></a><a name="ul188501347195919"></a><ul id="ul188501347195919"><li>只读：目标数据库实例将转化为只读、不可写入的状态，迁移任务结束后恢复可读写状态，此选项可有效的确保数据迁移的完整性和成功率，推荐此选项。</li><li>读写：目标数据库可以读写，但需要避免操作或接入应用后会更改迁移中的数据（注意：无业务的程序常常也有微量的数据操作），进而形成数据冲突、任务故障、且无法修复续传，充分了解要点后可选择此选项。</li></ul>
</li><li>在任务启动、任务全量迁移阶段，不建议对源数据库做删除类型的DDL操作，比如删除数据库、索引、视图等，这样可能会引起任务迁移失败。</li><li>增量迁移场景下，不支持源数据库进行恢复到某个备份点的操作（PITR）。</li><li>增量迁移过程中，若源库存在分布式事务，可能会导致迁移失败。</li><li>为了保持数据一致性，不允许对正在迁移中的目标数据库进行修改操作(包括但不限于DDL、DML操作)。</li><li>增量迁移阶段，支持断点续传功能，在主机系统崩溃的情况下，对于非事务性的无主键的表可能会出现重复插入数据的情况。</li><li>在迁移任务结束之前，不允许源数据库提前中断公网连接。</li><li>迁移过程中，不允许源库写入binlog格式为statement的数据。</li><li>迁移过程中，不允许源库执行清除binlog的操作。</li><li>为了避免正在迁移的数据被其他事务锁死，导致读数据超时，建议在业务低峰期进行数据迁移。</li><li>迁移过程中，<span id="text1980165413315"><a name="text1980165413315"></a><a name="text1980165413315"></a>GaussDB(for MySQL)</span>会将MyISAM表自动转换成InnoDB，转化失败则迁移失败。</li><li>选择表级对象迁移时，增量迁移过程中不建议对表进行重命名操作。</li><li>建议将expire_log_day参数设置在合理的范围，确保恢复时断点处的binlog尚未过期，以保证服务中断后的顺利恢复。</li><li>如果源数据库为自建库，并且安装了Percona Server for MySQL 5.6.x或Percona Server for MySQL 5.7.x时，内存管理器必须使用Jemalloc库，以避免因系统表频繁查询带来的内存回收不及时，并最终导致数据库Out of Memory问题。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section1645253517920"></a>

在使用数据复制服务进行实时迁移的过程中，对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table1291601510111"></a>
<table><thead align="left"><tr id="row1691661551120"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p99168157118"><a name="p99168157118"></a><a name="p99168157118"></a><strong id="b13916151511117"><a name="b13916151511117"></a><a name="b13916151511117"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p3916715121114"><a name="p3916715121114"></a><a name="p3916715121114"></a><strong id="b691661521115"><a name="b691661521115"></a><a name="b691661521115"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row16916815121117"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p16916111517112"><a name="p16916111517112"></a><a name="p16916111517112"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1591691501119"></a><a name="ul1591691501119"></a><ul id="ul1591691501119"><li><strong id="b1891715152113"><a name="b1891715152113"></a><a name="b1891715152113"></a>全量迁移最小权限要求：</strong><a name="ul1991751519111"></a><a name="ul1991751519111"></a><ul id="ul1991751519111"><li>源数据库帐户需要具备如下权限：SELECT、SHOW VIEW、EVENT。</li><li>目标数据库帐号必须拥有如下权限：SELECT、CREATE、DROP、DELETE、INSERT、UPDATE、INDEX、EVENT、CREATE VIEW、CREATE ROUTINE、TRIGGER、WITH GRANT OPTION。</li></ul>
</li><li><strong id="b891719158111"><a name="b891719158111"></a><a name="b891719158111"></a>全量+增量迁移最小权限要求：</strong><a name="ul11917615121115"></a><a name="ul11917615121115"></a><ul id="ul11917615121115"><li>源数据库帐户需要具备如下权限：SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</li><li>目标数据库帐号必须拥有如下权限：SELECT、CREATE、DROP、DELETE、INSERT、UPDATE、INDEX、EVENT、CREATE VIEW、CREATE ROUTINE、TRIGGER、WITH GRANT OPTION。</li></ul>
</li></ul>
</td>
</tr>
<tr id="row13917181581110"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p191711514117"><a name="p191711514117"></a><a name="p191711514117"></a>迁移对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul2917151531119"></a><a name="ul2917151531119"></a><ul id="ul2917151531119"><li>支持数据库、表、视图、索引、约束、函数、存储过程、触发器（TRIGGER）和事件（EVENT）的迁移。</li><li>不支持系统库的迁移以及事件状态的迁移。</li><li>不支持迁移加密表。</li><li>不支持非MyISAM和非InnoDB表的迁移。</li></ul>
</td>
</tr>
<tr id="row7918111541116"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p209181315151120"><a name="p209181315151120"></a><a name="p209181315151120"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul149181215151114"></a><a name="ul149181215151114"></a><ul id="ul149181215151114"><li>源数据库中的库名、表名、视图名不能包含：'&lt;&gt;/\以及非ASCII字符。</li><li>MySQL源数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议源数据库binlog保存时间越长越好，建议为3天。</li><li>源数据库expire_logs_days参数值为0，可能会导致迁移失败。</li><li>增量迁移时，必须设置MySQL源数据库的server_id。如果源数据库版本小于或等于MySQL5.6，server_id的取值范围在2－4294967296之间；如果源数据库版本大于或等于MySQL5.7，server_id的取值范围在1－4294967296之间。</li><li>MySQL源数据库建议开启skip-name-resolve，减少连接超时的可能性。</li><li>源数据库GTID状态建议为开启状态。</li><li>源数据库不能包含有空库。</li></ul>
</td>
</tr>
<tr id="row4918915111120"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1991861571111"><a name="p1991861571111"></a><a name="p1991861571111"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul691815151114"></a><a name="ul691815151114"></a><ul id="ul691815151114"><li>建议MySQL目标库的binlog日志格式为Row格式，否则增量迁移可能出错。</li><li>目标数据库实例的运行状态必须正常。</li><li>除了MySQL系统数据库之外，目标数据库不能包含与源数据库同名的数据库。</li><li>建议目标库的事务隔离级别至少保证在已提交读。</li></ul>
</td>
</tr>
</tbody>
</table>


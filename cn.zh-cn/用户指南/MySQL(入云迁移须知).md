# MySQL-\>MySQL<a name="drs_04_0088"></a>

## 使用技巧（需要人为配合）<a name="section182303625619"></a>

-   如果您使用的是全量迁移模式（离线迁移），确保源和目标数据库无业务写入，保证迁移前后数据一致。

-   如果您使用的是全量+增量迁移模式（在线迁移），支持在源数据库有业务数据写入的情况下进行迁移，推荐**提前2-3天**启动任务，并配合如下使用技巧和对应场景的[操作要求](#section8705182416394)，以确保顺利迁移。
    -   全量迁移

        基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行迁移任务，相对静态的数据，迁移时复杂度将会降低。如果迁移不可避免业务高峰期，推荐使用迁移限速功能，即“流速模式“选择“限速“。

        -   全量迁移会对源数据库有一定的访问压力。
        -   迁移无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
        -   正在迁移的数据被其他事务长时间锁死，可能导致读数据超时。
        -   由于MySQL固有特点限制，CPU资源紧张时，存储引擎为Tokudb的表，读取速度可能下降至10%。

    -   数据对比

        建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。



## 操作要求<a name="section8705182416394"></a>

针对一些无法预知或人为因素及环境突变导致迁移失败的情况，数据复制服务提供以下常见的操作限制，供您在迁移过程中参考。

**表 1**  操作要求

<a name="table8635652153911"></a>
<table><thead align="left"><tr id="row463525233913"><th class="cellrowborder" valign="top" width="18.39%" id="mcps1.2.3.1.1"><p id="p1863575215396"><a name="p1863575215396"></a><a name="p1863575215396"></a><strong id="b1863585243911"><a name="b1863585243911"></a><a name="b1863585243911"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.61%" id="mcps1.2.3.1.2"><p id="p1563519525399"><a name="p1563519525399"></a><a name="p1563519525399"></a><strong id="b1563585217392"><a name="b1563585217392"></a><a name="b1563585217392"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row1563515526392"><td class="cellrowborder" valign="top" width="18.39%" headers="mcps1.2.3.1.1 "><p id="p8635155212398"><a name="p8635155212398"></a><a name="p8635155212398"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.61%" headers="mcps1.2.3.1.2 "><a name="ul16351152203920"></a><a name="ul16351152203920"></a><ul id="ul16351152203920"><li><a href="#table1151143114403">表2</a>中的环境要求均不允许在迁移过程中修改，直至迁移结束。</li><li>相互关联的数据对象要确保同时迁移，避免迁移因关联对象缺失，导致迁移失败。常见的关联关系：视图引用表、视图引用视图、存储过程/函数/触发器引用视图/表、主外键关联表等。</li><li>不支持外键级联操作。</li><li>由于MySQL本身限制，若源库的一次性事件（EVENT）设定的触发时间在迁移开始前，该事件（EVENT）不会迁移到目标库。</li><li>多对一场景下，创建迁移任务时，目标库读写设置需要跟已有任务设置为一致。</li><li>增量迁移会过滤创建用户、删除用户及修改用户权限的DDL操作。</li><li>由于无主键表缺乏行的唯一性标志，网络不稳定时涉及少量重试，表数据存在少量不一致的可能性。</li><li>不支持目标数据库恢复到全量迁移时间段范围内的PITR操作。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建迁移任务。</li><li>源库和目标库为RDS for MySQL实例时，不支持带有TDE特性并建立具有加密功能表。</li></ul>
</td>
</tr>
<tr id="row063615524393"><td class="cellrowborder" valign="top" width="18.39%" headers="mcps1.2.3.1.1 "><p id="p17636452203910"><a name="p17636452203910"></a><a name="p17636452203910"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.61%" headers="mcps1.2.3.1.2 "><a name="ul186361526392"></a><a name="ul186361526392"></a><ul id="ul186361526392"><li>在任务启动、任务全量迁移阶段，不建议对源数据库做删除类型的DDL操作，比如删除数据库、索引、视图等，这样可能会引起任务迁移失败。</li><li>在结束迁移任务时，将进行所选事件（EVENT）和触发器（TRIGGER）的迁移。请确保任务结束前，不要断开源和目标数据库的网络连通性，并在结束任务时关注迁移日志上报的状态，达到数据库完整迁移效果。</li><li>迁移过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>迁移任务目标数据库可以设置“只读”和“读写”。<a name="ul188501347195919"></a><a name="ul188501347195919"></a><ul id="ul188501347195919"><li>只读：目标数据库实例将转化为只读、不可写入的状态，迁移任务结束后恢复可读写状态，此选项可有效的确保数据迁移的完整性和成功率，推荐此选项。</li><li>读写：目标数据库可以读写，但需要避免操作或接入应用后会更改迁移中的数据（注意：无业务的程序常常也有微量的数据操作），进而形成数据冲突、任务故障、且无法修复续传，充分了解要点后可选择此选项。</li></ul>
</li><li>增量迁移场景下，不支持源数据库进行恢复到某个备份点的操作（PITR）。</li><li>为了保持数据一致性，不允许对正在迁移中的目标数据库进行修改操作(包括但不限于DDL、DML操作)。</li><li>增量迁移阶段，支持断点续传功能，在主机系统崩溃的情况下，对于非事务性的无主键的表可能会出现重复插入数据的情况。</li><li>迁移过程中，不允许源库写入binlog格式为statement的数据。</li><li>迁移过程中，不允许源库执行清除binlog的操作。</li><li>选择表级对象迁移时，增量迁移过程中不支持对表进行重命名操作。</li><li>源库不支持阿里云RDS的只读副本。</li><li>如果源数据库为自建库，并且安装了Percona Server for MySQL 5.6.x或Percona Server for MySQL 5.7.x时，内存管理器必须使用Jemalloc库，以避免因系统表频繁查询带来的内存回收不及时，并最终导致数据库Out of Memory问题。</li><li>迁移过程中，不允许在源库创建库名为ib_logfile的数据库。</li><li>建议将expire_log_day参数设置在合理的范围，确保恢复时断点处的binlog尚未过期，以保证服务中断后的顺利恢复。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section2037814611407"></a>

实时迁移对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table1151143114403"></a>
<table><thead align="left"><tr id="row45193154018"><th class="cellrowborder" valign="top" width="18.37%" id="mcps1.2.3.1.1"><p id="p951163111404"><a name="p951163111404"></a><a name="p951163111404"></a><strong id="b151113144010"><a name="b151113144010"></a><a name="b151113144010"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.63%" id="mcps1.2.3.1.2"><p id="p3511431194012"><a name="p3511431194012"></a><a name="p3511431194012"></a><strong id="b2517315404"><a name="b2517315404"></a><a name="b2517315404"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row85103117403"><td class="cellrowborder" valign="top" width="18.37%" headers="mcps1.2.3.1.1 "><p id="p115110311402"><a name="p115110311402"></a><a name="p115110311402"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.63%" headers="mcps1.2.3.1.2 "><a name="ul1351143154019"></a><a name="ul1351143154019"></a><ul id="ul1351143154019"><li><strong id="b175123119406"><a name="b175123119406"></a><a name="b175123119406"></a>全量迁移最小权限要求：</strong><a name="ul6511131114018"></a><a name="ul6511131114018"></a><ul id="ul6511131114018"><li>源数据库帐户需要具备如下权限：<p id="p181171882593"><a name="p181171882593"></a><a name="p181171882593"></a>SELECT、SHOW VIEW、EVENT。</p>
</li><li>目标数据库帐号必须拥有如下权限：<p id="p2051621235910"><a name="p2051621235910"></a><a name="p2051621235910"></a>SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、INDEX、EVENT、CREATE VIEW、CREATE ROUTINE、TRIGGER、WITH GRANT OPTION。</p>
</li></ul>
</li><li><strong id="b251931194020"><a name="b251931194020"></a><a name="b251931194020"></a>全量+增量最小迁移权限要求：</strong><a name="ul155183164017"></a><a name="ul155183164017"></a><ul id="ul155183164017"><li>源数据库帐户需要具备如下权限：<p id="p6430191705917"><a name="p6430191705917"></a><a name="p6430191705917"></a>SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</p>
</li><li>目标数据库帐号必须拥有如下权限：<p id="p3454221165913"><a name="p3454221165913"></a><a name="p3454221165913"></a>SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、INDEX、EVENT、CREATE VIEW、CREATE ROUTINE、TRIGGER、WITH GRANT OPTION。</p>
</li></ul>
</li><li><strong id="b115253154011"><a name="b115253154011"></a><a name="b115253154011"></a>用户迁移最小权限要求：</strong><a name="ul15521031124010"></a><a name="ul15521031124010"></a><ul id="ul15521031124010"><li>用户迁移时，当源数据库为非阿里云数据库时，帐户需要有mysql.user的SELECT权限，源数据库为阿里云数据库，则帐户需要同时具有mysql.user和mysql.user_view的SELECT权限。</li><li>目标数据库帐户需要有mysql库的SELECT，INSERT，UPDATE，DELETE权限。</li></ul>
</li></ul>
</td>
</tr>
<tr id="row15263104014"><td class="cellrowborder" valign="top" width="18.37%" headers="mcps1.2.3.1.1 "><p id="p145217313405"><a name="p145217313405"></a><a name="p145217313405"></a>迁移对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.63%" headers="mcps1.2.3.1.2 "><a name="ul1352531134013"></a><a name="ul1352531134013"></a><ul id="ul1352531134013"><li>支持数据库、表、视图、索引、约束、函数、存储过程、触发器（TRIGGER）和事件（EVENT）的迁移。</li><li>不支持系统库的迁移以及事件状态的迁移。</li><li>不支持非MyISAM和非InnoDB表的迁移。</li></ul>
</td>
</tr>
<tr id="row165293174018"><td class="cellrowborder" valign="top" width="18.37%" headers="mcps1.2.3.1.1 "><p id="p115213319405"><a name="p115213319405"></a><a name="p115213319405"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.63%" headers="mcps1.2.3.1.2 "><a name="ul6525316404"></a><a name="ul6525316404"></a><ul id="ul6525316404"><li>源数据库中的库名不能包含：'&lt;`&gt;/\"以及非ASCII字符。</li><li>源数据库中的表名、视图名不能包含：'&lt;&gt;/\"以及非ASCII字符。</li><li>源数据库中的库名不允许为ib_logfile。</li><li>MySQL源数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议源数据库binlog保存时间越长越好，建议为3天。</li><li>源数据库expire_logs_days参数值为0，可能会导致迁移失败。</li><li>增量迁移时，必须设置MySQL源数据库的server_id。如果源数据库版本小于或等于MySQL5.6，server_id的取值范围在2－4294967296之间；如果源数据库版本大于或等于MySQL5.7，server_id的取值范围在1－4294967296之间。</li><li>MySQL源数据库建议开启skip-name-resolve，减少连接超时的可能性。</li><li>源数据库GTID状态建议为开启状态。</li><li>源库不支持mysql binlog dump命令。</li><li>源数据库和目标数据库字符集需保持一致，否则迁移失败。</li><li>源数据库log_slave_updates参数需设置为开启状态，否则会导致迁移失败。</li><li>源数据库的binlog_row_image参数需设置为FULL，否则会导致迁移失败。</li><li>源数据库MySQL8.0目前不支持参数lower_case_table_names等于0的迁移。</li></ul>
</td>
</tr>
<tr id="row1053113154013"><td class="cellrowborder" valign="top" width="18.37%" headers="mcps1.2.3.1.1 "><p id="p11531931144014"><a name="p11531931144014"></a><a name="p11531931144014"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.63%" headers="mcps1.2.3.1.2 "><a name="ul155318314406"></a><a name="ul155318314406"></a><ul id="ul155318314406"><li>不支持从高版本迁移到低版本。</li><li>建议MySQL目标库的binlog日志格式为Row格式，否则增量迁移可能出错。</li><li>目标数据库实例的运行状态必须正常。</li><li>目标数据库实例必须有足够的磁盘空间。</li><li>除了MySQL系统数据库之外，目标数据库不能包含与源数据库同名的数据库。</li><li>建议目标库的事务隔离级别至少保证在已提交读。</li><li>DRS迁移时会有大量数据写入目标库，目标库max_allowed_packet 参数过小会导致无法写入，建议将目标库max_allowed_packet参数值设置大一点，使其大于100MB。</li><li>目标数据库GTID状态建议为开启状态。</li><li>源数据库和目标数据库的参数server_uuid相同, 将导致增量迁移失败。</li><li>源数据库和目标数据库的参数collation_server需保持一致，否则可能导致迁移失败。</li><li>所选迁移对象和外键依赖的表需一起进行迁移，否则会导致迁移失败。</li><li>源数据库和目标数据库的参数time_zone需保持一致，否则可能导致迁移失败。</li><li>源数据库和目标数据库的sql_mode参数值需保持一致，否则可能导致迁移失败。</li><li>迁移的对象中包含引擎为MyISAM的表，则目标数据库sql_mode不能包含no_engine_substitution参数，否则可能会导致迁移失败。</li><li>源数据库和目标数据库的innodb_strict_mode参数值需保持一致，否则可能导致迁移失败。</li><li>目标数据库和源数据库的lower_case_table_names参数需保持一致，否则可能导致迁移失败。</li><li>目标数据库的log_bin_trust_function_creators参数需设置为on，否则可能导致迁移失败。</li></ul>
</td>
</tr>
</tbody>
</table>


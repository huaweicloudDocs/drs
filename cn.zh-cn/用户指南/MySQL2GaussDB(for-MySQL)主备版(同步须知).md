# MySQL-\>GaussDB\(for MySQL\)主备版<a name="drs_03_1124"></a>

## 使用技巧（需要人为配合）<a name="section98341051155812"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section83714237916)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。
    -   同步无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。
    -   由于MySQL固有特点限制，CPU资源紧张时，存储引擎为Tokudb的表，读取速度可能下降至10%。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section83714237916"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table447817192112"></a>
<table><thead align="left"><tr id="row247717122116"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p1448817102113"><a name="p1448817102113"></a><a name="p1448817102113"></a><strong id="b5481417172113"><a name="b5481417172113"></a><a name="b5481417172113"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p1948161716213"><a name="p1948161716213"></a><a name="p1948161716213"></a><strong id="b2481717102115"><a name="b2481717102115"></a><a name="b2481717102115"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row5481117142115"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p248121711219"><a name="p248121711219"></a><a name="p248121711219"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul134813171215"></a><a name="ul134813171215"></a><ul id="ul134813171215"><li><a href="#table1291601510111">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>相互关联的数据对象要确保同时同步，避免因关联对象缺失，导致同步失败。常见的关联关系：视图引用表、视图引用视图、存储过程/函数/触发器引用视图/表、主外键关联表等。</li><li>不支持源数据库恢复到之前时间点的操作(PITR)。</li><li>支持断点续传功能，但是对于无主键的表可能会出现重复插入数据的情况。</li><li>创建同步任务时，不允许将目标库设为只读。</li><li>源库和目标库是相同的RDS实例时，不支持没有库映射的<span id="text134841714211"><a name="text134841714211"></a><a name="text134841714211"></a>实时同步</span>。</li><li>源库不允许存在与目标库同名的无主键表。</li><li>不支持目标数据库恢复到全量同步时间段范围内的PITR操作。</li><li>不支持外键级联操作。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li><li>源库和目标库为RDS for MySQL实例时，不支持带有TDE特性并建立具有加密功能表。</li></ul>
</td>
</tr>
<tr id="row1548151702116"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p114811742114"><a name="p114811742114"></a><a name="p114811742114"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul15482178216"></a><a name="ul15482178216"></a><ul id="ul15482178216"><li>同步过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>不支持强制清理binlog，否则会导致同步任务失败。</li><li>当在全量同步过程中，对MyISAM表执行修改操作时，可能造成数据不一致。</li><li>全量同步过程中不支持DDL操作。</li><li>表级同步时，增量同步过程中只支持表的DDL操作。</li><li>选择表级对象同步时，增量同步过程中不建议对表进行重命名操作。</li><li>使用了附加列功能，单表的列数超过500时，对该表添加附加列可能会超过列数上限，会导致任务失败。</li><li>建议将expire_log_day参数设置在合理的范围，确保恢复时断点处的binlog尚未过期，以保证服务中断后的顺利恢复。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section1645253517920"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table1291601510111"></a>
<table><thead align="left"><tr id="row1691661551120"><th class="cellrowborder" valign="top" width="18.39%" id="mcps1.2.3.1.1"><p id="p99168157118"><a name="p99168157118"></a><a name="p99168157118"></a><strong id="b13916151511117"><a name="b13916151511117"></a><a name="b13916151511117"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.61%" id="mcps1.2.3.1.2"><p id="p3916715121114"><a name="p3916715121114"></a><a name="p3916715121114"></a><strong id="b691661521115"><a name="b691661521115"></a><a name="b691661521115"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row16916815121117"><td class="cellrowborder" valign="top" width="18.39%" headers="mcps1.2.3.1.1 "><p id="p16916111517112"><a name="p16916111517112"></a><a name="p16916111517112"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.61%" headers="mcps1.2.3.1.2 "><a name="ul11917615121115"></a><a name="ul11917615121115"></a><ul id="ul11917615121115"><li>源数据库帐户需要具备如下权限：SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</li><li>目标数据库帐号必须拥有如下权限：SELECT、CREATE、DROP、DELETE、INSERT、UPDATE、INDEX、EVENT、CREATE VIEW、CREATE ROUTINE、TRIGGER、WITH GRANT OPTION。</li></ul>
</td>
</tr>
<tr id="row13917181581110"><td class="cellrowborder" valign="top" width="18.39%" headers="mcps1.2.3.1.1 "><p id="p191711514117"><a name="p191711514117"></a><a name="p191711514117"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.61%" headers="mcps1.2.3.1.2 "><a name="ul36492315100"></a><a name="ul36492315100"></a><ul id="ul36492315100"><li>支持表、主键索引、唯一索引、普通索引、存储过程、视图、函数的同步，不支持事件、触发器的同步。</li><li>库映射时源库中不允许存在存储过程、视图、函数对象。</li><li>映射的库中不允许存在除表外的对象且在同步过程中不允许创建这些对象，否则会导致同步任务失败。</li><li>不支持非MyISAM和非InnoDB表的同步。</li><li>不支持已选择的表与未选择的表之间互相rename的DDL操作，否则会导致同步任务失败。</li></ul>
</td>
</tr>
<tr id="row7918111541116"><td class="cellrowborder" valign="top" width="18.39%" headers="mcps1.2.3.1.1 "><p id="p209181315151120"><a name="p209181315151120"></a><a name="p209181315151120"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.61%" headers="mcps1.2.3.1.2 "><a name="ul17312412391"></a><a name="ul17312412391"></a><ul id="ul17312412391"><li>MySQL源数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议源数据库binlog保存时间越长越好，建议为3天。</li><li>源数据库expire_logs_days参数值为0，可能会导致同步失败。</li><li>增量同步时，必须设置MySQL源数据库的server_id。如果源数据库版本小于或等于MySQL5.6，server_id的取值范围在2－4294967296之间；如果源数据库版本大于或等于MySQL5.7，server_id的取值范围在1－4294967296之间。</li><li>源数据库中的库名、表名、视图名不能包含：'&lt;`&gt;/\以及非ASCII字符。</li><li>不支持非MyISAM和非InnoDB的表同步到RDS。</li></ul>
<a name="ul14902561114"></a><a name="ul14902561114"></a><ul id="ul14902561114"><li>源数据库中的库名和库映射的名称不允许为ib_logfile。</li><li>数据库映射时，源库中存在视图、存储过程等对象，可能会导致<span id="text74269361043"><a name="text74269361043"></a><a name="text74269361043"></a>实时同步</span>失败。</li></ul>
</td>
</tr>
<tr id="row4918915111120"><td class="cellrowborder" valign="top" width="18.39%" headers="mcps1.2.3.1.1 "><p id="p1991861571111"><a name="p1991861571111"></a><a name="p1991861571111"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.61%" headers="mcps1.2.3.1.2 "><a name="ul691815151114"></a><a name="ul691815151114"></a><ul id="ul691815151114"><li>目标数据库实例的运行状态必须正常。</li><li>目标数据库实例必须有足够的磁盘空间。</li></ul>
<a name="ul10475104441519"></a><a name="ul10475104441519"></a><ul id="ul10475104441519"><li>除了MySQL系统数据库之外，当目标库和源库同名时，目标数据库中若存在与源库同名的表，则表结构必须与源库保持一致。</li><li>目标数据库的字符集必须与源数据库一致。</li><li>目标数据库的时区设置必须与源数据库一致。</li><li>同步的对象中包含引擎为MyISAM的表，则目标数据库sql_mode不能包含no_engine_substitution参数，否则可能会导致同步失败。</li></ul>
</td>
</tr>
</tbody>
</table>


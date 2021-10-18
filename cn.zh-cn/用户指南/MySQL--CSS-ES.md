# MySQL-\>CSS/ES<a name="drs_04_0460"></a>

## 使用技巧（需要人为配合）<a name="section449714073815"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1691943218231)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section1691943218231"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table6669158121317"></a>
<table><thead align="left"><tr id="row1266958141317"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p667016871319"><a name="p667016871319"></a><a name="p667016871319"></a><strong id="b36734814134"><a name="b36734814134"></a><a name="b36734814134"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p367420813132"><a name="p367420813132"></a><a name="p367420813132"></a><strong id="b3674158181318"><a name="b3674158181318"></a><a name="b3674158181318"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row126746851319"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1467419871316"><a name="p1467419871316"></a><a name="p1467419871316"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul567488121311"></a><a name="ul567488121311"></a><ul id="ul567488121311"><li><a href="#table14964101613137">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>不支持外键级联操作。</li><li>增量同步会过滤所有的DDL操作。</li><li>不支持源数据库恢复到全量同步时间段范围内的PITR操作。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li><li>源库为RDS for MySQL实例时，不支持带有TDE特性并建立具有加密功能表。</li></ul>
</td>
</tr>
<tr id="row196741983132"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p176751480139"><a name="p176751480139"></a><a name="p176751480139"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul12996271422"></a><a name="ul12996271422"></a><ul id="ul12996271422"><li>在任务启动、任务全量同步阶段，不建议对源数据库做DDL操作</li><li>同步过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>增量同步过程中，若源库存在分布式事务，可能会导致同步失败。</li><li>为了保持数据一致性，不允许对正在同步中的目标数据库进行修改操作（包括但不限于DDL操作）。</li><li>增量同步阶段，支持断点续传功能，在主机系统崩溃的情况下，对于非事务性的无主键的表可能会出现重复插入数据的情况。</li><li>同步过程中，不允许源库写入binlog格式为statement的数据。</li><li>同步过程中，不允许源库执行清除binlog的操作。</li><li>选择表级对象同步时，增量同步过程中不支持对表进行重命名操作。</li><li>同步过程中，不允许在源库创建库名为ib_logfile的数据库。</li><li>建议将expire_log_day参数设置在合理的范围，确保恢复时断点处的binlog尚未过期，以保证服务中断后的顺利恢复。</li><li>binary的值会base64 加密后再写入目标库</li><li>datetime类型源库无时区到目标库则是用户指定的</li><li>源库时间字段目标库不支持的范围统一转成null</li><li>源库类型是binary类型会截断后面为0的字节，原因是源库是定长的自动补齐长度，目标库是变长类型。</li><li>表字段名称全部转成小写。</li><li>目标库数据_id如果指定源库多列生成需要用“:”分隔。</li><li>选择同步对象时，单次选择的库表名称和列名称的大小不能超过4M。如果超过该限制，可以通过再编辑同步对象功能，分批增加同步对象。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section86695405239"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table14964101613137"></a>
<table><thead align="left"><tr id="row4964191661318"><th class="cellrowborder" valign="top" width="18.29%" id="mcps1.2.3.1.1"><p id="p1496471613137"><a name="p1496471613137"></a><a name="p1496471613137"></a><strong id="b1964131615138"><a name="b1964131615138"></a><a name="b1964131615138"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.71000000000001%" id="mcps1.2.3.1.2"><p id="p1896510163133"><a name="p1896510163133"></a><a name="p1896510163133"></a><strong id="b1996541615137"><a name="b1996541615137"></a><a name="b1996541615137"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row89651816131318"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p8965616181312"><a name="p8965616181312"></a><a name="p8965616181312"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><p id="p5628114194513"><a name="p5628114194513"></a><a name="p5628114194513"></a><strong id="b2628201410451"><a name="b2628201410451"></a><a name="b2628201410451"></a>全量+增量最小同步权限要求：</strong></p>
<a name="ul1662817141450"></a><a name="ul1662817141450"></a><ul id="ul1662817141450"><li>源数据库帐户需要具备如下权限：<p id="p166281314104516"><a name="p166281314104516"></a><a name="p166281314104516"></a>SELECT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</p>
</li><li>目标数据库帐号必须拥有如下权限：<p id="p1029612232457"><a name="p1029612232457"></a><a name="p1029612232457"></a>READ、WRITE。</p>
</li></ul>
</td>
</tr>
<tr id="row109651168135"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p1596591615135"><a name="p1596591615135"></a><a name="p1596591615135"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul59651116191319"></a><a name="ul59651116191319"></a><ul id="ul59651116191319"><li>支持表数据的同步。</li></ul>
<a name="ul1581416459456"></a><a name="ul1581416459456"></a><ul id="ul1581416459456"><li>不支持数据库、视图、索引、约束、函数、存储过程、触发器（TRIGGER）和事件（EVENT）的同步。</li><li>不支持系统库的同步以及事件状态的同步。</li></ul>
</td>
</tr>
<tr id="row12965916181317"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p9966616101320"><a name="p9966616101320"></a><a name="p9966616101320"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul18911176184620"></a><a name="ul18911176184620"></a><ul id="ul18911176184620"><li>源数据库中的库名不能包含：'&lt;`&gt;/\"以及非ASCII字符。</li><li>源数据库中的表名、视图名不能包含：'&lt;&gt;/\"以及非ASCII字符。</li><li>源数据库中的库名不允许为ib_logfile。</li><li>MySQL源数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议源数据库binlog保存时间越长越好，建议为3天。</li><li>源数据库expire_logs_days参数值为0，可能会导致同步失败。</li><li>增量同步时，必须设置MySQL源数据库的server_id。如果源数据库版本小于或等于MySQL5.6，server_id的取值范围在2－4294967296之间；如果源数据库版本大于或等于MySQL5.7，server_id的取值范围在1－4294967296之间。</li><li>MySQL源数据库建议开启skip-name-resolve，减少连接超时的可能性。</li><li>源数据库GTID状态建议为开启状态。</li><li>源库不支持mysql binlog dump命令。</li><li>源数据库和目标数据库字符集需保持一致，否则同步失败。</li><li>源数据库log_slave_updates参数需设置为开启状态，否则会导致同步失败。</li><li>源数据库的binlog_row_image参数需设置为FULL，否则会导致同步失败。</li><li>源数据库MySQL8.0目前不支持参数lower_case_table_names等于0的同步。</li></ul>
</td>
</tr>
<tr id="row79670166134"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p2096731610131"><a name="p2096731610131"></a><a name="p2096731610131"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul892915203469"></a><a name="ul892915203469"></a><ul id="ul892915203469"><li>目标数据库实例的运行状态必须正常。</li><li>目标数据库实例必须有足够的磁盘空间。</li></ul>
</td>
</tr>
</tbody>
</table>


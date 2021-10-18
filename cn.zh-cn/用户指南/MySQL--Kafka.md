# MySQL-\>Kafka<a name="drs_04_0118"></a>

## 使用技巧（需要人为配合）<a name="section449714073815"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1691943218231)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   同步无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
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
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul567488121311"></a><a name="ul567488121311"></a><ul id="ul567488121311"><li><a href="#table14964101613137">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>不支持外键级联操作。</li><li>不支持源数据库恢复到之前时间点的操作(PITR)。</li><li>支持断点续传功能，但是对于无主键的表可能会出现重复插入数据的情况。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li><li>数据类型不兼容时，可能引起同步失败。</li><li>源库为RDS for MySQL实例时，不支持带有TDE特性并建立具有加密功能表。</li></ul>
</td>
</tr>
<tr id="row196741983132"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p176751480139"><a name="p176751480139"></a><a name="p176751480139"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul86758815135"></a><a name="ul86758815135"></a><ul id="ul86758815135"><li><span id="text1667515841318"><a name="text1667515841318"></a><a name="text1667515841318"></a>实时同步</span>过程中，如果修改了源库的用户名、密码，会导致同步任务失败，需要在数据复制服务控制台将上述信息重新修改正确，然后重试任务可继续进行<span id="text116752082133"><a name="text116752082133"></a><a name="text116752082133"></a>实时同步</span>。一般情况下不建议在同步过程中修改上述信息。</li><li><span id="text20675128181316"><a name="text20675128181316"></a><a name="text20675128181316"></a>实时同步</span>过程中，如果修改了源库端口，会导致同步任务失败。针对该情况，系统自动更新为正确的端口，重试任务后即可进行同步。一般情况下不建议在同步过程中修改端口。</li><li><span id="text067511881313"><a name="text067511881313"></a><a name="text067511881313"></a>实时同步</span>过程中，对于因修改IP地址导致同步任务失败的情况，系统自动更新为正确的IP地址，需要重试任务可继续进行同步。一般情况下，不建议修改IP地址。</li><li>不支持强制清理binlog，否则会导致同步任务失败。</li><li>当在同步过程中，对MyISAM表执行修改操作时，可能造成数据不一致。</li><li>选择表级对象同步时，同步过程中不建议对表进行重命名操作。</li><li>建议将expire_log_day参数设置在合理的范围，确保恢复时断点处的binlog尚未过期，以保证服务中断后的顺利恢复。</li><li>该链路不支持SSL安全连接。</li></ul>
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
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul13965111681311"></a><a name="ul13965111681311"></a><ul id="ul13965111681311"><li>源数据库帐户需要具备如下权限：SELECT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT、RELOAD。</li></ul>
</td>
</tr>
<tr id="row109651168135"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p1596591615135"><a name="p1596591615135"></a><a name="p1596591615135"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul59651116191319"></a><a name="ul59651116191319"></a><ul id="ul59651116191319"><li>支持表数据的同步。</li></ul>
<a name="ul139659167131"></a><a name="ul139659167131"></a><ul id="ul139659167131"><li>不支持非MyISAM和非InnoDB表的同步。</li></ul>
</td>
</tr>
<tr id="row12965916181317"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p9966616101320"><a name="p9966616101320"></a><a name="p9966616101320"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul15966171614139"></a><a name="ul15966171614139"></a><ul id="ul15966171614139"><li>MySQL源数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议源数据库binlog保存时间越长越好，建议为3天。</li><li>源数据库expire_logs_days参数值为0，可能会导致同步失败。</li><li>增量同步时，必须设置MySQL源数据库的server_id。如果源数据库版本小于或等于MySQL5.6，server_id的取值范围在2－4294967296之间；如果源数据库版本大于或等于MySQL5.7，server_id的取值范围在1－4294967296之间。</li><li>源数据库中的库、表名不能包含：'&lt;`&gt;/\以及非ASCII字符。</li></ul>
</td>
</tr>
<tr id="row79670166134"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p2096731610131"><a name="p2096731610131"></a><a name="p2096731610131"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><p id="p1296720167139"><a name="p1296720167139"></a><a name="p1296720167139"></a>消费时 isolation.level 参数为read_committed。</p>
</td>
</tr>
</tbody>
</table>


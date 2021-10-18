# GaussDB\(for MySQL\)主备版-\>Kafka<a name="drs_04_0450"></a>

## 操作要求<a name="section1610153915412"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table12647171253513"></a>
<table><thead align="left"><tr id="row1564871213515"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p3648412193518"><a name="p3648412193518"></a><a name="p3648412193518"></a><strong id="b17648512133512"><a name="b17648512133512"></a><a name="b17648512133512"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p464812124355"><a name="p464812124355"></a><a name="p464812124355"></a><strong id="b18648131218355"><a name="b18648131218355"></a><a name="b18648131218355"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row664891218358"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1364831210356"><a name="p1364831210356"></a><a name="p1364831210356"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1864810128358"></a><a name="ul1864810128358"></a><ul id="ul1864810128358"><li><a href="#table1165317124353">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li></ul>
<a name="ul546342714715"></a><a name="ul546342714715"></a><ul id="ul546342714715"><li>不支持外键级联操作。</li><li>不支持源数据库恢复到之前时间点的操作(PITR)。</li><li>支持断点续传功能，但是对于无主键的表可能会出现重复插入数据的情况。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li><li>数据类型不兼容时，可能引起同步失败。</li></ul>
</td>
</tr>
<tr id="row1265191218352"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p465151223517"><a name="p465151223517"></a><a name="p465151223517"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul311585588"></a><a name="ul311585588"></a><ul id="ul311585588"><li>增量同步过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>不支持强制清理binlog，否则会导致同步任务失败。</li><li>该链路不支持SSL安全连接。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section165311339195419"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table1165317124353"></a>
<table><thead align="left"><tr id="row186541712123514"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p13654201219353"><a name="p13654201219353"></a><a name="p13654201219353"></a><strong id="b1465491203520"><a name="b1465491203520"></a><a name="b1465491203520"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p1765401210352"><a name="p1765401210352"></a><a name="p1765401210352"></a><strong id="b14654212193514"><a name="b14654212193514"></a><a name="b14654212193514"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row26541126359"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p765513125358"><a name="p765513125358"></a><a name="p765513125358"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul12455726185518"></a><a name="ul12455726185518"></a><ul id="ul12455726185518"><li>源数据库帐户需要具备如下权限：SELECT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT、RELOAD。</li></ul>
</td>
</tr>
<tr id="row365561219359"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p865571218352"><a name="p865571218352"></a><a name="p865571218352"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul164551726105519"></a><a name="ul164551726105519"></a><ul id="ul164551726105519"><li>支持表数据的同步。</li></ul>
<a name="ul1245572615556"></a><a name="ul1245572615556"></a><ul id="ul1245572615556"><li>不支持非MyISAM和非InnoDB表的同步。</li></ul>
</td>
</tr>
<tr id="row1865611218353"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p19657191273514"><a name="p19657191273514"></a><a name="p19657191273514"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul44561926135515"></a><a name="ul44561926135515"></a><ul id="ul44561926135515"><li>源数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议源数据库binlog保存时间越长越好，建议为3天。</li><li>源数据库expire_logs_days参数值为0，可能会导致同步失败。</li><li>必须设置MySQL源数据库的server_id，server_id的取值范围在1－4294967296之间。</li><li>源数据库中的库、表名不能包含：'&lt;`&gt;/\以及非ASCII字符。</li></ul>
</td>
</tr>
<tr id="row365941218353"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p196598122350"><a name="p196598122350"></a><a name="p196598122350"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul617932422417"></a><a name="ul617932422417"></a><ul id="ul617932422417"><li>消费时 isolation.level 参数为read_committed。</li><li>目标库为普通Kafka。</li></ul>
</td>
</tr>
</tbody>
</table>


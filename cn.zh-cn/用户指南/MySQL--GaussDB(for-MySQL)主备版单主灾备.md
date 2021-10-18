# MySQL-\>GaussDB\(for MySQL\)主备版单主灾备<a name="drs_04_0123"></a>

## 使用技巧（需要人为配合）<a name="section1923414505593"></a>

建议您配合如下使用技巧和[操作要求](#section17465143816328)，进行灾备以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行灾备任务。
    -   全量灾备会对源数据库有一定的访问压力。
    -   灾备无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
    -   正在灾备的数据被其他事务长时间锁死，可能导致读数据超时。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section17465143816328"></a>

在使用数据复制服务进行数据灾备的过程中，存在一些无法预知或因人为因素及环境突变导致同步失败的情况，针对该情况，数据复制服务提供以下常见的操作限制，供您在数据灾备过程中参考。

**表 1**  操作要求

<a name="table1552118332341"></a>
<table><thead align="left"><tr id="row155229333349"><th class="cellrowborder" valign="top" width="18.44%" id="mcps1.2.3.1.1"><p id="p17522833163418"><a name="p17522833163418"></a><a name="p17522833163418"></a><strong id="b852203353414"><a name="b852203353414"></a><a name="b852203353414"></a>类型</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.56%" id="mcps1.2.3.1.2"><p id="p11522133343413"><a name="p11522133343413"></a><a name="p11522133343413"></a><strong id="b4522163393413"><a name="b4522163393413"></a><a name="b4522163393413"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row1552223310346"><td class="cellrowborder" valign="top" width="18.44%" headers="mcps1.2.3.1.1 "><p id="p195227330348"><a name="p195227330348"></a><a name="p195227330348"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.56%" headers="mcps1.2.3.1.2 "><a name="ul135221633153415"></a><a name="ul135221633153415"></a><ul id="ul135221633153415"><li><a href="#table280819474349">表2</a>中的环境要求均不允许在灾备过程中修改，直至灾备结束。</li><li>业务数据库进行的参数修改不会记录在日志里，所以也不会同步至灾备数据库，请在灾备数据库升主后调整参数。</li><li>外部数据库创建的高权限用户若超出RDS MySQL支持范围，不会同步至灾备数据库，如super权限。</li><li>不支持外键级联操作。</li><li>不支持业务数据库恢复到之前时间点的操作(PITR)。</li><li>不支持强制清理binlog，否则会导致灾备任务失败。</li><li>网络中断在30秒内恢复的，不影响数据灾备，超过30秒，则可能会导致灾备任务失败。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建灾备任务。</li><li>支持断点续传功能，但对于无主键的表可能会出现重复插入数据的情况。</li><li>存在灾备任务时，不允许创迁移或者同步任务。</li><li>灾备为单主灾备关系，不支持多写的多主模式，如果外部数据库没有提供superuser权限，则外部数据库为备时无法设置只读，请严格确保备节点的数据只来自主节点的同步，任何其他地方的写入将会导致备库数据被污染，使得灾备出现数据冲突而无法修复。</li><li>如果外部数据库为备且为只读，该只读只有superuser权限的账号可以写入数据，其他账号无法写入，但仍然需要确保备节点通过这个账号写入任何数据导致备库数据被污染，使得灾备出现数据冲突而无法修复。</li><li>低版本到高版本灾备时，业务活动需要同时兼容低版本和高版本，否则容易造成灾备失败。</li><li>业务数据库为RDS for MySQL实例时，不支持带有TDE特性并建立具有加密功能表。</li></ul>
</td>
</tr>
<tr id="row1152317339348"><td class="cellrowborder" valign="top" width="18.44%" headers="mcps1.2.3.1.1 "><p id="p2523143313341"><a name="p2523143313341"></a><a name="p2523143313341"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.56%" headers="mcps1.2.3.1.2 "><a name="ul175231033123419"></a><a name="ul175231033123419"></a><ul id="ul175231033123419"><li>数据灾备过程中，如果修改了业务库用于灾备的密码，会导致该灾备任务失败，需要在数据复制服务控制台将上述信息重新修改正确，然后重试任务可继续进行数据灾备。一般情况下不建议在灾备过程中修改上述信息。</li><li>数据灾备过程中，如果修改了业务库端口，会导致该灾备任务失败。一般情况下不建议在灾备过程中修改业务库端口。</li><li>数据灾备过程中，如果业务库为非本云关系型数据库实例，不支持修改IP地址。本云关系型数据库实例，对于因修改IP地址导致灾备任务失败的情况，系统自动更新为正确的IP地址，重试任务可继续进行同步。一般情况下，不建议修改IP地址。</li><li>数据灾备过程中，不建议做删除类型的DDL操作，可能会引起任务失败。</li><li>禁止源端在灾备任务执行主备倒换过程中进行写入操作，否则会出现数据污染或者表结构不一致，并最终导致业务端和灾备端数据不一致。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section3303545163218"></a>

在使用数据复制服务进行数据灾备的过程中，对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table280819474349"></a>
<table><thead align="left"><tr id="row1880817470349"><th class="cellrowborder" valign="top" width="17.89%" id="mcps1.2.3.1.1"><p id="p14809104718346"><a name="p14809104718346"></a><a name="p14809104718346"></a><strong id="b7809247113414"><a name="b7809247113414"></a><a name="b7809247113414"></a>类型</strong></p>
</th>
<th class="cellrowborder" valign="top" width="82.11%" id="mcps1.2.3.1.2"><p id="p19809847153419"><a name="p19809847153419"></a><a name="p19809847153419"></a><strong id="b17809114763415"><a name="b17809114763415"></a><a name="b17809114763415"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row080954719343"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p1880914714344"><a name="p1880914714344"></a><a name="p1880914714344"></a>数据库权限配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul11809104723417"></a><a name="ul11809104723417"></a><ul id="ul11809104723417"><li>业务数据库帐户需要具备如下权限：SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、TRIGGER、SHOW VIEW、EVENT、INDEX、LOCK TABLES、CREATE VIEW、 CREATE ROUTINE、 ALTER ROUTINE、 CREATE USER、RELOAD、REPLICATION SLAVE、REPLICATION CLIENT、WITH GRANT OPTION。</li><li>灾备数据库帐户需要具备如下权限：SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、TRIGGER、SHOW VIEW、EVENT、INDEX、LOCK TABLES、CREATE VIEW、 CREATE ROUTINE、 ALTER ROUTINE、 CREATE USER、RELOAD、REPLICATION SLAVE、REPLICATION CLIENT、WITH GRANT OPTION。</li><li>RDS for MySQL实例的root帐户默认已具备上述权限。</li></ul>
</td>
</tr>
<tr id="row880994773412"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p1680914719347"><a name="p1680914719347"></a><a name="p1680914719347"></a>灾备对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul118091947193418"></a><a name="ul118091947193418"></a><ul id="ul118091947193418"><li>不支持非MyISAM和非InnoDB表的灾备。</li><li>不支持系统表。</li><li>不支持触发器和事件的灾备。</li><li>不支持对系统库下自定义对象有操作权限的帐号灾备。</li><li>不支持指定部分业务库进行灾备，跨库DDL、rename等操作将造成容灾失败。</li></ul>
</td>
</tr>
<tr id="row15810164773413"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p15810134719343"><a name="p15810134719343"></a><a name="p15810134719343"></a>业务数据库配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul4810747153419"></a><a name="ul4810747153419"></a><ul id="ul4810747153419"><li>MySQL业务数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议业务数据库binlog保存时间越长越好，建议为7天。</li><li>业务库不允许存在空账号或者空密码。</li><li>灾备中，必须设置MySQL业务数据库的server－id。如果业务数据库版本小于或等于MySQL5.6，server－id的取值范围为2~4294967296；如果业务数据库版本大于或等于MySQL5.7，server－id的取值范围为1~4294967296。</li><li>业务数据库须开启GTID。</li><li>业务数据库名称在1到64个字符之间，由小写字母、数字、中划线、下划线组成，不能包含其他特殊字符。</li><li>业务数据库中的表名、视图名不能包含：'&lt;&gt;/\以及非ASCII字符。</li><li>数据库expire_logs_days参数值为0，可能会导致灾备失败。</li></ul>
</td>
</tr>
<tr id="row68115472343"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p19811134710349"><a name="p19811134710349"></a><a name="p19811134710349"></a>灾备数据库配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul18811194715348"></a><a name="ul18811194715348"></a><ul id="ul18811194715348"><li>灾备数据库实例的运行状态必须正常，若数据库实例是主备实例，复制状态也必须正常。</li><li>灾备数据库实例必须有足够的磁盘空间。</li><li>除了系统数据库之外，灾备库必须是空实例。</li><li>灾备数据库需开启binlog和GTID。</li></ul>
</td>
</tr>
</tbody>
</table>


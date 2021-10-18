# GaussDB\(for MySQL\)主备版-\>GaussDB\(for MySQL\)主备版单主灾备<a name="drs_03_1119"></a>

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

<a name="table6923195824315"></a>
<table><thead align="left"><tr id="row18923358154311"><th class="cellrowborder" valign="top" width="18.44%" id="mcps1.2.3.1.1"><p id="p109231958144312"><a name="p109231958144312"></a><a name="p109231958144312"></a><strong id="b189231158164315"><a name="b189231158164315"></a><a name="b189231158164315"></a>类型</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.56%" id="mcps1.2.3.1.2"><p id="p14923858134315"><a name="p14923858134315"></a><a name="p14923858134315"></a><strong id="b1692385884312"><a name="b1692385884312"></a><a name="b1692385884312"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row992395854318"><td class="cellrowborder" valign="top" width="18.44%" headers="mcps1.2.3.1.1 "><p id="p149231158124313"><a name="p149231158124313"></a><a name="p149231158124313"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.56%" headers="mcps1.2.3.1.2 "><a name="ul1192315812439"></a><a name="ul1192315812439"></a><ul id="ul1192315812439"><li><a href="#table8998563443">表2</a>中的环境要求均不允许在灾备过程中修改，直至灾备结束。</li><li>业务数据库进行的参数修改不会记录在日志里，所以也不会同步至灾备数据库，请在灾备数据库升主后调整参数。</li><li>不支持业务数据库恢复到之前时间点的操作(PITR)。</li><li>不支持强制清理binlog，否则会导致灾备任务失败。</li><li>网络中断在30秒内恢复的，不影响数据灾备，超过30秒，则可能会导致灾备任务失败。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建灾备任务。</li><li>支持断点续传功能，但对于无主键的表可能会出现重复插入数据的情况。</li><li>存在灾备任务时，不允许创迁移或者同步任务。</li><li>灾备为单主灾备关系，不支持多写的多主模式，请严格确保备节点的数据只来自主节点的同步，任何其他地方的写入将会导致备库数据被污染，使得灾备出现数据冲突而无法修复。</li><li>如果外部数据库为备且为只读，该只读只有superuser权限的账号可以写入数据，其他账号无法写入，但仍然需要确保备节点通过这个账号写入任何数据导致备库数据被污染，使得灾备出现数据冲突而无法修复。</li></ul>
</td>
</tr>
<tr id="row15924155844312"><td class="cellrowborder" valign="top" width="18.44%" headers="mcps1.2.3.1.1 "><p id="p119244585438"><a name="p119244585438"></a><a name="p119244585438"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.56%" headers="mcps1.2.3.1.2 "><a name="ul892418585438"></a><a name="ul892418585438"></a><ul id="ul892418585438"><li>数据灾备过程中，如果修改了业务库用于灾备的密码，会导致该灾备任务失败，需要在数据复制服务控制台将上述信息重新修改正确，然后重试任务可继续进行数据灾备。一般情况下不建议在灾备过程中修改上述信息。</li><li>数据灾备过程中，如果修改了业务库端口，会导致该灾备任务失败。一般情况下不建议在灾备过程中修改业务库端口。</li><li>数据灾备过程中，本云关系型数据库实例，对于因修改IP地址导致灾备任务失败的情况，系统自动更新为正确的IP地址，重试任务可继续进行同步。一般情况下，不建议修改IP地址。</li><li>数据灾备过程中，不建议做删除类型的DDL操作，可能会引起任务失败。</li><li>禁止源端在灾备任务执行主备倒换过程中进行写入操作，否则会出现数据污染或者表结构不一致，并最终导致业务端和灾备端数据不一致。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section17319599322"></a>

在使用数据复制服务进行数据灾备的过程中，对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table8998563443"></a>
<table><thead align="left"><tr id="row11998166124414"><th class="cellrowborder" valign="top" width="17.89%" id="mcps1.2.3.1.1"><p id="p399819611449"><a name="p399819611449"></a><a name="p399819611449"></a><strong id="b119981668447"><a name="b119981668447"></a><a name="b119981668447"></a>类型</strong></p>
</th>
<th class="cellrowborder" valign="top" width="82.11%" id="mcps1.2.3.1.2"><p id="p59984674414"><a name="p59984674414"></a><a name="p59984674414"></a><strong id="b39980615447"><a name="b39980615447"></a><a name="b39980615447"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row39981767442"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p399856114411"><a name="p399856114411"></a><a name="p399856114411"></a>数据库权限配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul2998765445"></a><a name="ul2998765445"></a><ul id="ul2998765445"><li>业务数据库帐户需要具备如下权限：SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、TRIGGER、SHOW VIEW、EVENT、INDEX、LOCK TABLES、CREATE VIEW、 CREATE ROUTINE、 ALTER ROUTINE、 CREATE USER、RELOAD、REPLICATION SLAVE、REPLICATION CLIENT、WITH GRANT OPTION。</li><li>灾备数据库帐户需要具备如下权限：SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、TRIGGER、SHOW VIEW、EVENT、INDEX、LOCK TABLES、CREATE VIEW、 CREATE ROUTINE、 ALTER ROUTINE、 CREATE USER、RELOAD、REPLICATION SLAVE、REPLICATION CLIENT、WITH GRANT OPTION。</li><li>GaussDB(for MySQL)主备版实例的root帐户默认已具备上述权限。</li></ul>
</td>
</tr>
<tr id="row299915614448"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p1999926154414"><a name="p1999926154414"></a><a name="p1999926154414"></a>灾备对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul189997614444"></a><a name="ul189997614444"></a><ul id="ul189997614444"><li>不支持非MyISAM和非InnoDB表的灾备。</li><li>不支持系统表。</li><li>不支持触发器和事件的灾备。</li><li>不支持对系统库下自定义对象有操作权限的帐号灾备。</li><li>不支持指定部分业务库进行灾备，跨库DDL、rename等操作将造成容灾失败。</li></ul>
</td>
</tr>
<tr id="row14999176184418"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p1599912615448"><a name="p1599912615448"></a><a name="p1599912615448"></a>业务数据库配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul12999962448"></a><a name="ul12999962448"></a><ul id="ul12999962448"><li>业务数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议业务数据库binlog保存时间越长越好，建议为7天。</li><li>业务数据库须开启GTID。</li><li>业务数据库名称在1到64个字符之间，由小写字母、数字、中划线、下划线组成，不能包含其他特殊字符。</li><li>业务数据库中的表名、视图名不能包含：'&lt;&gt;/\以及非ASCII字符。</li></ul>
</td>
</tr>
<tr id="row7007114411"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p5012719445"><a name="p5012719445"></a><a name="p5012719445"></a>灾备数据库配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul1108717446"></a><a name="ul1108717446"></a><ul id="ul1108717446"><li>灾备数据库实例的运行状态必须正常，若数据库实例是主备实例，复制状态也必须正常。</li><li>灾备数据库实例必须有足够的磁盘空间。</li><li>灾备数据库大版本号必须与业务库保持一致。</li><li>灾备库必须是空实例，且灾备任务开始后灾备库会被设置成只读。</li><li>灾备数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>灾备数据库须开启GTID。</li></ul>
</td>
</tr>
</tbody>
</table>


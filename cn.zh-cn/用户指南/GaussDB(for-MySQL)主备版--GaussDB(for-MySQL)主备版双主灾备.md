# GaussDB\(for MySQL\)主备版-\>GaussDB\(for MySQL\)主备版双主灾备<a name="drs_04_0129"></a>

## 使用技巧（需要人为配合）<a name="section1923414505593"></a>

建议您配合如下使用技巧和[操作要求](#section17465143816328)，进行灾备以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行灾备任务。
    -   全量灾备会对源数据库有一定的访问压力。
    -   灾备无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
    -   正在灾备的数据被其他事务长时间锁死，可能导致读数据超时。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section17465143816328"></a>

在使用数据复制服务进行双主数据灾备的过程中，存在一些无法预知或因人为因素及环境突变导致同步失败的情况，针对该情况，数据复制服务提供以下常见的操作限制，供您在双主灾备过程中参考。

**表 1**  操作要求

<a name="table1562974574617"></a>
<table><thead align="left"><tr id="row062912453460"><th class="cellrowborder" valign="top" width="18.44%" id="mcps1.2.3.1.1"><p id="p963018454469"><a name="p963018454469"></a><a name="p963018454469"></a><strong id="b3630154504619"><a name="b3630154504619"></a><a name="b3630154504619"></a>类型</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.56%" id="mcps1.2.3.1.2"><p id="p13630845194614"><a name="p13630845194614"></a><a name="p13630845194614"></a><strong id="b196302045174617"><a name="b196302045174617"></a><a name="b196302045174617"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row1063014514619"><td class="cellrowborder" valign="top" width="18.44%" headers="mcps1.2.3.1.1 "><p id="p156303454462"><a name="p156303454462"></a><a name="p156303454462"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.56%" headers="mcps1.2.3.1.2 "><a name="ul3630945184620"></a><a name="ul3630945184620"></a><ul id="ul3630945184620"><li><a href="#table849153474">表2</a>中的环境要求均不允许在灾备过程中修改，直至灾备结束。</li><li>双主灾备是两条独立的链路，相互之间没有协同作用，由于一些不可控因素，可能会出现使用双边数据不一致的情况（例如，主1负载过重，主2负载较轻，双边同时接入读写操作的业务流量时，由于同步任务的时延差异客观上不可控，导致执行顺序与真实顺序不相同，造成数据错乱）。因此，<strong id="b663094513464"><a name="b663094513464"></a><a name="b663094513464"></a>灾备前请对同一数据进行单元化设计，确保数据单元（可以为库、表、行）一边接读写流量，另一边只能接只读业务，即双主灾备是整体上双主，但微观上数据单元仍然是一边读写，一边只读。</strong>常见场景请参见<a href="https://support.huaweicloud.com/drs_faq/drs_04_0037.html" target="_blank" rel="noopener noreferrer">实时灾备异常场景</a>。</li><li>如果不可避免双边同时刷新同一数据单元，就可能出现数据冲突，针对数据冲突的情况，DRS采用冲突覆盖的策略，即：<a name="ul663044584614"></a><a name="ul663044584614"></a><ul id="ul663044584614"><li>删除时，该数据不存在则忽略，即不做操作。</li><li>插入时，该数据存在则进行替换，即使用新的数据进行更新动作。</li><li>更新时，该数据不存在则插入最新记录。</li></ul>
</li><li>业务需要避免双边主键生成冲突（例如，可以使用uuid方式，或者“区域+自增id”的主键规则来避免冲突）。</li><li>业务方能容忍同步时延一定的波动，同步因故中断或者网络等原因造成的较大延迟，业务上需要考虑其影响性的容忍度。</li><li>双主灾备不同于单主灾备，无需进行主备倒换。</li></ul>
</td>
</tr>
<tr id="row3630945164616"><td class="cellrowborder" valign="top" width="18.44%" headers="mcps1.2.3.1.1 "><p id="p9630745174619"><a name="p9630745174619"></a><a name="p9630745174619"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.56%" headers="mcps1.2.3.1.2 "><a name="ul5630114518468"></a><a name="ul5630114518468"></a><ul id="ul5630114518468"><li>由于灾备的细微时延不可控，业务上执行DDL时要在无业务期，且RPO&amp;RTO =0稳定30s以上在主1执行，避免在主2执行DDL（DRS只同步主1的DDL操作到主2）。</li><li>双边保持严格的对等效果，即表列行均一致（主1和主2的表结构需始终保持一致）。</li><li>在正向任务进入灾备且RPO&amp;RTO小于60s，方可启动反向任务。</li><li>双主灾备进入灾备后，请先在主2进行测试验证，符合预期后再考虑切部分业务流量到主2。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section17319599322"></a>

在使用数据复制服务进行数据灾备的过程中，对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table849153474"></a>
<table><thead align="left"><tr id="row1949452475"><th class="cellrowborder" valign="top" width="17.89%" id="mcps1.2.3.1.1"><p id="p64910513471"><a name="p64910513471"></a><a name="p64910513471"></a><strong id="b174915104717"><a name="b174915104717"></a><a name="b174915104717"></a>类型</strong></p>
</th>
<th class="cellrowborder" valign="top" width="82.11%" id="mcps1.2.3.1.2"><p id="p449205174710"><a name="p449205174710"></a><a name="p449205174710"></a><strong id="b10493584716"><a name="b10493584716"></a><a name="b10493584716"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row84945104711"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p114910564710"><a name="p114910564710"></a><a name="p114910564710"></a>数据库权限配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul194975134714"></a><a name="ul194975134714"></a><ul id="ul194975134714"><li>业务数据库帐户需要具备如下权限：SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、TRIGGER、SHOW VIEW、EVENT、INDEX、LOCK TABLES、CREATE VIEW、 CREATE ROUTINE、 ALTER ROUTINE、 CREATE USER、RELOAD、REPLICATION SLAVE、REPLICATION CLIENT、WITH GRANT OPTION。</li><li>灾备数据库帐户需要具备如下权限：SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、TRIGGER、SHOW VIEW、EVENT、INDEX、LOCK TABLES、CREATE VIEW、 CREATE ROUTINE、 ALTER ROUTINE、 CREATE USER、RELOAD、REPLICATION SLAVE、REPLICATION CLIENT、WITH GRANT OPTION。</li><li>GaussDB(for MySQL)主备版实例的root帐户默认已具备上述权限。</li></ul>
</td>
</tr>
<tr id="row750658470"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p95015584715"><a name="p95015584715"></a><a name="p95015584715"></a>灾备对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul105017512476"></a><a name="ul105017512476"></a><ul id="ul105017512476"><li>不支持非MyISAM和非InnoDB表的灾备。</li><li>不支持系统表。</li><li>不支持触发器和事件的灾备。</li><li>不支持对系统库下自定义对象有操作权限的帐号灾备。</li><li>不支持在主2上执行DDL的场景。</li></ul>
</td>
</tr>
<tr id="row7501510470"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p85018514471"><a name="p85018514471"></a><a name="p85018514471"></a>业务数据库配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul115075174713"></a><a name="ul115075174713"></a><ul id="ul115075174713"><li>业务数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议业务数据库binlog保存时间越长越好，建议为7天。</li><li>业务库不允许存在空账号或者空密码。</li><li>业务数据库须开启GTID。</li><li>业务数据库名称在1到64个字符之间，由小写字母、数字、中划线、下划线组成，不能包含其他特殊字符。</li><li>业务数据库中的表名、视图名不能包含：'&lt;&gt;/\以及非ASCII字符。</li><li>数据库expire_logs_days参数值为0，可能会导致灾备失败。</li></ul>
</td>
</tr>
<tr id="row351456476"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p3518564717"><a name="p3518564717"></a><a name="p3518564717"></a>灾备数据库配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul051754473"></a><a name="ul051754473"></a><ul id="ul051754473"><li>灾备数据库实例的运行状态必须正常，若数据库实例是主备实例，复制状态也必须正常。</li><li>灾备数据库实例必须有足够的磁盘空间。</li><li>主1灾备库大版本号必须与主2灾备库保持一致。</li><li>主2灾备库必须是空实例，且在正向任务启动后主2灾备库会被设置成只读，等待反向任务启动并进行灾备后被恢复成读写。</li></ul>
<a name="ul790113249429"></a><a name="ul790113249429"></a><ul id="ul790113249429"><li>灾备数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>灾备数据库须开启GTID。</li></ul>
</td>
</tr>
</tbody>
</table>


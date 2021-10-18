# MySQL-\>MySQL双主灾备<a name="drs_04_0127"></a>

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

<a name="table72104211454"></a>
<table><thead align="left"><tr id="row42174210457"><th class="cellrowborder" valign="top" width="18.44%" id="mcps1.2.3.1.1"><p id="p152116422456"><a name="p152116422456"></a><a name="p152116422456"></a><strong id="b162194212457"><a name="b162194212457"></a><a name="b162194212457"></a>类型</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.56%" id="mcps1.2.3.1.2"><p id="p202154214512"><a name="p202154214512"></a><a name="p202154214512"></a><strong id="b221194210451"><a name="b221194210451"></a><a name="b221194210451"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row1821542124519"><td class="cellrowborder" valign="top" width="18.44%" headers="mcps1.2.3.1.1 "><p id="p132111420453"><a name="p132111420453"></a><a name="p132111420453"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.56%" headers="mcps1.2.3.1.2 "><a name="ul1121242154519"></a><a name="ul1121242154519"></a><ul id="ul1121242154519"><li><a href="#table028935213452">表2</a>中的环境要求均不允许在灾备过程中修改，直至灾备结束。</li><li>目前仅支持白名单用户使用，需要提交工单申请才能使用。</li><li>双主灾备是两条独立的链路，相互之间没有协同作用，由于一些不可控因素，可能会出现使用双边数据不一致的情况（例如，主1负载过重，主2负载较轻，双边同时接入读写操作的业务流量时，由于同步任务的时延差异客观上不可控，导致执行顺序与真实顺序不相同，造成数据错乱）。因此，<strong id="b121114264510"><a name="b121114264510"></a><a name="b121114264510"></a>灾备前请对同一数据进行单元化设计，确保数据单元（可以为库、表、行）一边接读写流量，另一边只能接只读业务，即双主灾备是整体上双主，但微观上数据单元仍然是一边读写，一边只读。</strong>常见场景请参见<a href="https://support.huaweicloud.com/drs_faq/drs_04_0037.html" target="_blank" rel="noopener noreferrer">实时灾备异常场景</a>。</li><li>如果不可避免双边同时刷新同一数据单元，就可能出现数据冲突，针对数据冲突的情况，DRS采用冲突覆盖的策略，即：<a name="ul422164264510"></a><a name="ul422164264510"></a><ul id="ul422164264510"><li>删除时，该数据不存在则忽略，即不做操作。</li><li>插入时，该数据存在则进行替换，即使用新的数据进行更新动作。</li><li>更新时，该数据不存在则插入最新记录。</li></ul>
</li><li>业务需要避免双边主键生成冲突（例如，可以使用uuid方式，或者“区域+自增id”的主键规则来避免冲突）。</li><li>业务方能容忍同步时延一定的波动，同步因故中断或者网络等原因造成的较大延迟，业务上需要考虑其影响性的容忍度。</li><li>不支持外键级联操作。</li><li>双主灾备不同于单主灾备，无需进行主备倒换。</li></ul>
</td>
</tr>
<tr id="row62211421455"><td class="cellrowborder" valign="top" width="18.44%" headers="mcps1.2.3.1.1 "><p id="p522154264510"><a name="p522154264510"></a><a name="p522154264510"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.56%" headers="mcps1.2.3.1.2 "><a name="ul12221042174518"></a><a name="ul12221042174518"></a><ul id="ul12221042174518"><li>由于灾备的细微时延不可控，业务上执行DDL时要在无业务期，且RPO&amp;RTO =0稳定30s以上在主1执行，避免在主2执行DDL（DRS只同步主1的DDL操作到主2）。</li><li>双边保持严格的对等效果，即表列行均一致（主1和主2的表结构需始终保持一致）。</li><li>在正向任务进入灾备且RPO&amp;RTO小于60s，方可启动反向任务。</li><li>双主灾备进入灾备后，请先在主2进行测试验证，符合预期后再考虑切部分业务流量到主2。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section17319599322"></a>

在使用数据复制服务进行数据灾备的过程中，对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table028935213452"></a>
<table><thead align="left"><tr id="row2028995244516"><th class="cellrowborder" valign="top" width="17.89%" id="mcps1.2.3.1.1"><p id="p17289125217457"><a name="p17289125217457"></a><a name="p17289125217457"></a><strong id="b928919524454"><a name="b928919524454"></a><a name="b928919524454"></a>类型</strong></p>
</th>
<th class="cellrowborder" valign="top" width="82.11%" id="mcps1.2.3.1.2"><p id="p18289452114510"><a name="p18289452114510"></a><a name="p18289452114510"></a><strong id="b182894527451"><a name="b182894527451"></a><a name="b182894527451"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row112891252124515"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p4289352194516"><a name="p4289352194516"></a><a name="p4289352194516"></a>数据库权限配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul172893528452"></a><a name="ul172893528452"></a><ul id="ul172893528452"><li>业务数据库帐户需要具备如下权限：SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、TRIGGER、SHOW VIEW、EVENT、INDEX、LOCK TABLES、CREATE VIEW、 CREATE ROUTINE、 ALTER ROUTINE、 CREATE USER、RELOAD、REPLICATION SLAVE、REPLICATION CLIENT、WITH GRANT OPTION。</li><li>灾备数据库帐户需要具备如下权限：SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、TRIGGER、SHOW VIEW、EVENT、INDEX、LOCK TABLES、CREATE VIEW、 CREATE ROUTINE、 ALTER ROUTINE、 CREATE USER、RELOAD、REPLICATION SLAVE、REPLICATION CLIENT、WITH GRANT OPTION。</li><li>RDS for MySQL实例的root帐户默认已具备上述权限。</li></ul>
</td>
</tr>
<tr id="row20290652154514"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p62900529458"><a name="p62900529458"></a><a name="p62900529458"></a>灾备对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul16290115244510"></a><a name="ul16290115244510"></a><ul id="ul16290115244510"><li>不支持非MyISAM和非InnoDB表的灾备。</li><li>不支持系统表。</li><li>不支持触发器和事件的灾备。</li><li>不支持对系统库下自定义对象有操作权限的帐号灾备。</li><li>不支持在主2上执行DDL的场景。</li></ul>
</td>
</tr>
<tr id="row10290115210455"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p6290165218456"><a name="p6290165218456"></a><a name="p6290165218456"></a>业务数据库配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul829014528457"></a><a name="ul829014528457"></a><ul id="ul829014528457"><li>MySQL业务数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议业务数据库binlog保存时间越长越好，建议为7天。</li><li>业务库不允许存在空账号或者空密码。</li><li>灾备中，必须设置MySQL业务数据库的server－id。如果业务数据库版本小于或等于MySQL5.6，server－id的取值范围为2~4294967296；如果业务数据库版本大于或等于MySQL5.7，server－id的取值范围为1~4294967296。</li><li>业务数据库须开启GTID。</li><li>业务数据库名称在1到64个字符之间，由小写字母、数字、中划线、下划线组成，不能包含其他特殊字符。</li><li>业务数据库中的表名、视图名不能包含：'&lt;&gt;/\以及非ASCII字符。</li><li>数据库expire_logs_days参数值为0，可能会导致灾备失败。</li></ul>
</td>
</tr>
<tr id="row9290852154516"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p329065244518"><a name="p329065244518"></a><a name="p329065244518"></a>灾备数据库配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul15290135219459"></a><a name="ul15290135219459"></a><ul id="ul15290135219459"><li>灾备数据库实例的运行状态必须正常，若数据库实例是主备实例，复制状态也必须正常。</li><li>灾备数据库实例必须有足够的磁盘空间。</li><li>主1灾备库大版本号必须与主2灾备库保持一致。</li><li>除了MySQL系统数据库之外，主2灾备库必须是空实例，且在正向任务启动后主2灾备库会被设置成只读，等待反向任务启动并进行灾备后被恢复成读写。</li></ul>
</td>
</tr>
</tbody>
</table>


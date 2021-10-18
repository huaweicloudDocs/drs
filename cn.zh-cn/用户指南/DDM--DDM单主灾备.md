# DDM-\>DDM单主灾备<a name="drs_04_0124"></a>

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

<a name="table9996155023720"></a>
<table><thead align="left"><tr id="row1199605010376"><th class="cellrowborder" valign="top" width="17.7%" id="mcps1.2.3.1.1"><p id="p399615033714"><a name="p399615033714"></a><a name="p399615033714"></a><strong id="b1599645033716"><a name="b1599645033716"></a><a name="b1599645033716"></a>类型</strong></p>
</th>
<th class="cellrowborder" valign="top" width="82.3%" id="mcps1.2.3.1.2"><p id="p18996650193712"><a name="p18996650193712"></a><a name="p18996650193712"></a><strong id="b13996150133719"><a name="b13996150133719"></a><a name="b13996150133719"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row1996650123715"><td class="cellrowborder" valign="top" width="17.7%" headers="mcps1.2.3.1.1 "><p id="p1299635083715"><a name="p1299635083715"></a><a name="p1299635083715"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="82.3%" headers="mcps1.2.3.1.2 "><a name="ul1299645063720"></a><a name="ul1299645063720"></a><ul id="ul1299645063720"><li><a href="#table17124124153819">表2</a>中的环境要求均不允许在灾备过程中修改，直至灾备结束。</li><li>业务数据库进行的参数修改不会记录在日志里，所以也不会同步至灾备数据库，请在灾备数据库升主后调整参数。</li><li>不支持业务数据库恢复到之前时间点的操作(PITR)。</li><li>不支持强制清理binlog，否则会导致灾备任务失败。</li><li>支持断点续传功能，但对于无主键的表可能会出现重复插入数据的情况。</li><li>存在灾备任务时，不允许创迁移或者同步任务。</li><li>灾备为单主灾备关系，不支持多写的多主模式，如果外部数据库没有提供superuser权限，则外部数据库为备时无法设置只读，请严格确保备节点的数据只来自主节点的同步，任何其他地方的写入将会导致备库数据被污染，使得灾备出现数据冲突而无法修复。</li><li>DDM灾备库不支持自动创建逻辑库，需要根据业务库逻辑库规则提前创建。</li><li>不支持灾备过程中新增DDM逻辑库。</li><li>不支持灾备过程中DDM逻辑库扩容(平移、翻倍)操作。</li></ul>
</td>
</tr>
<tr id="row09965505376"><td class="cellrowborder" valign="top" width="17.7%" headers="mcps1.2.3.1.1 "><p id="p2996050103713"><a name="p2996050103713"></a><a name="p2996050103713"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="82.3%" headers="mcps1.2.3.1.2 "><a name="ul18997125019373"></a><a name="ul18997125019373"></a><ul id="ul18997125019373"><li>数据灾备过程中，如果修改了业务库用于灾备的密码，会导致该灾备任务失败，需要在数据复制服务控制台将上述信息重新修改正确，然后重试任务可继续进行数据灾备。一般情况下不建议在灾备过程中修改上述信息。</li><li>数据灾备过程中，如果修改了业务库端口，会导致该灾备任务失败。一般情况下不建议在灾备过程中修改业务库端口。</li><li>数据灾备过程中，不建议做删除类型的DDL操作，可能会引起任务失败。</li><li>禁止源端在灾备任务执行主备倒换过程中进行写入操作，否则会出现数据污染或者表结构不一致，并最终导致业务端和灾备端数据不一致。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section17319599322"></a>

在使用数据复制服务进行数据灾备的过程中，对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table17124124153819"></a>
<table><thead align="left"><tr id="row61241341385"><th class="cellrowborder" valign="top" width="17.89%" id="mcps1.2.3.1.1"><p id="p11249403818"><a name="p11249403818"></a><a name="p11249403818"></a><strong id="b151252420388"><a name="b151252420388"></a><a name="b151252420388"></a>类型</strong></p>
</th>
<th class="cellrowborder" valign="top" width="82.11%" id="mcps1.2.3.1.2"><p id="p1312519419381"><a name="p1312519419381"></a><a name="p1312519419381"></a><strong id="b21254417384"><a name="b21254417384"></a><a name="b21254417384"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row7125446383"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p512524163813"><a name="p512524163813"></a><a name="p512524163813"></a>灾备对象约束</p>
<p id="p121253412387"><a name="p121253412387"></a><a name="p121253412387"></a></p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul7125749389"></a><a name="ul7125749389"></a><ul id="ul7125749389"><li>不支持非MyISAM和非InnoDB表的灾备。</li><li>不支持对系统库下自定义对象有操作权限的帐号灾备。</li><li>不支持DDM层面的账号权限灾备。</li></ul>
</td>
</tr>
<tr id="row1812584143816"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p14125142389"><a name="p14125142389"></a><a name="p14125142389"></a>业务数据库配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul148190271552"></a><a name="ul148190271552"></a><ul id="ul148190271552"><li>公网模式下，DDM和DDM绑定的RDS for MySQL实例都必须绑定EIP。</li></ul>
<a name="ul1312516419389"></a><a name="ul1312516419389"></a><ul id="ul1312516419389"><li>DDM绑定的RDS for MySQL实例的binlog日志必须打开，且binlog日志格式必须为Row格式并打开GTID。</li><li>在磁盘空间允许的情况下，建议业务数据库binlog保存时间越长越好，建议为7天。</li><li>业务数据库名称在1到64个字符之间，由小写字母、数字、中划线、下划线组成，不能包含其他特殊字符。</li><li>业务数据库中的表名不能包含：'&lt;&gt;/\以及非ASCII字符。</li></ul>
</td>
</tr>
<tr id="row41268473817"><td class="cellrowborder" valign="top" width="17.89%" headers="mcps1.2.3.1.1 "><p id="p201261243383"><a name="p201261243383"></a><a name="p201261243383"></a>灾备数据库配置</p>
</td>
<td class="cellrowborder" valign="top" width="82.11%" headers="mcps1.2.3.1.2 "><a name="ul21261412388"></a><a name="ul21261412388"></a><ul id="ul21261412388"><li>灾备数据库实例的运行状态必须正常，若数据库实例是主备实例，复制状态也必须正常</li></ul>
<a name="ul1412615463814"></a><a name="ul1412615463814"></a><ul id="ul1412615463814"><li>灾备数据库实例必须有足够的磁盘空间。</li><li>灾备DDM实例绑定的RDS需开启binlog和GTID。</li><li>灾备DDM实例与业务DDM实例绑定的RDS实例个数要保持一致。</li><li>灾备DDM实例的逻辑分片规则需要跟业务DDM的保持一致，建议使用DDM实例的逻辑库导入导出功能来保证一致性。</li></ul>
</td>
</tr>
</tbody>
</table>


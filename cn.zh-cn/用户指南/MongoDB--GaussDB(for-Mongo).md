# MongoDB-\>GaussDB\(for Mongo\)<a name="drs_04_0096"></a>

## 使用技巧（需要人为配合）<a name="section182303625619"></a>

-   如果您使用的是全量迁移模式（离线迁移），确保源和目标数据库无业务写入，保证迁移前后数据一致。

-   如果您使用的是全量+增量迁移模式（在线迁移），支持在源数据库有业务数据写入的情况下进行迁移，推荐**提前2-3天**启动任务，并配合如下使用技巧和对应场景的[操作要求](#section83714237916)，以确保顺利迁移。
    -   全量迁移

        基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行迁移任务，相对静态的数据，迁移时复杂度将会降低。

        -   全量迁移会对源数据库有一定的访问压力。
        -   迁移无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
        -   正在迁移的数据被其他事务长时间锁死，可能导致读数据超时。

    -   数据对比

        建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。



## 操作要求<a name="section83714237916"></a>

针对一些无法预知或人为因素及环境突变导致迁移失败的情况，数据复制服务提供以下常见的操作限制，供您在迁移过程中参考。

**表 1**  操作要求

<a name="table9737163714363"></a>
<table><thead align="left"><tr id="row167378370361"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p77371937113614"><a name="p77371937113614"></a><a name="p77371937113614"></a><strong id="b9737123711361"><a name="b9737123711361"></a><a name="b9737123711361"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p19737133714362"><a name="p19737133714362"></a><a name="p19737133714362"></a><strong id="b1873793717364"><a name="b1873793717364"></a><a name="b1873793717364"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row17737133713618"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p17737113773613"><a name="p17737113773613"></a><a name="p17737113773613"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul17381837143614"></a><a name="ul17381837143614"></a><ul id="ul17381837143614"><li><a href="#table122410571363">表2</a>中的环境要求均不允许在迁移过程中修改，直至迁移结束。</li><li>相互关联的数据对象要确保同时迁移，避免迁移因关联对象缺失，导致迁移失败。常见的关联关系：视图引用集合、视图引用视图等。</li><li>副本集：MongoDB数据库的副本集实例状态必须正常，要存在主节点。</li></ul>
<a name="ul17381371360"></a><a name="ul17381371360"></a><ul id="ul17381371360"><li><strong id="b14738193711366"><a name="b14738193711366"></a><a name="b14738193711366"></a>源数据库为非集群实例时，增量迁移阶段支持如下操作：</strong><a name="ul9738163783613"></a><a name="ul9738163783613"></a><ul id="ul9738163783613"><li>支持数据库（database）新建、删除。</li><li>支持文档（document）新增、删除、更新。</li><li>支持集合（collection）新建、删除。</li><li>支持索引（index）新建、删除。</li><li>支持视图（view）新建，删除。</li><li>支持convertToCapped、collMod、renameCollection命令。</li></ul>
</li><li><strong id="b473863733611"><a name="b473863733611"></a><a name="b473863733611"></a>目标库是集群实例时，包括副本到集群、集群到集群的全量+增量迁移，全量阶段和增量阶段，不能对迁移对象做创建和删除操作，否则会导致任务失败。</strong></li><li>对于在源数据库已经存在TTL索引的集合，或者在增量迁移期间在源库数据创建了TTL索引的集合，由于源数据库和目标库数据库时区，时钟的不一致，不能保证迁移完成之后数据的一致性。</li><li>如果源数据库的MongoDB服务不是单独部署的，而是和其他的服务部署在同一台机器，则必须要给源数据库的wiredTiger引擎加上cacheSizeGB的参数配置，建议值设为最小空闲内存的一半。</li><li>选择集合迁移时，增量迁移过程中不建议对集合进行重命名操作。</li><li>如果源数据库是副本集，则建议填写所有的主节点和备节点信息，以防主备切换影响迁移任务。如果填写的是主备多个节点的信息，注意所有的节点信息必须属于同一个副本集实例。</li><li>如果源数据库是集群，则建议填写多个mongos信息，以防单个mongos节点故障影响迁移任务。如果填写的是多个mongos信息，注意所有的mongos信息必须属于同一个集群。如果是集群的增量迁移任务，建议shard信息填写所有的主节点和备节点，以防主备切换影响迁移任务，并且注意所填写的主备信息必须属于同一个shard。确保填写的所有shard节点信息必须隶属于同一个集群。</li><li><span id="text8739153720363"><a name="text8739153720363"></a><a name="text8739153720363"></a>GaussDB(for Mongo)</span>集群最大可支持创建的集合数可以根据公式计算：最大chunk数*4*shard实例数。<p id="p17739153763613"><a name="p17739153763613"></a><a name="p17739153763613"></a><span id="text187391537163611"><a name="text187391537163611"></a><a name="text187391537163611"></a>GaussDB(for Mongo)</span>实例不同规格对应的最大chunk数如下：</p>
<p id="p973916373368"><a name="p973916373368"></a><a name="p973916373368"></a>1U4G-&gt;50；</p>
<p id="p157391837143611"><a name="p157391837143611"></a><a name="p157391837143611"></a>2U8G-&gt;100；</p>
<p id="p17739173783615"><a name="p17739173783615"></a><a name="p17739173783615"></a>4U16G-&gt;200；</p>
<p id="p97391137143611"><a name="p97391137143611"></a><a name="p97391137143611"></a>8U32G-&gt;400；</p>
<p id="p2739103713613"><a name="p2739103713613"></a><a name="p2739103713613"></a>16U64G-&gt;800；</p>
<p id="p1373913719364"><a name="p1373913719364"></a><a name="p1373913719364"></a>32U128G-&gt;1600。</p>
<p id="p773933763612"><a name="p773933763612"></a><a name="p773933763612"></a>请根据源库集合数情况，判断目标库是否满足要求。</p>
</li><li>非全部迁移场景下，为防止drop database操作删除目标库已有的集合，drop database不会同步到目标库。<a name="ul58210151956"></a><a name="ul58210151956"></a><ul id="ul58210151956"><li>源库是MongoDB 3.6以下版本（不含3.6）时，执行drop database会导致源库删除集合但目标库没有删除。</li><li>源库是MongoDB 3.6及以上版本（含3.6）时，drop database 操作在oplog中会体现为drop database 和drop collection操作，所以目标库也会删除相应集合，不会出现问题。</li></ul>
</li></ul>
</td>
</tr>
<tr id="row5739143716369"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1073912374369"><a name="p1073912374369"></a><a name="p1073912374369"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul137391837173614"></a><a name="ul137391837173614"></a><ul id="ul137391837173614"><li>为了保持数据一致性，在整个迁移过程中，不允许对正在迁移中的目标数据库进行修改操作(包括但不限于DDL、DML操作)。</li><li>迁移过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>在任务启动、任务全量迁移阶段，不建议对源数据库做删除类型的DDL操作，比如删除数据库、集合、索引、文档、视图等，这样可能会引起任务迁移失败。</li><li>在整个迁移过程中，不支持源数据库主备切换导致数据回滚的情况。</li><li>选择集合迁移时，增量迁移过程中不建议对集合进行重命名操作。</li><li>不支持全量迁移和增量迁移阶段insert、update源库大于16MB的文档。</li><li>为了提高迁移的速度，在开始迁移之前，建议在源数据库删掉不需要的索引，只保留必须的索引。在迁移过程中不建议对源库创建索引，如果必须要创建索引，请使用后台的方式创建索引。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section1645253517920"></a>

实时迁移对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table122410571363"></a>
<table><thead align="left"><tr id="row16224145793620"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p10224165753619"><a name="p10224165753619"></a><a name="p10224165753619"></a><strong id="b1222511573363"><a name="b1222511573363"></a><a name="b1222511573363"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p322515715368"><a name="p322515715368"></a><a name="p322515715368"></a><strong id="b822514579368"><a name="b822514579368"></a><a name="b822514579368"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row922515719363"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p18225157173616"><a name="p18225157173616"></a><a name="p18225157173616"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><p id="p2225155793618"><a name="p2225155793618"></a><a name="p2225155793618"></a>源数据库最小权限要求：</p>
<a name="ul4225195717367"></a><a name="ul4225195717367"></a><ul id="ul4225195717367"><li><strong id="b202251357103612"><a name="b202251357103612"></a><a name="b202251357103612"></a>全量迁移权限要求：</strong><a name="ul722511576367"></a><a name="ul722511576367"></a><ul id="ul722511576367"><li>副本集：连接源数据库的用户权限需要对admin数据库有readAnyDatabase权限。</li><li>集群：连接源数据库的用户权限需要对admin数据库有readAnyDatabase权限，对config数据库有read权限。</li><li>单节点：连接源数据库的用户权限需要对admin数据库有readAnyDatabase权限。</li><li>如果需要迁移源数据库用户和角色信息，连接源数据库的用户权限需要对admin数据库的系统表system.users，system.roles有读权限。</li></ul>
</li><li><strong id="b162268571369"><a name="b162268571369"></a><a name="b162268571369"></a>全量+增量迁移权限要求：</strong><a name="ul1222625716362"></a><a name="ul1222625716362"></a><ul id="ul1222625716362"><li>副本集：连接源数据库的用户权限需要对admin数据库有readAnyDatabase权限，对local数据库有read权限。</li><li>单节点：连接源数据库的用户权限需要对admin数据库有readAnyDatabase权限，对local数据库有read权限。</li><li>集群：连接源数据库mongos节点的用户权限需要对admin数据库有readAnyDatabase权限，对config数据库有read权限， 连接源数据库分片节点的用户权限需要对admin数据库有readAnyDatabase权限，对local数据库有read权限。</li><li>如果需要迁移源数据库用户和角色信息，连接源数据库的用户权限需要对admin数据库的系统表system.users，system.roles有读权限。</li></ul>
</li></ul>
<p id="p1122619570365"><a name="p1122619570365"></a><a name="p1122619570365"></a>目标数据库最小权限要求：连接目标数据库的用户权限需要对admin数据库有readAnyDatabase权限，对目标数据库有readWrite权限。</p>
</td>
</tr>
<tr id="row1922675783616"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p18226105715368"><a name="p18226105715368"></a><a name="p18226105715368"></a>迁移对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul182271057143612"></a><a name="ul182271057143612"></a><ul id="ul182271057143612"><li>副本集：目前只支持集合(包括验证器，是否是固定集合)，索引和视图的迁移。</li><li>集群：目前只支持集合（包括验证器，是否是固定集合），分片键，索引和视图的迁移。</li><li>单节点：目前只支持集合（包括验证器，是否是固定集合），索引和视图的迁移。</li><li>不支持_id字段没有索引的集合。</li><li>不支持BinData()的第一个参数为2。</li></ul>
</td>
</tr>
<tr id="row122271857193614"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p82271573369"><a name="p82271573369"></a><a name="p82271573369"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul192271657173611"></a><a name="ul192271657173611"></a><ul id="ul192271657173611"><li>不支持源数据库的库名、集合名或视图名中包含如下字符：'&lt;&gt;.。</li><li>如果迁移任务是源数据集群的增量，则源数据必须关闭Balancer。</li><li>源数据库不能是<span id="text13228155715361"><a name="text13228155715361"></a><a name="text13228155715361"></a>GaussDB(for Mongo)</span>实例。</li></ul>
</td>
</tr>
<tr id="row1122812579362"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p52281557143618"><a name="p52281557143618"></a><a name="p52281557143618"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul6228757193611"></a><a name="ul6228757193611"></a><ul id="ul6228757193611"><li>目标数据库实例的运行状态必须正常。</li><li>目标数据库实例必须有足够的磁盘空间。</li><li>多个源数据库迁移到同一个目标数据库时，所选的待迁移数据库的库名不能重复。</li><li>集群到集群的全量迁移，如果源数据库的集群没有开启分片，则需要保证目标数据库主shard节点的磁盘空间大于源数据库数据大小。</li><li>目前不支持从高版本数据库到低版本数据库的迁移。</li></ul>
</td>
</tr>
</tbody>
</table>


# Oracle-\>GaussDB\(DWS\)<a name="drs_04_0114"></a>

## 使用技巧（需要人为配合）<a name="section449714073815"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1691943218231)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。
    -   同步无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section1691943218231"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table10347155094512"></a>
<table><thead align="left"><tr id="row1034755011456"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p2347195018450"><a name="p2347195018450"></a><a name="p2347195018450"></a><strong id="b14347135011457"><a name="b14347135011457"></a><a name="b14347135011457"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p113485508459"><a name="p113485508459"></a><a name="p113485508459"></a><strong id="b1934815017452"><a name="b1934815017452"></a><a name="b1934815017452"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row9348165034512"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p13348950194518"><a name="p13348950194518"></a><a name="p13348950194518"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul14348150184518"></a><a name="ul14348150184518"></a><ul id="ul14348150184518"><li><a href="#table119358174618">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li></ul>
<a name="ul113481950184519"></a><a name="ul113481950184519"></a><ul id="ul113481950184519"><li>相互关联的数据对象要确保同时同步，避免因关联对象缺失，导致同步失败。</li><li>表等对象名同步到目标库后会转换成小写，如ABC会转换为abc。因此增量同步阶段，选择的源库的表中不能存在仅大小写不同的表，可能会导致同步失败。</li><li>如有中文、日文等特殊字符，业务连接Oracle数据库使用的编码需和Oracle数据库服务端编码一致，否则目标库可能会出现乱码。</li><li>由于无主键表缺乏行的唯一性标志，网络不稳定时涉及少量重试，表数据存在少量不一致的可能性。</li><li>Oracle中表结构长度（所有列长字节数之和，char、varchar2等类型字节长度和编码有关）超过65535时，可能导致同步失败。</li><li>源库为Oracle RAC环境时，如果需要使用scanip，需要保证scanip与源库的所有vip互通，否则无法通过连接检查。若不使用scanip，可以使用某一节点的vip，其他节点异常不影响同步。</li><li>对于Oracle RAC集群，建议使用scanip+ servicename方式创建任务，scanip具有更强的容错性，更好的负载能力，更快的同步体验。</li><li>索引同步只同步普通索引，主键等约束在表结构中进行同步。</li><li>增量同步时，BLOB末尾的0x00、CLOB末尾的空格会被截断。</li><li>当Oracle字符集是WE8MSWIN1252时，CLOB列同步到目标库可能出现乱码，建议先修改源库字符集为AL32UTF8再同步数据。</li></ul>
</td>
</tr>
<tr id="row103491750124516"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1834945054519"><a name="p1834945054519"></a><a name="p1834945054519"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul123495509459"></a><a name="ul123495509459"></a><ul id="ul123495509459"><li>同步程中，不允许删除连接源和目标数据库的用户的用户名、密码、权限，或修改目标数据库的端口号。</li><li>选择表级对象同步时，增量同步过程中不建议对表进行重命名操作。</li><li>库级映射和表级映射均不区分大小写，例如映射为abc与映射为ABC，同步到目标库后均为abc。</li><li>任务再编辑增加新表时，请确保新增的表的事务都已提交，否则未提交的事务可能无法同步到目标库。建议在业务低峰期做增加表的操作。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section86695405239"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table119358174618"></a>
<table><thead align="left"><tr id="row6935131174618"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p59361715465"><a name="p59361715465"></a><a name="p59361715465"></a><strong id="b59361418463"><a name="b59361418463"></a><a name="b59361418463"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p19361518466"><a name="p19361518466"></a><a name="p19361518466"></a><strong id="b13936171174618"><a name="b13936171174618"></a><a name="b13936171174618"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row693610164610"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p8936215466"><a name="p8936215466"></a><a name="p8936215466"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1893613134613"></a><a name="ul1893613134613"></a><ul id="ul1893613134613"><li>源数据库端：<a name="ul975014120564"></a><a name="ul975014120564"></a><ul id="ul975014120564"><li>需要具有CREATE SESSION、SELECT ANY TRANSACTION、SELECT ANY TABLE、SELECT ANY DICTIONARY权限和EXECUTE_CATALOG_ROLE角色，若Oracle为12C及以上版本还需要LOGMINING权限。</li><li>12c 以上版本 PDB 数据库同步时，需要为用户赋予如下权限：<p id="p1967452219333"><a name="p1967452219333"></a><a name="p1967452219333"></a>在CDB下创建C##前缀的容器数据库用户赋予CREATE SESSION、SELECT ANY DICTIONARY、SELECT ANY TABLE、LOGMINING、EXECUTE_CATALOG_ROLE权限和SET CONTAINER权限（GRANT&nbsp;SET&nbsp;CONTAINER&nbsp;TO&nbsp;C##USERNAME&nbsp;CONTAINER=&nbsp;ALL;）。</p>
<p id="p721274311526"><a name="p721274311526"></a><a name="p721274311526"></a>在PDB下为C##前缀用户赋予以下权限（其中RESTRICTED SESSION、SELECT ON SYS.COL$、 SELECT ON SYS.OBJ$权限需要单独赋予）：RESTRICTED SESSION、CREATE SESSION、SELECT ANY DICTIONARY、EXECUTE_CATALOG_ROLE、SELECT ANY TRANSACTION、SELECT ANY TABLE、LOGMINING、SELECT ON SYS.COL$、SELECT ON SYS.OBJ$。</p>
</li></ul>
</li><li>目标数据库帐号必须具有每张表的如下权限：INSERT、SELECT、UPDATE、DELETE、CONNECT、CREATE、REFERENCES。</li></ul>
</td>
</tr>
<tr id="row189361711463"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p593620124619"><a name="p593620124619"></a><a name="p593620124619"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1993711124614"></a><a name="ul1993711124614"></a><ul id="ul1993711124614"><li>支持表、索引、约束（主键、空、非空）的同步，不支持视图、外键、存储过程、触发器、函数、事件、虚拟列的同步。</li><li>不支持的数据类型有：xml、geometry、point、lineString、polygon、geometrycollection、multipoint、multilinestring、multipolygon。</li><li>对于TIMESTAMP WITH TIME ZONE类型，根据目标库时区做转换后不得大于“9999-12-31 23:59:59.999999”。</li><li>源库支持to_date和sys_guid函数做默认值。将函数作为default值时，需要目标库也有相同功能的函数。对于目标库不存在对应函数的情况，默认值函数可能会被置空。</li><li>不支持默认值含有表达式的函数的表的同步。</li><li>不支持同步源库中的临时表。</li></ul>
</td>
</tr>
<tr id="row693781174617"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p593731164611"><a name="p593731164611"></a><a name="p593731164611"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul17937161194620"></a><a name="ul17937161194620"></a><ul id="ul17937161194620"><li>库名、表名不支持的字符有：非ASCII字符、“. ”、 “&gt;”、 “&lt;”、 “\”、 “`”、 “|”、 “,”、 “? ”、 “! ”、 “"”和 “'”。</li><li>同步过程中，要求源数据库打开归档日志。</li><li>源数据库不允许含有空库。</li></ul>
</td>
</tr>
<tr id="row693718115462"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p593813113461"><a name="p593813113461"></a><a name="p593813113461"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1938141184615"></a><a name="ul1938141184615"></a><ul id="ul1938141184615"><li>目标数据库实例的运行状态必须正常。</li><li>目标数据库实例必须有足够的磁盘空间。</li><li>增量同步的表要禁用外键，因为DRS并行回放会使得不同表之间的写入顺序和源库不一致，可能会触发外键约束限制，造成同步失败。</li></ul>
</td>
</tr>
</tbody>
</table>


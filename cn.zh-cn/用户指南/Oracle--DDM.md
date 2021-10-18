# Oracle-\>DDM<a name="drs_04_0112"></a>

## 使用技巧（需要人为配合）<a name="section449714073815"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1610153915412)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section1610153915412"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table88398497411"></a>
<table><thead align="left"><tr id="row16839184994117"><th class="cellrowborder" valign="top" width="18.3%" id="mcps1.2.3.1.1"><p id="p108399495417"><a name="p108399495417"></a><a name="p108399495417"></a><strong id="b1383911493411"><a name="b1383911493411"></a><a name="b1383911493411"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.69999999999999%" id="mcps1.2.3.1.2"><p id="p883954934110"><a name="p883954934110"></a><a name="p883954934110"></a><strong id="b783934916419"><a name="b783934916419"></a><a name="b783934916419"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row784064912419"><td class="cellrowborder" valign="top" width="18.3%" headers="mcps1.2.3.1.1 "><p id="p18840184912417"><a name="p18840184912417"></a><a name="p18840184912417"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.69999999999999%" headers="mcps1.2.3.1.2 "><a name="ul38401049204120"></a><a name="ul38401049204120"></a><ul id="ul38401049204120"><li><a href="#table17842174974118">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>表对象名同步到目标库后会转换成小写，如ABC和abc。因此增量同步阶段，选择的源库表中不能存在表名称字母相同但大小写不同的表，否则，会导致同步失败。</li><li>如有中文、日文等特殊字符，业务连接Oracle数据库使用的编码需和Oracle数据库服务端编码一致，否则目标库会出现乱码。</li><li>Oracle中表结构同步到DDM后表的字符集为utf8mb4。</li><li>由于无主键表缺乏行的唯一性标志，网络不稳定时涉及少量重试，表数据存在少量不一致的可能性。</li><li>Oracle中表结构长度（所有列长字节数之和，char、varchar2等类型字节长度和编码有关）超过65535时，可能导致同步失败。</li><li>源库为Oracle RAC环境时，如果需要使用scanip，需要保证scanip与源库的所有vip互通，否则无法通过连接检查。若不使用scanip，可以使用某一节点的vip，其他节点异常不影响同步。</li><li>对于Oracle RAC集群，建议使用scanip+ servicename方式创建任务，scanip具有更强的容错性，更好的负载能力，更快的同步体验。</li><li>数据类型不兼容时，可能引起同步失败。</li><li>增量同步时，BLOB末尾的0x00、CLOB末尾的空格会被截断。</li><li>当Oracle字符集是WE8MSWIN1252时，CLOB列同步到目标库可能出现乱码，建议先修改源库字符集为AL32UTF8再同步数据。</li></ul>
</td>
</tr>
<tr id="row78418491414"><td class="cellrowborder" valign="top" width="18.3%" headers="mcps1.2.3.1.1 "><p id="p8841124916413"><a name="p8841124916413"></a><a name="p8841124916413"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.69999999999999%" headers="mcps1.2.3.1.2 "><a name="ul084119498416"></a><a name="ul084119498416"></a><ul id="ul084119498416"><li>对于同步中的数据库对象，在同步期间，目标库不能进行写入操作，否则会导致数据不一致。</li><li>同步过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>同步过程中，源库不能做DDL变更。</li><li>选择表级对象同步时，增量同步过程中不建议对表进行重命名操作。</li><li>源库的用户对应目标库的数据库。</li><li>源库用户、表结构信息同步至目标库后全部转换为小写。如表Ab及表AB同步至目标库为ab。</li><li>不支持索引组织表的同步。</li><li>同步任务全量阶段开始前，如有长时间未提交的事务，有可能丢失数据。</li><li>任务再编辑增加新表时，请确保新增的表的事务都已提交，否则未提交的事务可能无法同步到目标库。建议在业务低峰期做增加表的操作。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section165311339195419"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table17842174974118"></a>
<table><thead align="left"><tr id="row1842144914117"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p784244917415"><a name="p784244917415"></a><a name="p784244917415"></a><strong id="b1684234912417"><a name="b1684234912417"></a><a name="b1684234912417"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p198421149144113"><a name="p198421149144113"></a><a name="p198421149144113"></a><strong id="b9842249114111"><a name="b9842249114111"></a><a name="b9842249114111"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row1284213494413"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p8843104944113"><a name="p8843104944113"></a><a name="p8843104944113"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul14843849134113"></a><a name="ul14843849134113"></a><ul id="ul14843849134113"><li>源数据库端：<a name="ul10114111002010"></a><a name="ul10114111002010"></a><ul id="ul10114111002010"><li>全量+增量同步时需要具有CREATE SESSION、SELECT ANY DICTIONARY、EXECUTE_CATALOG_ROLE、SELECT ANY TRANSACTION权限和SELECT ANY TABLE权限，若Oracle为12c及以上版本还需要LOGMINING权限。全量同步时需要具有CREATE SESSION、SELECT ANY DICTIONARY、SELECT ANY TABLE和FLASHBACK ANY TABLE权限。</li><li>12c 以上版本 PDB 数据库同步时，需要为用户赋予如下权限：<p id="p35231981356"><a name="p35231981356"></a><a name="p35231981356"></a>在CDB下创建C##前缀的容器数据库用户赋予CREATE SESSION、SELECT ANY DICTIONARY、SELECT ANY TABLE、LOGMINING、EXECUTE_CATALOG_ROLE权限和SET CONTAINER权限（GRANT&nbsp;SET&nbsp;CONTAINER&nbsp;TO&nbsp;C##USERNAME&nbsp;CONTAINER=&nbsp;ALL;）。</p>
<p id="p205231982058"><a name="p205231982058"></a><a name="p205231982058"></a>在PDB下为C##前缀用户赋予以下权限（其中RESTRICTED SESSION、SELECT ON SYS.COL$、 SELECT ON SYS.OBJ$权限需要单独赋予）：</p>
<p id="p11808629123117"><a name="p11808629123117"></a><a name="p11808629123117"></a>全量+增量同步时需要具有RESTRICTED SESSION、CREATE SESSION、SELECT ANY DICTIONARY、EXECUTE_CATALOG_ROLE、SELECT ANY TRANSACTION、SELECT ANY TABLE、LOGMINING、SELECT ON SYS.COL$、SELECT ON SYS.OBJ$。全量同步时需要具有RESTRICTED SESSION、CREATE SESSION、SELECT ANY DICTIONARY、SELECT ANY TABLE、FLASHBACK ANY TABLE、SELECT ON SYS.COL$、SELECT ON SYS.OBJ$。</p>
</li></ul>
</li><li>目标数据库端：提供的目标数据库帐号必须拥有如下权限：SELECT、CREATE、DROP、DELETE、INSERT、UPDATE、ALTER、INDEX、EVENT、RELOAD、CREATE VIEW。</li></ul>
</td>
</tr>
<tr id="row6843849164115"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1184316497413"><a name="p1184316497413"></a><a name="p1184316497413"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1284316497419"></a><a name="ul1284316497419"></a><ul id="ul1284316497419"><li>增量同步不支持DDL的同步。</li><li>全量阶段不支持bfile，xml、sdo_geometry、urowid和自定义类型。</li><li>增量阶段不支持bfile，xml、interval、sdo_geometry、urowid和自定义类型。</li><li>目前只支持同步源库的数据，不支持同步源库表结构及其他数据库对象。</li><li>用户需要在目标库根据源端逻辑库的表结构，自行在目标库创建对应的表结构及索引。未在目标库创建的对象，视为用户不选择这个对象进行同步。</li><li>源库在目标库创建的表结构， 必须与源库的表结构完全一致 。</li><li>源库支持to_date和sys_guid函数做默认值。将函数作为default值时，需要目标库也有相同功能的函数。对于目标库不存在对应函数的情况，默认值函数可能会被置空。</li><li>不支持默认值含有表达式的函数的表的同步。</li><li>不支持同步源库中的临时表。</li></ul>
</td>
</tr>
<tr id="row684394919410"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p7843164914110"><a name="p7843164914110"></a><a name="p7843164914110"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul28432492419"></a><a name="ul28432492419"></a><ul id="ul28432492419"><li>Oracle单行记录不能超过8KB（text、blob部分计算），原因是MySQL innoDB引擎限制单行大小不能超过8KB。</li><li>不建议以字符串类型作为主键或唯一键，因为Oracle的字符串作为主键、唯一键时区分空格，而MySQL不区分，可能导致数据不一致和死锁问题。</li><li>binary_float或者binary_double类型不支持设置Nan、Inf、-Inf三个值，因为MySQL不支持</li><li>Oracle中建议列名不要取名AUTO_PK_ROW_ID，原因是这个列名在MySQL5.7中是保留列名，无法创建出来。</li><li>Oracle中number(p, s)字段的精度不要超过p: [1, 38], s:[p-65, min(p, 30)]的精度表示范围。其中，s取值依赖于p的取值变化，即下限为p-65, 上限为p或30中取最小值。例如：当p=1, s的取值范围是[-64, 1]。当p=38, s取值范围是[-27, 30]。<p id="p11704172118710"><a name="p11704172118710"></a><a name="p11704172118710"></a>int字段的值不要超过（65，0）的精度表示范围。原因是MySQL数字的表示范围比Oracle小。</p>
</li><li>不支持表名包含除下划线外的其他特殊字符的表的同步。</li><li>源数据库中的库名不允许为ib_logfile。</li><li>增量同步时，要求源数据库打开归档日志。</li><li>源数据库不允许含有空库。</li></ul>
</td>
</tr>
<tr id="row6845114920419"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1784518499415"><a name="p1784518499415"></a><a name="p1784518499415"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul12845124919410"></a><a name="ul12845124919410"></a><ul id="ul12845124919410"><li>同步前，目标数据库必须存在待同步数据库及表，且库名，表名，列名，索引名、约束名等必须为对应的小写名称。</li><li>用户在目标库自建的表结构时，请确认不要使用不区分大小写（_ci结尾）的排序字符集（Collation）。</li><li>DRS同步时会有大量数据写入目标库，目标库max_allowed_packet 参数过小会导致无法写入，建议将目标库max_allowed_packet参数值设置为大于100MB。</li><li>增量同步的表要禁用外键，因为DRS并行回放会使得不同表之间的写入顺序和源库不一致，可能会触发外键约束限制，造成同步失败。</li></ul>
</td>
</tr>
</tbody>
</table>


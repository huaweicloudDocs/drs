# Oracle-\>GaussDB\(for MySQL\)主备版<a name="drs_04_0110"></a>

## 使用技巧（需要人为配合）<a name="section98341051155812"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1691943218231)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。
    -   同步无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section1691943218231"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table19550111913304"></a>
<table><thead align="left"><tr id="row95501119163012"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p955161913303"><a name="p955161913303"></a><a name="p955161913303"></a><strong id="b11551201912309"><a name="b11551201912309"></a><a name="b11551201912309"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p35511419123012"><a name="p35511419123012"></a><a name="p35511419123012"></a><strong id="b8551319113018"><a name="b8551319113018"></a><a name="b8551319113018"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row1455131912302"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p055114191305"><a name="p055114191305"></a><a name="p055114191305"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1855131916307"></a><a name="ul1855131916307"></a><ul id="ul1855131916307"><li><a href="#table13321027153010">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>相互关联的数据对象要确保同时同步，避免因关联对象缺失，导致同步失败。常见的关联关系：主外键关联表等。</li><li>表等对象名同步到目标库后会转换成小写，如ABC和abc。因此增量同步阶段，选择的源库的表中不能存在仅大小写不同的表，否则，会导致同步失败。</li><li>源库和目标库时区设置必须一致。</li><li>如有中文、日文等特殊字符，业务连接Oracle数据库使用的编码需和Oracle数据库服务端编码一致，否则目标库会出现乱码。</li><li>Oracle中表结构同步到MySQL后表的字符集为UTF8MB4。</li><li>由于无主键表缺乏行的唯一性标志，网络不稳定时涉及少量重试，表数据存在少量不一致的可能性。</li><li>Oracle中表结构长度（所有列长字节数之和，char、varchar2等类型字节长度和编码有关）超过65535时，可能导致同步失败。</li><li>源库为Oracle RAC环境时，如果需要使用scanip，需要保证scanip与源库的所有vip互通，否则无法通过连接检查。若不使用scanip，可以使用某一节点的vip，其他节点异常不影响同步。</li><li>对于Oracle RAC集群，建议使用scanip+ servicename方式创建任务，scanip具有更强的容错性，更好的负载能力，更快的同步体验。</li><li>数据类型不兼容时，可能引起同步失败。</li><li>增量同步时，BLOB末尾的0x00、CLOB末尾的空格会被截断。</li><li>当Oracle字符集是WE8MSWIN1252时，CLOB列同步到目标库可能出现乱码，建议先修改源库字符集为AL32UTF8再同步数据。</li></ul>
</td>
</tr>
<tr id="row1855114193303"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p135511919193015"><a name="p135511919193015"></a><a name="p135511919193015"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul3551171912307"></a><a name="ul3551171912307"></a><ul id="ul3551171912307"><li>对于同步中的数据库对象，在同步期间，目标库不能进行写入操作，否则会导致数据不一致。</li><li>同步过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>增量同步过程中，支持部分DDL操作。<a name="ul182043364312"></a><a name="ul182043364312"></a><ul id="ul182043364312"><li>表级同步支持alter&nbsp;table&nbsp;add&nbsp;column、alter&nbsp;table&nbsp;drop&nbsp;column、alter&nbsp;table&nbsp;rename&nbsp;column、alter&nbsp;table&nbsp;modify&nbsp;column以及truncate&nbsp;table的基本DDL，不支持默认值等的修改。</li></ul>
</li><li>增量DDL不支持全角、中文等特殊字符。</li><li>库级映射和表级映射均不区分大小写，例如映射为abc与映射为ABC，同步到目标库后均为abc。</li><li>任务再编辑增加新表时，请确保新增的表的事务都已提交，否则未提交的事务可能无法同步到目标库。建议在业务低峰期做增加表的操作。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section86695405239"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table13321027153010"></a>
<table><thead align="left"><tr id="row14332172743018"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p1332122733017"><a name="p1332122733017"></a><a name="p1332122733017"></a><strong id="b1333210279303"><a name="b1333210279303"></a><a name="b1333210279303"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p833272783019"><a name="p833272783019"></a><a name="p833272783019"></a><strong id="b1133242783015"><a name="b1133242783015"></a><a name="b1133242783015"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row1533262713014"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p33321727203011"><a name="p33321727203011"></a><a name="p33321727203011"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul833342793015"></a><a name="ul833342793015"></a><ul id="ul833342793015"><li>源数据库端：<a name="ul975014120564"></a><a name="ul975014120564"></a><ul id="ul975014120564"><li>需要具有CREATE SESSION、SELECT ANY TRANSACTION、SELECT ANY TABLE、SELECT ANY DICTIONARY权限和EXECUTE_CATALOG_ROLE角色，若Oracle为12C及以上版本还需要LOGMINING权限。</li><li>12c 以上版本 PDB 数据库同步时，需要为用户赋予如下权限：<p id="p1967452219333"><a name="p1967452219333"></a><a name="p1967452219333"></a>在CDB下创建C##前缀的容器数据库用户赋予CREATE SESSION、SELECT ANY DICTIONARY、SELECT ANY TABLE、LOGMINING、EXECUTE_CATALOG_ROLE权限和SET CONTAINER权限（GRANT&nbsp;SET&nbsp;CONTAINER&nbsp;TO&nbsp;C##USERNAME&nbsp;CONTAINER=&nbsp;ALL;）。</p>
<p id="p721274311526"><a name="p721274311526"></a><a name="p721274311526"></a>在PDB下为C##前缀用户赋予以下权限（其中RESTRICTED SESSION、SELECT ON SYS.COL$、 SELECT ON SYS.OBJ$权限需要单独赋予）：RESTRICTED SESSION、CREATE SESSION、SELECT ANY DICTIONARY、EXECUTE_CATALOG_ROLE、SELECT ANY TRANSACTION、SELECT ANY TABLE、LOGMINING、SELECT ON SYS.COL$、SELECT ON SYS.OBJ$。</p>
</li></ul>
</li><li>目标数据库端：提供的目标数据库帐号必须拥有如下权限：SELECT、INSERT、CREATE、DROP、UPDATE、ALTER、DELETE、INDEX。</li></ul>
</td>
</tr>
<tr id="row53331227143014"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1633392711307"><a name="p1633392711307"></a><a name="p1633392711307"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul8333227113011"></a><a name="ul8333227113011"></a><ul id="ul8333227113011"><li>支持库、表结构、主键、唯一键、普通索引、表数据的同步，其他数据库对象暂不支持，如存储过程、触发器、函数、序列、包、同义词、用户等。</li><li>全量阶段不支持bfile，xml、sdo_geometry、urowid和自定义类型。</li><li>增量阶段不支持bfile，xml、interval、sdo_geometry、urowid和自定义类型。</li><li>源库支持to_date和sys_guid函数做默认值。将函数作为default值时，需要目标库也有相同功能的函数。对于目标库不存在对应函数的情况，默认值函数可能会被置空。</li><li>不支持默认值含有表达式的函数的表的同步。</li><li>不支持同步源库中的临时表。</li></ul>
</td>
</tr>
<tr id="row1633362753018"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p20333162763017"><a name="p20333162763017"></a><a name="p20333162763017"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul8333327123019"></a><a name="ul8333327123019"></a><ul id="ul8333327123019"><li>Oracle单行记录不能超过8K（text、blob部分计算），原因是MySQL innodb引擎限制单行大小不能超过8K。</li><li>不建议以字符串类型作为主键或唯一键，因为Oracle的字符串作为主键、唯一键时区分空格，而MySQL不区分，可能导致数据不一致和死锁问题。</li><li>binary_float或者binary_double类型不支持设置Nan、Inf、-Inf三个值，因为MySQL不支持。</li><li>Oracle的check约束同步到MySQL会失效，原因是MySQL不支持check约束。</li><li>Oracle中建议列名不要取名AUTO_PK_ROW_ID，原因是这个列名在MySQL5.7中是保留列名，无法创建出来。</li><li>Oracle中number(p, s)字段的精度不要超过p: [1, 38], s:[p-65, min(p, 30)]的精度表示范围。其中，s取值依赖于p的取值变化，即下限为p-65, 上限为p或30中取最小值。例如：当p=1, s的取值范围是[-64, 1]。当p=38, s取值范围是[-27, 30]。<p id="p113331327113019"><a name="p113331327113019"></a><a name="p113331327113019"></a>int字段的值不要超过（65，0）的精度表示范围。原因是MySQL数字的表示范围比Oracle小。</p>
</li><li>库名、表名不支持的字符有：非ASCII字符、“. ”、 “&gt;”、 “&lt;”、 “\”、 “`”、 “|”、 “,”、 “? ”、 “! ”、 “"”和 “'”。</li><li>源数据库中的库名不允许为ib_logfile。</li><li>Oracle到<span id="text14334102733017"><a name="text14334102733017"></a><a name="text14334102733017"></a>GaussDB(for MySQL)</span>的全量+增量同步，要求源数据库打开归档日志。</li><li>源数据库不允许含有空库。</li><li>源数据库不允许存在索引列的长度之和超过目标库索引列长度限制的索引，具体长度要求请参见<a href="https://support.huaweicloud.com/drs_faq/drs_04_0022.html" target="_blank" rel="noopener noreferrer">索引长度说明</a>。</li><li>默认值不支持default user，MySQL没有对应的语法。</li><li>目前仅支持如下字符集：ZHS16GBK、AL32UTF8、UTF8、US7ASCII、WE8MSWIN1252。</li><li>附加日志级别为all或者pk + ui。</li><li>源库为RAC时，不支持增加、减少节点数量。</li><li>源库为RAC时，如果需要使用scanip，需要drs node能够连接全部节点的vip，否则无法通过连接检查。</li></ul>
</td>
</tr>
<tr id="row7335027183010"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p3335152703019"><a name="p3335152703019"></a><a name="p3335152703019"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1433516276303"></a><a name="ul1433516276303"></a><ul id="ul1433516276303"><li>目标数据库不能存在待同步数据库。</li><li>用户在目标库自建的表结构时请确认不要使用不区分大小写（_ci结尾）的排序字符集（Collation）。</li><li>DRS同步时会有大量数据写入目标库，目标库max_allowed_packet 参数过小会导致无法写入，建议将目标库max_allowed_packet参数值设置为大于100MB。</li><li>增量同步的表要禁用外键，因为DRS并行回放会使得不同表之间的写入顺序和源库不一致，可能会触发外键约束限制，造成同步失败。</li></ul>
</td>
</tr>
</tbody>
</table>


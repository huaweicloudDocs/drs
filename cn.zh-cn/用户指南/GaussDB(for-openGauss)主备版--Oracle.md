# GaussDB\(for openGauss\)主备版-\>Oracle<a name="drs_11_0435"></a>

## 操作要求<a name="section1610153915412"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table1583011417373"></a>
<table><thead align="left"><tr id="row98309413719"><th class="cellrowborder" valign="top" width="18.18%" id="mcps1.2.3.1.1"><p id="p783118463714"><a name="p783118463714"></a><a name="p783118463714"></a><strong id="b08311947379"><a name="b08311947379"></a><a name="b08311947379"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.82000000000001%" id="mcps1.2.3.1.2"><p id="p1283117483717"><a name="p1283117483717"></a><a name="p1283117483717"></a><strong id="b783110413376"><a name="b783110413376"></a><a name="b783110413376"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row168311041373"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p78311049379"><a name="p78311049379"></a><a name="p78311049379"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul3831134133714"></a><a name="ul3831134133714"></a><ul id="ul3831134133714"><li><a href="#table16834134203715">表 环境要求</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>该链路不支持SSL安全连接。</li><li>不建议在数据库中使用非精确数值类型做主键，该特性影响 DRS 增量场景下对 UPDATE、DELETE语句的同步，同时也会导致内容比对不可用。主键支持的类型可参考<a href="https://support.huaweicloud.com/productdesc-drs/drs_08_0002.html#section6" target="_blank" rel="noopener noreferrer">Oracle数据库-&gt;GaussDB(for openGauss)数据库映射关系</a>。</li><li>一个同步任务只能对一个数据库进行数据同步，如果一个GaussDB(for openGauss)实例下有多个数据库需要同步，则需要为每个数据库创建实时同步任务。</li></ul>
</td>
</tr>
<tr id="row17832442377"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p6832154143713"><a name="p6832154143713"></a><a name="p6832154143713"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul11177172432116"></a><a name="ul11177172432116"></a><ul id="ul11177172432116"><li>一般情况下，此链路为Oracle到<span id="text2017722472111"><a name="text2017722472111"></a><a name="text2017722472111"></a>GaussDB(for openGauss)</span>主备版同步链路的反向逃生链路，并与Oracle到<span id="text19177102412217"><a name="text19177102412217"></a><a name="text19177102412217"></a>GaussDB(for openGauss)</span>主备版同步链路配合使用，不建议单独使用此链路做其他场景的数据同步。</li><li>表等对象名同步到目标库后会转换成大写。因此全量和增量同步阶段，选择的源库表中不能存在表名称字母相同但大小写不同的表，否则，会导致同步失败。如果此链路作为Oracle到<span id="text122261578125"><a name="text122261578125"></a><a name="text122261578125"></a>GaussDB(for openGauss)</span>主备版的逃生链路使用，建议仅同步Oracle端为大写的schema名和表名，且<span id="text6335185851211"><a name="text6335185851211"></a><a name="text6335185851211"></a>GaussDB(for openGauss)</span>主备版端为小写的schema名和表名。</li><li>实时同步过程中，受限于<span id="text182871159225"><a name="text182871159225"></a><a name="text182871159225"></a>GaussDB(for openGauss)</span>逻辑复制功能，不支持DDL语句的同步。一般情况下，不建议同步过程中进行DDL操作。</li><li>实时同步过程中，修改源库的用户名、密码、IP和端口，可能会导致同步任务失败。</li></ul>
<a name="ul178332415376"></a><a name="ul178332415376"></a><ul id="ul178332415376"><li>对于全量同步中的目标数据库表对象，不能进行写入操作，否则会导致数据不一致。</li><li>增量同步中，需保持源库和目标库表的主键列一致。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section165311339195419"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table16834134203715"></a>
<table><thead align="left"><tr id="row1283494123712"><th class="cellrowborder" valign="top" width="18.18%" id="mcps1.2.3.1.1"><p id="p188351841371"><a name="p188351841371"></a><a name="p188351841371"></a><strong id="b483514123718"><a name="b483514123718"></a><a name="b483514123718"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.82000000000001%" id="mcps1.2.3.1.2"><p id="p083515423713"><a name="p083515423713"></a><a name="p083515423713"></a><strong id="b9835441376"><a name="b9835441376"></a><a name="b9835441376"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row1383511483717"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p12835204143712"><a name="p12835204143712"></a><a name="p12835204143712"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul115444197331"></a><a name="ul115444197331"></a><ul id="ul115444197331"><li>源数据库端需要同时拥有以下权限：<a name="ul141507123018"></a><a name="ul141507123018"></a><ul id="ul141507123018"><li>库级权限：需要使用root或其他有Sysadmin角色的DATABASE用户登录postgres基库，赋予用户DATABASE的CONNECT权限以及REPLICATION权限。</li><li>SCHEMA级权限：需要使用 root、或其他有Sysadmin角色的DATABASE用户、或目标数据库的OWNER用户登入目标数据库，赋予用户SCHEMA的USAGE权限。</li><li>表级权限：需要使用 root、或其他有Sysadmin角色的DATABASE用户、或目标数据库的OWNER用户登入目标数据库 ，赋予用户SCHEMA下所有表的SELECT权限。</li></ul>
</li><li>目标库账户需要同时拥有以下角色或权限：<a name="ul18797164693115"></a><a name="ul18797164693115"></a><ul id="ul18797164693115"><li>拥有DATABASE或表的SELECT、INSERT、UPDATE、DELETE权限。</li><li>拥有SCHEMA的RESOURCE权限。</li></ul>
</li></ul>
</td>
</tr>
<tr id="row183614416375"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p1983624103710"><a name="p1983624103710"></a><a name="p1983624103710"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul1614210181446"></a><a name="ul1614210181446"></a><ul id="ul1614210181446"><li>不支持无主键表的同步。</li><li>支持的数据类型有BIGINT，BIT，BIT VARYING，BLOB，BOOLEAN，BYTEA，CHARACTER，CHARACTER VARYING，CLOB，DATE，DOUBLE PRECISION，INTEGER，MONEY，NUMBER，NUMERIC，NVARCHAR2，RAW，REAL，SMALLDATETIME，SMALLINT，TEXT，TIME WITH TIME ZONE，TIME WITHOUT TIME ZONE，TIMESTAMP WITH TIME ZONE，TIMESTAMP WITHOUT TIME ZONE，TINYINT。</li><li>全量同步时仅支持表数据、表结构和索引约束的同步。</li><li>增量同步不支持列存表、压缩表、非日志表、临时表数据同步。</li></ul>
</td>
</tr>
<tr id="row983716423713"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p18378413377"><a name="p18378413377"></a><a name="p18378413377"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul198371347377"></a><a name="ul198371347377"></a><ul id="ul198371347377"><li>增量同步时<span id="text714511371317"><a name="text714511371317"></a><a name="text714511371317"></a>GaussDB(for openGauss)</span>源数据库日志模式(wal_level)必须为logical。</li><li>全量和增量同步时源数据库中的库名和表名不能包含：+%"&lt;&gt;'\以及非ASCII字符。</li><li>源库必须是本云<span id="text31376581319"><a name="text31376581319"></a><a name="text31376581319"></a>GaussDB(for openGauss)</span>主备版实例。</li><li>源库字符集目前仅支持UTF8。</li></ul>
</td>
</tr>
<tr id="row88386418375"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p18381240377"><a name="p18381240377"></a><a name="p18381240377"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul5838646374"></a><a name="ul5838646374"></a><ul id="ul5838646374"><li>全量和增量同步时必须先在目标实例中手动创建SCHEMA和表。</li><li>增量同步的表要禁用外键，因为DRS并行回放会使得不同表之间的写入顺序和源库不一致，可能会触发外键约束限制，造成同步失败。</li></ul>
</td>
</tr>
</tbody>
</table>


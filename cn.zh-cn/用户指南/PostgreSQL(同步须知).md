# PostgreSQL-\>PostgreSQL<a name="drs_04_0107"></a>

## 使用技巧（需要人为配合）<a name="section98341051155812"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1691943218231)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section1691943218231"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table1416050154110"></a>
<table><thead align="left"><tr id="row1416114064110"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p41612014413"><a name="p41612014413"></a><a name="p41612014413"></a><strong id="b616112017413"><a name="b616112017413"></a><a name="b616112017413"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p2016110134112"><a name="p2016110134112"></a><a name="p2016110134112"></a><strong id="b9161902412"><a name="b9161902412"></a><a name="b9161902412"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row121618044120"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p61618014120"><a name="p61618014120"></a><a name="p61618014120"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul11161190104112"></a><a name="ul11161190104112"></a><ul id="ul11161190104112"><li><a href="#table12243151254116">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>实时同步会自动在目标库创建与源库相同的表和结构，不需要用户先行在目标库创建表结构。</li><li>同一个列上存在主键与唯一键时，只会同步主键。</li><li>一个同步任务只能对一个数据库进行数据同步，如果一个PostgreSQL实例下有多个数据库需要同步，则需要为每个数据库创建实时同步任务。</li><li>表级同步仅支持表、视图、物化视图和序列的对象选择，表上所创建的约束、索引和规则将随表一起同步，不同步触发器。相互关联的数据对象要确保同时同步或在目标库提前建好，避免因关联对象缺失，导致同步失败。常见的关联关系：视图引用表、视图引用视图、主外键关联表、表继承子表引用父表、表分区子分区表引用分区表、表自增列引用序列等。</li><li>同步对象权限时，如果目标库连接账号不具备SUPERUSER属性，源数据库中请勿存在对象的owner在对象上的权限被收回的情况，否则可能导致同步失败。</li></ul>
</td>
</tr>
<tr id="row1616210024114"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1916210015410"><a name="p1916210015410"></a><a name="p1916210015410"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul716215017417"></a><a name="ul716215017417"></a><ul id="ul716215017417"><li>同步过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>同步过程中，目标库不能进行写入操作，否则会导致数据不一致。</li><li>在任务启动、任务全量同步阶段，不允许对源数据库做DDL操作，比如删除表、增加表等，这样会导致任务同步失败。</li><li>增量同步过程中，支持部分DDL同步，详细操作可参考<a href="https://support.huaweicloud.com/usermanual-drs/drs_03_0088.html" target="_blank" rel="noopener noreferrer">PostgreSQL到PostgreSQL增量DDL同步</a>。</li><li>增量同步DDL是将源库执行的DDL在目标库完整地进行回放，请注意源库执行的DDL语句需要是目标库兼容的，否则可能导致任务失败。</li><li>全量同步物化视图后，如果目标数据库需要使用物化视图，需要执行以下刷新语句：<pre class="codeblock" id="codeblock5512112313440"><a name="codeblock5512112313440"></a><a name="codeblock5512112313440"></a>refresh materialized view matviewname;</pre>
</li><li>在增量数据同步过程中，如果选择了库级同步，且在增量同步过程中创建了新的无主键表或重命名已存在的无主键表，则需要在该表写入数据前执行以下命令：<pre class="codeblock" id="codeblock1890618571389"><a name="codeblock1890618571389"></a><a name="codeblock1890618571389"></a>alter table schema.table replica identity full;</pre>
</li><li>DRS使用test_decoding逻辑解码插件进行增量数据同步，在配置全量+增量任务之前，请确保源端PostgreSQL实例上安装了test_decoding插件。</li><li>全量同步过程中，DRS会向目标库PostgreSQL写入大量数据，会导致PostgreSQL的wal日志量急剧增长，PostgreSQL的磁盘有被写满的风险。可以通过在全量同步前关闭PostgreSQL的日志备份功能，减少wal日志的生产，同步完成后再将其打开的方式进行规避（具体操作方法可参考<a href="https://support.huaweicloud.com/api-rds/rds_09_0002.html" target="_blank" rel="noopener noreferrer">设置自动备份策略</a>）。<div class="caution" id="note1226619107717"><a name="note1226619107717"></a><a name="note1226619107717"></a><span class="cautiontitle"> 注意： </span><div class="cautionbody"><a name="ul1685483212511"></a><a name="ul1685483212511"></a><ul id="ul1685483212511"><li>关闭日志备份会影响数据库的灾备恢复，请根据实际情况谨慎选择。</li></ul>
</div></div>
</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section86695405239"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table12243151254116"></a>
<table><thead align="left"><tr id="row192436123410"><th class="cellrowborder" valign="top" width="18.42%" id="mcps1.2.3.1.1"><p id="p17243181254115"><a name="p17243181254115"></a><a name="p17243181254115"></a><strong id="b324381211411"><a name="b324381211411"></a><a name="b324381211411"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.58%" id="mcps1.2.3.1.2"><p id="p82432123418"><a name="p82432123418"></a><a name="p82432123418"></a><strong id="b14243171284116"><a name="b14243171284116"></a><a name="b14243171284116"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row02431312134113"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p13244151214111"><a name="p13244151214111"></a><a name="p13244151214111"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul1040212611348"></a><a name="ul1040212611348"></a><ul id="ul1040212611348"><li><strong id="b146331134115115"><a name="b146331134115115"></a><a name="b146331134115115"></a>全量+增量同步最小权限要求：</strong><a name="ul24621589527"></a><a name="ul24621589527"></a><ul id="ul24621589527"><li>源数据库帐户需要数据库的CONNECT权限，模式的USAGE权限，表的SELECT权限，序列的SELECT权限，无主键表还需要表的UPDATE、DELETE和TRUNCATE权限（仅用于进行短暂的无主键表锁表操作），还需备REPLICATION连接权限。<p id="p1642049174715"><a name="p1642049174715"></a><a name="p1642049174715"></a>REPLICATION连接权限的添加方法：在源数据库的“pg_hba.conf”配置文件的所有配置前增加一行配置“host replication &lt;src_user_name&gt; &lt;drs_instance_ip&gt;/32 md5”，在源库中通过SUPERUSER用户执行语句“select pg_reload_conf();”或重启数据库实例生效。</p>
</li><li>库级同步时，目标数据库账户需要具有CREATEDB权限，如果需要同步用户，还需要具有CREATEROLE权限。</li><li>表级同步时，如果数据库不存在，目标数据库账户需要具有CREATEDB权限；如果数据库存在，目标数据库账户需要数据库的CREATE和CONNECT权限；如果模式存在，需要模式的CREATE和USAGE权限。</li></ul>
</li></ul>
</td>
</tr>
<tr id="row102441712194111"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p1224491224118"><a name="p1224491224118"></a><a name="p1224491224118"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul1233752312477"></a><a name="ul1233752312477"></a><ul id="ul1233752312477"><li>支持的同步对象有：表、索引、外键、存储过程、函数、视图、约束、触发器、模式、插件、排序规则、编码转换信息、数据类型、聚合函数、操作符、序列、物化视图、统计扩展、规则、事件触发器、类型转换、转换信息、文本搜索解析器、文本搜索字典、文本搜索模版、文本搜索配置。</li></ul>
<a name="ul8301575568"></a><a name="ul8301575568"></a><ul id="ul8301575568"><li>支持的字段类型有：数字类型、货币类型、字符类型、二进制数据类型、日期/时间类型、布尔类型、枚举类型、几何类型、网络地址类型、位串类型、文本搜索类型、UUID类型、XML类型、JSON类型、数组、复合类型、范围类型。</li><li>插件同步将在目标库使用默认版本创建插件对象，仅支持插件的对象的同步，如果源库在使用某个插件的过程中有新增的插件元数据，请在同步结束后使用该插件自有的语法重建元数据。</li><li>不支持同步源库中的临时表。</li><li>不支持C语言函数。</li><li>支持在跨大版本间同步，不允许从高的大版本同步到低的大版本。</li><li>源库中的无日志表（UNLOGGED TABLE）进入增量期间后，将无法同步增量数据到目标库。</li><li>同步用户时，不会同步目标库已存在用户的任何属性、成员关系和默认访问权限，如需同步源库对应用户，请先在目标库删除已存在用户；用户默认访问权限仅在库级同步时进行同步；目标库连接账号不能作为其他用户的父用户，当目标库连接账号不是SUPERUSER时，其必须具备CREATEROLE属性，且源库账号的SUPERUSER、REPLICATION、BYPASSRLS属性无法同步。如果源库存在与目标库连接账号同名的用户，则其他用户与它的成员关系将在结束任务时进行同步，而非全量阶段。</li></ul>
<a name="ul1813485052510"></a><a name="ul1813485052510"></a><ul id="ul1813485052510"><li>不同步数据库中的系统模式，包括：“pg_”开头的任何模式、“information_schema”，RDS for PostgreSQL增强版还包括“sys”、“utl_raw”、“dbms_lob”、“dbms_output”和“dbms_random”。</li></ul>
</td>
</tr>
<tr id="row5245101224118"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p52454123417"><a name="p52454123417"></a><a name="p52454123417"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul17406112220"></a><a name="ul17406112220"></a><ul id="ul17406112220"><li>源数据库库名不支持如下字符：“+”、“%”、“"”、“'”、“\ ”、“&lt;”和“&gt;”，模式名和表名不支持“"”和“.”，列名不支持如下字符：“"”和“'”。</li><li>源数据库的max_replication_slots参数值必须大于当前已使用的复制槽数量。</li><li>源数据库的max_wal_senders参数值需不小于max_replication_slots参数值。</li><li>源数据库参数wal_level必须配置为logical。</li><li>源数据库中同一个数据库下的触发器名称必须唯一。</li><li>源数据库中无主键表的REPLICA IDENTITY属性必须为FULL。</li></ul>
<a name="ul1724561274115"></a><a name="ul1724561274115"></a><ul id="ul1724561274115"><li>源库不支持低于PostgreSQL 9.4的版本。</li><li>源库为RDS for PostgreSQL增强版时，目标库仅支持RDS for PostgreSQL增强版。</li><li>如需同步源库用户的密码，源库迁移账号必须具有系统表pg_catalog.pg_authid的select权限。</li></ul>
</td>
</tr>
<tr id="row1124641294113"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p92469122412"><a name="p92469122412"></a><a name="p92469122412"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul172461612154112"></a><a name="ul172461612154112"></a><ul id="ul172461612154112"><li>目标库版本不能低于源库版本。</li><li>目标数据库实例的运行状态必须正常。</li><li>库级同步时，如果源库不存在plpgsql之外的插件，目标数据库不能包含与源库要同步的数据库同名的数据库；如果源库安装了plpgsql之外的插件，请确保目标库仅在对应数据库中安装了插件，而未创建其他自建对象。</li><li>表级同步时，目标数据库不能包含与源库要同步的对象同名的对象。</li><li>目标数据库实例必须有足够的磁盘空间。</li><li>目标数据库和源数据库的lc_monetary参数值需保持一致。</li><li>目标数据库的block_size参数值必须大于源库中的对应参数值。</li><li>全量+增量同步时，如果源数据库中要同步的表包含外键，目标数据库的session_replication_role参数必须设置为replica。同步结束后，请将此参数设置为origin。</li><li>选择同步对象权限时，需要满足如下要求：<a name="ul1132614124419"></a><a name="ul1132614124419"></a><ul id="ul1132614124419"><li>目标库迁移用户不是SUPERUSER时，源库下层对象的owner必须具有上层对象的create权限，比如表的owner必须具有其schema上的create权限。</li><li>目标库迁移用户不是SUPERUSER时，无法同步父用户为SUPERUSER的成员关系，以及owner/grantor为SUPERUSER的对象的owner/grantor。</li><li>目标库迁移用户的default privilege需要为系统默认值，否则可能导致目标库与源库的对象权限不一致。</li></ul>
</li></ul>
</td>
</tr>
</tbody>
</table>


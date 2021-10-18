# PostgreSQL-\>PostgreSQL<a name="drs_04_0097"></a>

## 操作要求<a name="section83714237916"></a>

针对一些无法预知或人为因素及环境突变导致迁移失败的情况，数据复制服务提供以下常见的操作限制，供您在迁移过程中参考。

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
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul11161190104112"></a><a name="ul11161190104112"></a><ul id="ul11161190104112"><li><a href="#table12243151254116">表2</a>中的环境要求均不允许在迁移过程中修改，直至迁移结束。</li><li>一个迁移任务只能对一个数据库进行数据迁移，如果一个PostgreSQL实例下有多个数据库需要迁移，则需要为每个数据库创建实时迁移任务。</li><li>表级迁移仅支持表、视图、物化视图和序列的对象选择，表上所创建的约束、索引和规则将和表一起迁移，不迁移触发器。相互关联的数据对象要确保同时迁移或在目标库提前建好，避免迁移因关联对象缺失，导致迁移失败。常见的关联关系：视图引用表、视图引用视图、主外键关联表、表继承子表引用父表、表分区子分区表引用分区表、表自增列引用序列等。</li></ul>
</td>
</tr>
<tr id="row1616210024114"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1916210015410"><a name="p1916210015410"></a><a name="p1916210015410"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul716215017417"></a><a name="ul716215017417"></a><ul id="ul716215017417"><li>迁移过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>迁移过程中，目标库不能进行写入操作，否则会导致数据不一致。</li><li>在任务全量迁移阶段，由于迁移期间源库发生的变更无法完全同步到目标库，所以源库不能有任何对象和数据的变更操作，否则会导致目标库与源库的对象和数据状态不一致。如果源库无法停止非只读业务，请选择使用PostgreSQL的全量+增量实时同步而非全量实时迁移，可参考<a href="PostgreSQL(同步须知).md">PostgreSQL-&gt;PostgreSQL</a>。</li><li>在任务启动、任务全量迁移阶段，不允许对源数据库做DDL操作，比如删除表、增加表等，这样会导致任务迁移失败。</li><li>全量迁移物化视图后，如果目标数据库需要使用物化视图，需要执行以下刷新语句：<pre class="codeblock" id="codeblock9217112218395"><a name="codeblock9217112218395"></a><a name="codeblock9217112218395"></a>refresh materialized view matviewname;</pre>
</li><li>库级迁移时，如果目标库连接用户不具备SUPERUSER属性，源库中自建的以下对象将由于权限不足无法迁移：EVENT TRIGGER对象、指定WITHOUT FUNCTION参数的CAST对象、指定LEAKROOF或SUPPORT参数的FUNCTION对象。</li><li>全量迁移过程中，DRS会向目标库PostgreSQL写入大量数据，会导致PostgreSQL的wal日志量急剧增长，PostgreSQL的磁盘有被写满的风险。可以通过在全量迁移前关闭PostgreSQL的日志备份功能，减少wal日志的生产，迁移完成后再将其打开的方式进行规避（具体操作方法可参考<a href="https://support.huaweicloud.com/api-rds/rds_09_0002.html" target="_blank" rel="noopener noreferrer">设置自动备份策略</a>）。<div class="caution" id="note775611117557"><a name="note775611117557"></a><a name="note775611117557"></a><span class="cautiontitle"> 注意： </span><div class="cautionbody"><a name="ul1685483212511"></a><a name="ul1685483212511"></a><ul id="ul1685483212511"><li>关闭日志备份会影响数据库的灾备恢复，请根据实际情况谨慎选择。</li></ul>
</div></div>
</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section1645253517920"></a>

-   实时迁移对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

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
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul1940212610342"></a><a name="ul1940212610342"></a><ul id="ul1940212610342"><li><strong id="b1402626153410"><a name="b1402626153410"></a><a name="b1402626153410"></a>全量迁移最小权限要求：</strong><a name="ul14402102618346"></a><a name="ul14402102618346"></a><ul id="ul14402102618346"><li>源数据库帐户需要具备数据库的CONNECT权限，模式的USAGE权限，表的SELECT权限，序列的SELECT权限，无主键表还需要表的UPDATE、DELETE和TRUNCATE权限（仅用于进行短暂的无主键表锁表操作）。</li><li>库级迁移时，目标数据库账户需要具有CREATEDB权限。</li><li>表级迁移时，如果数据库不存在，目标数据库账户需要具有CREATEDB权限；如果数据库存在，目标数据库账户需要数据库的CREATE和CONNECT权限；如果模式存在，需要模式的CREATE和USAGE权限。</li></ul>
    </li></ul>
    </td>
    </tr>
    <tr id="row102441712194111"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p1224491224118"><a name="p1224491224118"></a><a name="p1224491224118"></a>迁移对象约束</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul8301575568"></a><a name="ul8301575568"></a><ul id="ul8301575568"><li>支持表、索引、外键、存储过程、函数、视图、约束、触发器、模式、插件、排序规则、编码转换信息、数据类型、聚合函数、操作符、序列、物化视图、统计扩展、规则、事件触发器、类型转换、转换信息、文本搜索解析器、文本搜索字典、文本搜索模版、文本搜索配置的迁移。</li><li>支持如下字段类型：数字类型、货币类型、字符类型、二进制数据类型、日期/时间类型、布尔类型、枚举类型、几何类型、网络地址类型、位串类型、文本搜索类型、UUID类型、XML类型、JSON类型、数组、复合类型、范围类型。</li><li>插件迁移将在目标库使用默认版本创建插件对象，仅支持插件的对象的迁移，如果源库在使用某个插件的过程中有新增的插件元数据，请在迁移结束后使用该插件自有的语法重建元数据。</li><li>不支持迁移源库中的临时表。</li><li>不支持C语言函数。</li><li>支持在跨大版本间迁移，不允许从高的大版本迁移到低的大版本。</li></ul>
    <a name="ul1813485052510"></a><a name="ul1813485052510"></a><ul id="ul1813485052510"><li>不迁移数据库中的系统模式，包括：“pg_”开头的任何模式、“information_schema”，RDS for PostgreSQL增强版还包括“sys”、“utl_raw”、“dbms_lob”、“dbms_output”和“dbms_random”。</li></ul>
    </td>
    </tr>
    <tr id="row5245101224118"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p52454123417"><a name="p52454123417"></a><a name="p52454123417"></a>源数据库要求</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul17406112220"></a><a name="ul17406112220"></a><ul id="ul17406112220"><li>源数据库库名不支持如下字符：“+”、“%”、“"”、“'”、“\ ”、“&lt;”和“&gt;”，模式名和表名不支持“"”和“.”。</li><li>源数据库中同一个数据库下的触发器名称必须唯一。</li><li>源库的block_size参数不能大于目标库。</li></ul>
    <a name="ul1724561274115"></a><a name="ul1724561274115"></a><ul id="ul1724561274115"><li>源库不支持低于PostgreSQL 9.4的版本。</li><li>源库为RDS for PostgreSQL增强版时，目标库仅支持RDS for PostgreSQL增强版。</li><li>为保证源数据库连接的安全性，请将源库的ssl参数设置为on，且源库连接用户的认证方式必须为密码口令认证。认证方式的修改方法为在源数据库的“pg_hba.conf”配置文件的所有配置前增加一行配置“host all &lt;src_user_name&gt; &lt;drs_instance_ip&gt;/32 md5”，在源库中通过SUPERUSER用户执行语句“select pg_reload_conf();”或重启数据库实例生效。</li></ul>
    </td>
    </tr>
    <tr id="row1124641294113"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p92469122412"><a name="p92469122412"></a><a name="p92469122412"></a>目标数据库要求</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul172461612154112"></a><a name="ul172461612154112"></a><ul id="ul172461612154112"><li>目标库版本不能低于源库版本。</li><li>目标数据库实例的运行状态必须正常。</li><li>库级迁移时，如果源库不存在plpgsql之外的插件，目标数据库不能包含与指定数据库同名的数据库；如果源库安装了plpgsql之外的插件，请确保目标库仅在对应数据库中安装了插件，而未创建其他自建对象。</li><li>表级迁移时，目标数据库不能包含与源库要迁移的对象同名的对象。</li><li>目标数据库实例必须有足够的磁盘空间。</li><li>目标数据库和源数据库的lc_monetary参数值需保持一致。</li><li>目标数据库的block_size参数值必须大于源库中的对应参数值。</li></ul>
    </td>
    </tr>
    </tbody>
    </table>



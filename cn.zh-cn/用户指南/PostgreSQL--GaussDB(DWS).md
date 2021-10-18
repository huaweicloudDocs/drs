# PostgreSQL-\>GaussDB\(DWS\)<a name="drs_03_1125"></a>

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
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul11161190104112"></a><a name="ul11161190104112"></a><ul id="ul11161190104112"><li><a href="#table12243151254116">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>相互关联的数据对象要确保同时同步，避免同步因关联对象缺失，导致同步失败。常见的关联关系：视图引用表、视图引用视图、主外键关联表、表继承子表引用父表、表分区子分区表引用分区表、表自增列引用序列等。</li><li>实时同步会自动在目标库创建与源库相同的表和结构，不需要用户先行在目标库创建表结构。</li><li>一个同步任务只能对一个数据库进行数据同步，如果一个PostgreSQL实例下有多个数据库需要同步，则需要为每个数据库创建实时同步任务。</li><li>表级同步时仅支持指定表名、序列名进行同步，如果同步表结构时出现依赖的对象（如type、sequence等）没有创建时，需要用户手动创建依赖对象后重试任务。</li><li>不支持在目标库创建表时指定分布列，源库表的主键约束必须包含目标库表分布列，主键约束没有包含分布列时，无法成功创建表，需要用户手动创建表后重试任务。</li><li>分区表、继承表将转换为普通表同步到目标库中。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li></ul>
</td>
</tr>
<tr id="row1616210024114"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1916210015410"><a name="p1916210015410"></a><a name="p1916210015410"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul16241732787"></a><a name="ul16241732787"></a><ul id="ul16241732787"><li>同步过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>在任务启动、任务全量同步阶段，不建议对源数据库做删除类型的DDL操作，比如删除数据库、索引、视图等，这样可能会引起任务同步失败。</li><li>在增量数据同步过程中，如果选择了库级同步，且在增量同步过程中创建了新的无主键表或重命名已存在的无主键表，则需要在该表写入数据前执行以下命令：<pre class="codeblock" id="codeblock32971690917"><a name="codeblock32971690917"></a><a name="codeblock32971690917"></a>alter table schema.table replica identity full;</pre>
</li><li>增量同步过程中，暂不支持源数据库DDL的复制。源库新增表、删除表、修改表名、表新增列、修改列类型等DDL操作将不会同步至目标库，而且相关表的数据也将无法同步至目标库。<div class="caution" id="note166441151175614"><a name="note166441151175614"></a><a name="note166441151175614"></a><span class="cautiontitle"> 注意： </span><div class="cautionbody"><p id="p186444513568"><a name="p186444513568"></a><a name="p186444513568"></a>DRS使用test_decoding逻辑解码插件进行增量数据同步，在配置全量+增量任务之前，请确保源端PostgreSQL实例上安装了test_decoding插件。</p>
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
<td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul8475249145217"></a><a name="ul8475249145217"></a><ul id="ul8475249145217"><li><strong id="b1757342714532"><a name="b1757342714532"></a><a name="b1757342714532"></a>全量同步最小权限要求：</strong><a name="ul11652204013533"></a><a name="ul11652204013533"></a><ul id="ul11652204013533"><li>源数据库帐户需要具备数据库的CONNECT权限，模式的USAGE权限，表的SELECT权限，PostgresSQL10.0以下的版本还需要序列的SELECT权限，无主键表还需要表的UPDATE、DELETE和TRUNCATE权限（仅用于进行短暂的无主键表锁表操作）。</li><li>库级同步时，目标数据库账户需要具有CREATEDB权限。</li><li>表级同步时，如果数据库不存在，目标数据库账户需要具有CREATEDB权限；如果数据库存在，目标数据库账户需要数据库的CREATE和CONNECT权限；如果模式存在，需要模式的CREATE和USAGE权限。</li></ul>
</li></ul>
<a name="ul84757496523"></a><a name="ul84757496523"></a><ul id="ul84757496523"><li><strong id="b18475204915215"><a name="b18475204915215"></a><a name="b18475204915215"></a>全量+增量同步最小权限要求：</strong><a name="ul1040212611348"></a><a name="ul1040212611348"></a><ul id="ul1040212611348"><li>源数据库帐户需要具备REPLICATION权限，数据库的CONNECT权限，模式的USAGE权限，表的SELECT权限，PostgresSQL10.0以下的版本还需要序列的SELECT权限。</li><li>库级同步时，目标数据库账户需要具有CREATEDB权限。</li><li>表级同步时，如果数据库不存在，目标数据库账户需要具有CREATEDB权限；如果数据库存在，目标数据库账户需要数据库的CREATE和CONNECT权限；如果模式存在，需要模式的CREATE和USAGE权限。</li></ul>
</li></ul>
</td>
</tr>
<tr id="row102441712194111"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p1224491224118"><a name="p1224491224118"></a><a name="p1224491224118"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul8301575568"></a><a name="ul8301575568"></a><ul id="ul8301575568"><li>库级同步仅支持表、序列、自定义类型的同步。</li><li>表级同步仅支持表、序列的同步。</li><li>不支持同步源库中的临时表。</li><li>表中必须包含以下数据类型：tinyint、smallint、int、bigint、numeric、decimal、char、bpchar、varchar、varchar2、nvarchar2、text、date、time、timetz、timestamp、timestamptz、interval、smalldatetime。</li><li>不支持xml、line类型同步。</li><li>源库中的无日志表（UNLOGGED TABLE）进入增量期间后，将无法同步增量数据到目标库。</li></ul>
<a name="ul1813485052510"></a><a name="ul1813485052510"></a><ul id="ul1813485052510"><li>不同步数据库中的系统模式，包括：“pg_”开头的任何模式、“information_schema”，RDS for PostgreSQL增强版还包括“sys”、“utl_raw”、“dbms_lob”、“dbms_output”和“dbms_random”。</li></ul>
</td>
</tr>
<tr id="row5245101224118"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p52454123417"><a name="p52454123417"></a><a name="p52454123417"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul17406112220"></a><a name="ul17406112220"></a><ul id="ul17406112220"><li>源数据库库名不支持如下字符：“+”、“%”、“"”、“'”、“\ ”、“&lt;”和“&gt;”，schema名和表名不支持“'”、“"”和“.”。</li></ul>
<a name="ul5283301112"></a><a name="ul5283301112"></a><ul id="ul5283301112"><li>同步的表必须包含主键，如果没有主键，需要设置无主建表的复制属性为full。</li></ul>
</td>
</tr>
<tr id="row1124641294113"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p92469122412"><a name="p92469122412"></a><a name="p92469122412"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul172461612154112"></a><a name="ul172461612154112"></a><ul id="ul172461612154112"><li>目标数据库实例的运行状态必须正常。</li><li>目标数据库不能包含与源库要同步的数据库同名的数据库。</li><li>目标数据库实例必须有足够的磁盘空间。</li></ul>
<a name="ul1465137572"></a><a name="ul1465137572"></a><ul id="ul1465137572"><li>目标数据库的字符集必须与源数据库一致。</li><li>目标数据库的时区设置必须与源数据库一致。</li><li>增量同步的表要禁用外键，因为DRS并行回放会使得不同表之间的写入顺序和源库不一致，可能会触发外键约束限制，造成同步失败。</li></ul>
</td>
</tr>
</tbody>
</table>


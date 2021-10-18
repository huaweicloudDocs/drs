# DDM-\>GaussDB\(DWS\)<a name="drs_04_0116"></a>

## 使用技巧（需要人为配合）<a name="section449714073815"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1691943218231)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section1691943218231"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table0488162412572"></a>
<table><thead align="left"><tr id="row54881224145717"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p144884246576"><a name="p144884246576"></a><a name="p144884246576"></a><strong id="b1048842414579"><a name="b1048842414579"></a><a name="b1048842414579"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p64881524195710"><a name="p64881524195710"></a><a name="p64881524195710"></a><strong id="b6489824115711"><a name="b6489824115711"></a><a name="b6489824115711"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row9489152495714"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1848922455711"><a name="p1848922455711"></a><a name="p1848922455711"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul6489172411572"></a><a name="ul6489172411572"></a><ul id="ul6489172411572"><li><a href="#table9324153225714">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>源数据库中存在主键重复的数据时, 直接同步将导致目标库数据比源库少, 请务必检查并订正数据后启动同步。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li><li>数据类型不兼容时，可能引起同步失败。</li></ul>
</td>
</tr>
<tr id="row6489152410578"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p17489152412570"><a name="p17489152412570"></a><a name="p17489152412570"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1248912411571"></a><a name="ul1248912411571"></a><ul id="ul1248912411571"><li>增量同步过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>增量同步场景下，不支持源数据库进行恢复操作</li><li>增量同步过程中，支持部分DDL操作。<a name="ul103341230182215"></a><a name="ul103341230182215"></a><ul id="ul103341230182215"><li>不支持 DROP_DATABASE、DROP_TABLE、TRUNCATE_TABLE、CREATE_VIEW、DROP_VIEW。</li><li>不支持使用Online DDL。</li><li>支持创建表，例如 ：<pre class="codeblock" id="codeblock191811018193710"><a name="codeblock191811018193710"></a><a name="codeblock191811018193710"></a>create table `ddl_test` (id int, c1 varchar(25), primary key(id));
create table `ddl_test_gho` like `ddl_test`;</pre>
</li><li>支持表的重命名，源表和目标表必须都在对象选择里面，例如：<pre class="codeblock" id="codeblock66961829183712"><a name="codeblock66961829183712"></a><a name="codeblock66961829183712"></a>rename table `ddl_test` to `ddl_test_new`;</pre>
</li><li>支持表字段的增和改，不支持删列，例如：<pre class="codeblock" id="codeblock181421335153719"><a name="codeblock181421335153719"></a><a name="codeblock181421335153719"></a>alter table `ddl_test` add column `c2` varchar(25); 
alter table `ddl_test` modify column `c1` varchar(50);
alter table `ddl_test` alter c1 set default 'xxx';</pre>
</li><li>支持修改表索引，例如：<pre class="codeblock" id="codeblock3289184533714"><a name="codeblock3289184533714"></a><a name="codeblock3289184533714"></a>alter table `ddl_test` drop primary key; 
alter table `ddl_test` add primary key(id); 
alter table `ddl_test` add index  `ddl_test_uk`(id);
alter table `ddl_test` drop index `ddl_test_uk`;</pre>
</li><li>表级同步支持增加列、修改列、增加主键和普通索引。</li><li>库级同步支持新建表、rename表、增加列、修改列、增加主键和普通索引。</li><li>新增和修改表名、列名、索引名时不能超出63字符，否则任务会失败。</li><li>源库无主键表增加主键的时候，必须含有第一列，否则任务会失败。</li></ul>
</li><li>创建任务后，不支持增加逻辑库或修改旧逻辑库关联新的RDS，否则会导致同步任务失败。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section86695405239"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table9324153225714"></a>
<table><thead align="left"><tr id="row53248326579"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p8324163210573"><a name="p8324163210573"></a><a name="p8324163210573"></a><strong id="b7324183213578"><a name="b7324183213578"></a><a name="b7324183213578"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p6324143210575"><a name="p6324143210575"></a><a name="p6324143210575"></a><strong id="b11325113295711"><a name="b11325113295711"></a><a name="b11325113295711"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row9325143210573"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1832513219577"><a name="p1832513219577"></a><a name="p1832513219577"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul14325173245711"></a><a name="ul14325173245711"></a><ul id="ul14325173245711"><li>源数据库DDM帐户需要具备SELECT权限，DDM物理分片数据库帐户需要具备如下权限：SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</li></ul>
<a name="ul1632533265720"></a><a name="ul1632533265720"></a><ul id="ul1632533265720"><li>提供的目标数据库帐号必须具有每张表的如下权限：INSERT、SELECT、UPDATE、DELETE、CONNECT、CREATE、REFERENCES。</li></ul>
</td>
</tr>
<tr id="row2032563215715"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p113253325578"><a name="p113253325578"></a><a name="p113253325578"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul162311853125620"></a><a name="ul162311853125620"></a><ul id="ul162311853125620"><li>全量同步支持数据、表结构和索引的同步。</li><li>目标库不支持唯一键表，同步过程中将忽略源数据库中的唯一键表。</li><li>不支持同步无主键表，若选择同步的表中存在无主键表，则同步失败。</li></ul>
</td>
</tr>
<tr id="row23251632185719"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p232511321573"><a name="p232511321573"></a><a name="p232511321573"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul232503255711"></a><a name="ul232503255711"></a><ul id="ul232503255711"><li>源物理分片数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，binlog保存时间越长越好，建议为3天。</li><li>增量同步时，必须设置MySQL源数据库的server_id。如果源数据库版本小于或等于MySQL5.6，server_id的取值范围在2－4294967296之间；如果源数据库版本大于或等于MySQL5.7，server_id的取值范围在1－4294967296之间。</li><li>源分库分表中间件中的库名、表名不能包含：'&lt;&gt;/\以及非ASCII字符。</li><li>源物理分片数据库建议开启skip-name-resolve，减少连接超时的可能性。</li><li>源物理分片数据库的GTID状态建议为开启状态。</li><li>源物理分片数据库不支持枚举类型和set集合类型的<span id="text19326143212573"><a name="text19326143212573"></a><a name="text19326143212573"></a>实时同步</span>。</li><li>源库的timestamp列的默认值，需要在目标库的合理取值内，否则会导致同步失败。</li></ul>
</td>
</tr>
<tr id="row532653214576"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p16326173265714"><a name="p16326173265714"></a><a name="p16326173265714"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1532617322571"></a><a name="ul1532617322571"></a><ul id="ul1532617322571"><li>目标数据库实例的运行状态必须正常。</li><li>目标数据库实例必须有足够的磁盘空间。</li><li>目标数据库的时区设置必须与源数据库一致。</li></ul>
</td>
</tr>
</tbody>
</table>


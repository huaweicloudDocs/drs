# MySQL-\>PostgreSQL<a name="drs_04_0103"></a>

## 使用技巧（需要人为配合）<a name="section98341051155812"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1691943218231)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。
    -   同步无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。
    -   由于MySQL固有特点限制，CPU资源紧张时，存储引擎为Tokudb的表，读取速度可能下降至10%。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section1691943218231"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table20914521301"></a>
<table><thead align="left"><tr id="row131075213014"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p151017523309"><a name="p151017523309"></a><a name="p151017523309"></a><strong id="b510185218302"><a name="b510185218302"></a><a name="b510185218302"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p1610185213305"><a name="p1610185213305"></a><a name="p1610185213305"></a><strong id="b21015525307"><a name="b21015525307"></a><a name="b21015525307"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row810952123012"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p51015520300"><a name="p51015520300"></a><a name="p51015520300"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul181015263020"></a><a name="ul181015263020"></a><ul id="ul181015263020"><li><a href="#table4268111193114">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>相互关联的数据对象要确保同时同步，避免因关联对象缺失，导致同步失败。常见的关联关系：视图引用表、视图引用视图等。</li><li>网络中断在30秒内恢复的，不影响<span id="text1311185212308"><a name="text1311185212308"></a><a name="text1311185212308"></a>实时同步</span>，如果超过30秒，则会导致同步任务失败。</li><li>支持通过映射方式实现多个库对一个库的<span id="text611185211305"><a name="text611185211305"></a><a name="text611185211305"></a>实时同步</span>，且映射库之间不允许存在同名表，该功能需要提交工单申请才能使用。<span id="text1836124514309"><a name="text1836124514309"></a><a name="text1836124514309"></a>您可以在管理控制台右上角，选择“工单 &gt; 新建工单”，完成工单提交。</span></li><li>不支持源数据库进行恢复操作。</li><li>不支持外键级联操作。</li><li>由于无主键表缺乏行的唯一性标志，网络不稳定时涉及少量重试，表数据存在少量不一致的可能性。</li><li>索引同步不区分索引类型，同步到目标数据库都是btree索引。</li><li>目标数据库与源数据库字符集不一致可能会导致同步后数据不一致或者同步失败。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li><li>数据类型不兼容时，可能引起同步失败。</li><li>仅支持记录违反非空约束的异常数据、char类型或varchar类型超出字段长度限制的异常数据。</li><li>源库和目标库为RDS for MySQL实例时，不支持带有TDE特性并建立具有加密功能表。</li></ul>
</td>
</tr>
<tr id="row141165273015"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p211205212305"><a name="p211205212305"></a><a name="p211205212305"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul31155273015"></a><a name="ul31155273015"></a><ul id="ul31155273015"><li><span id="text511145213304"><a name="text511145213304"></a><a name="text511145213304"></a>实时同步</span>过程中，若源库为RDS时，支持修改端口，修改之后同步任务失败，需要通过重试后继续进行同步。</li><li><span id="text811452193013"><a name="text811452193013"></a><a name="text811452193013"></a>实时同步</span>过程中，若源库为非RDS时，不支持修改端口。</li><li><span id="text51112522303"><a name="text51112522303"></a><a name="text51112522303"></a>实时同步</span>过程中，不支持IP、账号、密码修改。</li><li>不支持强制清理binlog，否则会导致同步任务失败。</li><li>全量同步过程中不支持DDL操作。</li><li>增量同步过程中，支持部分DDL操作。<a name="ul103341230182215"></a><a name="ul103341230182215"></a><ul id="ul103341230182215"><li>不支持 DROP_DATABASE、DROP_TABLE、TRUNCATE_TABLE、CREATE_VIEW、DROP_VIEW。</li><li>不支持使用Online DDL。</li><li>支持创建表，例如 ：<pre class="codeblock" id="codeblock191811018193710"><a name="codeblock191811018193710"></a><a name="codeblock191811018193710"></a>create table `ddl_test` (id int, c1 varchar(25), primary key(id));
create table `ddl_test_gho` like `ddl_test`;</pre>
</li><li>支持表的重命名，源表和目标表必须都在对象选择里面，例如：<pre class="codeblock" id="codeblock66961829183712"><a name="codeblock66961829183712"></a><a name="codeblock66961829183712"></a>rename table `ddl_test` to `ddl_test_new`;</pre>
</li><li>支持表字段的增删改，例如：<pre class="codeblock" id="codeblock181421335153719"><a name="codeblock181421335153719"></a><a name="codeblock181421335153719"></a>alter table `ddl_test` add column `c2` varchar(25); 
alter table `ddl_test` modify column `c1` varchar(50);
alter table `ddl_test` alter c1 set default 'xxx';</pre>
</li><li>支持修改表索引，例如：<pre class="codeblock" id="codeblock3289184533714"><a name="codeblock3289184533714"></a><a name="codeblock3289184533714"></a>alter table `ddl_test` drop primary key; 
alter table `ddl_test` add primary key(id); 
alter table `ddl_test` add index  `ddl_test_uk`(id);
alter table `ddl_test` drop index `ddl_test_uk`;</pre>
</li><li>表级同步支持增加列、修改列、增加主键和普通索引。多对一情况下执行colunm重命名操作，必须停业务操作，不然会有数据不一致的风险，例如：<pre class="codeblock" id="codeblock18761135514016"><a name="codeblock18761135514016"></a><a name="codeblock18761135514016"></a>alter table `ddl_test` modify column `c1` varchar(50);</pre>
</li><li>库级同步支持新建表、rename表、增加列、修改列、增加主键和普通索引。</li><li>新增和修改表名、列名、索引名时不能超出63字符，否则任务会失败。</li></ul>
</li><li>建议将expire_log_day参数设置在合理的范围，确保恢复时断点处的binlog尚未过期，以保证服务中断后的顺利恢复。</li><li>全量同步过程中，DRS会向目标库PostgreSQL写入大量数据，会导致PostgreSQL的wal日志量急剧增长，PostgreSQL的磁盘有被写满的风险。可以通过在全量同步前关闭PostgreSQL的日志备份功能，减少wal日志的生产，同步完成后再将其打开的方式进行规避（具体操作方法可参考<a href="https://support.huaweicloud.com/api-rds/rds_09_0002.html" target="_blank" rel="noopener noreferrer">设置自动备份策略</a>）。<div class="caution" id="note18510115315395"><a name="note18510115315395"></a><a name="note18510115315395"></a><span class="cautiontitle"> 注意： </span><div class="cautionbody"><p id="p775316544013"><a name="p775316544013"></a><a name="p775316544013"></a>关闭日志备份会影响数据库的灾备恢复，请根据实际情况谨慎选择。</p>
</div></div>
</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section86695405239"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table4268111193114"></a>
<table><thead align="left"><tr id="row192682116315"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p7268511173116"><a name="p7268511173116"></a><a name="p7268511173116"></a><strong id="b17268151111312"><a name="b17268151111312"></a><a name="b17268151111312"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p12691811123110"><a name="p12691811123110"></a><a name="p12691811123110"></a><strong id="b4269911193118"><a name="b4269911193118"></a><a name="b4269911193118"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row17269151111317"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p52691811163110"><a name="p52691811163110"></a><a name="p52691811163110"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul526901117315"></a><a name="ul526901117315"></a><ul id="ul526901117315"><li>源数据库帐户需要具备最小权限：SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</li><li>提供的目标数据库帐号必须具有每张表的如下权限：INSERT、SELECT、UPDATE、DELETE。RDS for PostgreSQL实例的root帐号默认已具有上述权限。</li></ul>
</td>
</tr>
<tr id="row1326961119317"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p726915111312"><a name="p726915111312"></a><a name="p726915111312"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul42695114312"></a><a name="ul42695114312"></a><ul id="ul42695114312"><li>支持表、索引、约束（主键、唯一键、空、非空）的同步，不支持视图、外键、存储过程、触发器、函数、事件、虚拟列的同步。</li><li>由于mysql中视图支持as select ... from a join b where ...等语法，pg不支持,可能会导致视图同步失败。</li><li>不支持的数据类型有：xml、geometry、point、lineString、polygon、geometrycollection、multipoint、multilinestring、multipolygon、json。</li><li>不支持非MyISAM和非InnoDB表的同步。</li></ul>
</td>
</tr>
<tr id="row1227001115315"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p13270121113118"><a name="p13270121113118"></a><a name="p13270121113118"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1627011193115"></a><a name="ul1627011193115"></a><ul id="ul1627011193115"><li>MySQL源数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议源数据库binlog保存时间越长越好，建议为3天。</li><li>源数据库expire_logs_days参数值为0，可能会导致同步失败。</li><li>必须设置MySQL源数据库的server－id，server－id的取值范围在2－4294967296之间。</li><li>源数据库中的库名不能包含：'.&lt;&gt;以及中文等其他非ASCII字符。</li><li>源数据库中的表名、视图名不能包含：'&lt;&gt;以及中文等其他非ASCII字符。</li></ul>
</td>
</tr>
<tr id="row172711411103110"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p82717119318"><a name="p82717119318"></a><a name="p82717119318"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul20271131114318"></a><a name="ul20271131114318"></a><ul id="ul20271131114318"><li>目标数据库实例的运行状态必须正常，若关系型数据库实例是主备实例，复制状态也必须正常。</li><li>目标数据库实例必须有足够的磁盘空间。</li><li>目标数据库的时区设置必须与源数据库一致。</li></ul>
</td>
</tr>
</tbody>
</table>


# MySQL-\>GaussDB\(DWS\)<a name="drs_04_0105"></a>

## 使用技巧（需要人为配合）<a name="section98341051155812"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1691943218231)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。
    -   由于MySQL固有特点限制，CPU资源紧张时，存储引擎为Tokudb的表，读取速度可能下降至10%。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section1691943218231"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table371033505819"></a>
<table><thead align="left"><tr id="row13710133535812"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p1671013565815"><a name="p1671013565815"></a><a name="p1671013565815"></a><strong id="b671116352584"><a name="b671116352584"></a><a name="b671116352584"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p17111735205818"><a name="p17111735205818"></a><a name="p17111735205818"></a><strong id="b11711163565817"><a name="b11711163565817"></a><a name="b11711163565817"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row37111335155813"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p8711183585818"><a name="p8711183585818"></a><a name="p8711183585818"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul2711183512589"></a><a name="ul2711183512589"></a><ul id="ul2711183512589"><li><a href="#table2264214592">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>相互关联的数据对象要确保同时同步，避免因关联对象缺失，导致同步失败。常见的关联关系：索引引用表等。</li><li>不支持外键级联操作。</li><li>网络中断在30秒内恢复的，不影响<span id="text27116359585"><a name="text27116359585"></a><a name="text27116359585"></a>实时同步</span>，如果超过30秒，则会导致同步任务失败。</li><li>不支持源数据库进行恢复操作。</li><li>索引同步不区分索引类型，同步到目标数据库都是默认的索引类型。</li><li>目标数据库与源数据库字符集不一致可能会导致同步后数据不一致或者同步失败。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li><li>数据类型不兼容时，可能引起同步失败。</li><li>源库为RDS for MySQL实例时，不支持带有TDE特性并建立具有加密功能表。</li><li>源库为RDS for MySQL实例时，支持源端多张表对<span id="text2308141819317"><a name="text2308141819317"></a><a name="text2308141819317"></a>GaussDB(DWS)</span>一张表的映射。详细操作可参考<a href="https://support.huaweicloud.com/usermanual-drs/drs_03_0040.html" target="_blank" rel="noopener noreferrer">MySQL数据库到DWS同步实例（多对一场景）</a>。</li></ul>
</td>
</tr>
<tr id="row27121435185818"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1071243555815"><a name="p1071243555815"></a><a name="p1071243555815"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul9712103585817"></a><a name="ul9712103585817"></a><ul id="ul9712103585817"><li><span id="text1871210355581"><a name="text1871210355581"></a><a name="text1871210355581"></a>实时同步</span>过程中，若源库为RDS时，支持修改端口，修改之后同步任务失败，需要通过重试后继续进行同步。</li><li><span id="text37120351585"><a name="text37120351585"></a><a name="text37120351585"></a>实时同步</span>过程中，若源库为非RDS时，不支持修改端口。</li><li><span id="text177121635145810"><a name="text177121635145810"></a><a name="text177121635145810"></a>实时同步</span>过程中，不支持IP、账号、密码修改。</li><li>增量同步过程中，支持部分DDL操作。<a name="ul103341230182215"></a><a name="ul103341230182215"></a><ul id="ul103341230182215"><li>不支持 DROP_DATABASE、DROP_TABLE、TRUNCATE_TABLE、CREATE_VIEW、DROP_VIEW。</li><li>不支持使用Online DDL。</li><li>支持创建表，例如 ：<pre class="codeblock" id="codeblock191811018193710"><a name="codeblock191811018193710"></a><a name="codeblock191811018193710"></a>create table `ddl_test` (id int, c1 varchar(25), primary key(id));
create table `ddl_test_gho` like `ddl_test`;</pre>
</li><li>支持表的重命名，源表和目标表必须都在对象选择里面，例如：<pre class="codeblock" id="codeblock66961829183712"><a name="codeblock66961829183712"></a><a name="codeblock66961829183712"></a>rename table `ddl_test` to `ddl_test_new`;</pre>
</li><li>支持表字段的增和改，不支持删列，例如：<pre class="codeblock" id="codeblock181421335153719"><a name="codeblock181421335153719"></a><a name="codeblock181421335153719"></a>alter table `ddl_test` add column `c2` varchar(25); 
alter table `ddl_test` modify column `c1` varchar(50);
alter table `ddl_test` alter c1 set default 'xxx';</pre>
</li><li>支持修改表索引，例如：<pre class="codeblock" id="codeblock3289184533714"><a name="codeblock3289184533714"></a><a name="codeblock3289184533714"></a>alter table `ddl_test` drop primary key; 
alter table `ddl_test` add primary key(id); 
alter table `ddl_test` add index  `ddl_test_uk`(id);
alter table `ddl_test` drop index `ddl_test_uk`;</pre>
</li><li>表级同步支持增加列、修改列、增加主键和普通索引。多对一情况下执行colunm重命名操作，必须停业务操作，不然会有数据不一致的风险，例如：<pre class="codeblock" id="codeblock18761135514016"><a name="codeblock18761135514016"></a><a name="codeblock18761135514016"></a>alter table `ddl_test` modify column `c1` varchar(50);</pre>
</li><li>库级同步支持新建表、rename表、增加列、修改列、增加主键和普通索引。</li><li>新增和修改表名、列名、索引名时不能超出63字符，否则任务会失败。</li><li>源库无主键表增加主键的时候，必须含有第一列，否则任务会失败。</li></ul>
</li><li>不支持强制清理binlog，否则会导致同步任务失败。</li><li>建议将expire_log_day参数设置在合理的范围，确保恢复时断点处的binlog尚未过期，以保证服务中断后的顺利恢复。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section86695405239"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table2264214592"></a>
<table><thead align="left"><tr id="row162611225916"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p42611210591"><a name="p42611210591"></a><a name="p42611210591"></a><strong id="b92622105916"><a name="b92622105916"></a><a name="b92622105916"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p42615275916"><a name="p42615275916"></a><a name="p42615275916"></a><strong id="b1926182155915"><a name="b1926182155915"></a><a name="b1926182155915"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row22613216597"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p226192115916"><a name="p226192115916"></a><a name="p226192115916"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1626182135910"></a><a name="ul1626182135910"></a><ul id="ul1626182135910"><li>源数据库帐户需要具备如下权限：SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</li><li>目标数据库帐号必须具有每张表的如下权限：INSERT、SELECT、UPDATE、DELETE、CONNECT、CREATE、REFERENCES。</li></ul>
</td>
</tr>
<tr id="row7261727594"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p926124592"><a name="p926124592"></a><a name="p926124592"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul18271128597"></a><a name="ul18271128597"></a><ul id="ul18271128597"><li>支持表、索引、约束（主键、空、非空）的同步，不支持视图、外键、存储过程、触发器、函数、事件、虚拟列的同步。</li><li>不支持的数据类型有：xml、geometry、point、lineString、polygon、geometrycollection、multipoint、multilinestring、multipolygon。</li><li>不支持非MyISAM和非InnoDB表的同步。</li></ul>
</td>
</tr>
<tr id="row162717211599"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p18277217592"><a name="p18277217592"></a><a name="p18277217592"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul92717216592"></a><a name="ul92717216592"></a><ul id="ul92717216592"><li>MySQL源数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议源数据库binlog保存时间越长越好，建议为3天。</li><li>源数据库expire_logs_days参数值为0，可能会导致同步失败。</li><li>必须设置MySQL源数据库的server－id，server－id的取值范围在2－4294967296之间。</li><li>源数据库中的库名不能包含：'.&lt;&gt;/\以及中文等其他非ASCII字符。</li><li>源数据库中的表名、视图名不能包含：'&lt;&gt;/\以及中文等其他非ASCII字符。</li></ul>
</td>
</tr>
<tr id="row192712212594"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p527422598"><a name="p527422598"></a><a name="p527422598"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul2027182125919"></a><a name="ul2027182125919"></a><ul id="ul2027182125919"><li>目标数据库实例的运行状态必须正常。</li><li>目标数据库实例必须有足够的磁盘空间。</li><li>目标数据库的时区设置必须与源数据库一致。</li></ul>
</td>
</tr>
</tbody>
</table>


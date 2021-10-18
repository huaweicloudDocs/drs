# MySQL-\>MySQL<a name="drs_04_0102"></a>

## 使用技巧（需要人为配合）<a name="section98341051155812"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1256917135149)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。
    -   同步无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。
    -   由于MySQL固有特点限制，CPU资源紧张时，存储引擎为Tokudb的表，读取速度可能下降至10%。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。
-   如果涉及多对一场景的同步任务，可参考[多对一的场景约束及操作建议](https://support.huaweicloud.com/drs_faq/drs_16_0120.html)。
-   如果涉及表级汇集的多对一同步任务，则不支持DDL，否则会导致同步全部失败。

## 操作要求<a name="section1256917135149"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table447817192112"></a>
<table><thead align="left"><tr id="row247717122116"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p1448817102113"><a name="p1448817102113"></a><a name="p1448817102113"></a><strong id="b5481417172113"><a name="b5481417172113"></a><a name="b5481417172113"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p1948161716213"><a name="p1948161716213"></a><a name="p1948161716213"></a><strong id="b2481717102115"><a name="b2481717102115"></a><a name="b2481717102115"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row5481117142115"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p248121711219"><a name="p248121711219"></a><a name="p248121711219"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul134813171215"></a><a name="ul134813171215"></a><ul id="ul134813171215"><li><a href="#table63691233102116">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>相互关联的数据对象要确保同时同步，避免因关联对象缺失，导致同步失败。常见的关联关系：视图引用表、视图引用视图、存储过程/函数/触发器引用视图/表、主外键关联表等。</li><li>不支持源数据库恢复到之前时间点的操作(PITR)。</li><li>支持断点续传功能，但是对于无主键的表可能会出现重复插入数据的情况。</li><li>创建同步任务时，不允许将目标库设为只读。</li><li>当前仅MySQL-&gt;MySQL的同步支持多对一任务同步，进行表级多对一同步时，源库不允许存在无主键表。</li><li>源库和目标库是相同的RDS实例时，不支持没有库映射的<span id="text134841714211"><a name="text134841714211"></a><a name="text134841714211"></a>实时同步</span>。</li><li>源库不允许存在与目标库同名的无主键表。</li><li>不支持目标数据库恢复到全量同步时间段范围内的PITR操作。</li><li>不支持外键级联操作。</li><li>进行多对一同步任务时，若多个同步任务同步同一张表，则在任务启动之后，系统会自动创建一个父任务来关联多个同步任务，父任务的命名规则为“DRS-Group-(目标库实例名)”。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li><li>源库和目标库为RDS for MySQL实例时，不支持带有TDE特性并建立具有加密功能表。</li></ul>
</td>
</tr>
<tr id="row1548151702116"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p114811742114"><a name="p114811742114"></a><a name="p114811742114"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul15482178216"></a><a name="ul15482178216"></a><ul id="ul15482178216"><li><span id="text649161718215"><a name="text649161718215"></a><a name="text649161718215"></a>实时同步</span>过程中，如果修改了源库或者目标库的用户名、密码，会导致同步任务失败，需要在数据复制服务控制台将上述信息重新修改正确，然后重试任务可继续进行<span id="text3494175218"><a name="text3494175218"></a><a name="text3494175218"></a>实时同步</span>。一般情况下不建议在同步过程中修改上述信息。</li><li><span id="text184911173211"><a name="text184911173211"></a><a name="text184911173211"></a>实时同步</span>过程中，如果修改了源库或者目标库端口，会导致同步任务失败。针对该情况，数据复制服务提供不同的处理机制。<a name="ul20491217132116"></a><a name="ul20491217132116"></a><ul id="ul20491217132116"><li>对于源库端口，需要在数据复制服务控制台修改为正确的端口，然后重试任务可继续进行<span id="text74991715217"><a name="text74991715217"></a><a name="text74991715217"></a>实时同步</span>。</li><li>对于目标库端口，系统自动更新为正确的端口，需要重试任务即可进行同步。<p id="p144914179219"><a name="p144914179219"></a><a name="p144914179219"></a>一般情况下不建议在同步过程中修改端口。</p>
</li></ul>
</li><li><span id="text1949517152113"><a name="text1949517152113"></a><a name="text1949517152113"></a>实时同步</span>过程中，如果源库为非本云关系型数据库实例，不支持修改IP地址。如果是本云关系型数据库实例，对于因修改IP地址导致同步任务失败的情况，系统自动更新为正确的IP地址，需要重试任务可继续进行同步。一般情况下，不建议修改IP地址。</li><li>不支持强制清理binlog，否则会导致同步任务失败。</li><li>为了保持数据一致性，不允许对正在同步中的目标数据库进行修改操作(包括但不限于DDL、DML操作)。</li><li>当在全量同步过程中，对MyISAM表执行修改操作时，可能造成数据不一致。</li><li>表级同步时，增量同步过程中只支持表的DDL操作。</li><li>表级同步时，增量同步过程中不建议对表进行重命名操作。</li><li>表级同步时，增量同步过程支持使用Online DDL，可参考<a href="https://support.huaweicloud.com/drs_faq/drs_16_1124.html" target="_blank" rel="noopener noreferrer">DRS实时同步支持使用Online DDL工具吗</a>。</li><li>建议将expire_log_day参数设置在合理的范围，确保恢复时断点处的binlog尚未过期，以保证服务中断后的顺利恢复。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section138481227181416"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table63691233102116"></a>
<table><thead align="left"><tr id="row1337063362116"><th class="cellrowborder" valign="top" width="18.29%" id="mcps1.2.3.1.1"><p id="p337016333210"><a name="p337016333210"></a><a name="p337016333210"></a><strong id="b2037083302110"><a name="b2037083302110"></a><a name="b2037083302110"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.71000000000001%" id="mcps1.2.3.1.2"><p id="p13370153317219"><a name="p13370153317219"></a><a name="p13370153317219"></a><strong id="b3370183312215"><a name="b3370183312215"></a><a name="b3370183312215"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row0370143362116"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p13370433162116"><a name="p13370433162116"></a><a name="p13370433162116"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul1237019330212"></a><a name="ul1237019330212"></a><ul id="ul1237019330212"><li>源数据库帐户需要具备如下权限：<p id="p31857299557"><a name="p31857299557"></a><a name="p31857299557"></a>SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</p>
</li><li>提供的目标数据库帐号必须拥有如下权限：<p id="p1899731185511"><a name="p1899731185511"></a><a name="p1899731185511"></a>SELECT、CREATE、DROP、DELETE、INSERT、UPDATE。</p>
<p id="p4571727145517"><a name="p4571727145517"></a><a name="p4571727145517"></a>RDS for MySQL实例的root帐户默认已具备上述权限。</p>
</li></ul>
</td>
</tr>
<tr id="row73701233102115"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p1937018335211"><a name="p1937018335211"></a><a name="p1937018335211"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul23701433152114"></a><a name="ul23701433152114"></a><ul id="ul23701433152114"><li>支持表、主键索引、唯一索引、普通索引、存储过程、视图、函数的同步，不支持事件、触发器的同步。</li></ul>
<a name="ul1137013392118"></a><a name="ul1137013392118"></a><ul id="ul1137013392118"><li>库映射时源库中不允许存在存储过程、视图、函数对象。</li><li>映射的库中不允许存在除表外的对象且在同步过程中不允许创建这些对象，否则会导致同步任务失败。</li><li>不支持非MyISAM和非InnoDB表的同步。</li><li>不支持已选择的表与未选择的表之间互相rename的DDL操作，否则会导致同步任务失败。</li></ul>
</td>
</tr>
<tr id="row3370533132115"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p637193313217"><a name="p637193313217"></a><a name="p637193313217"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul93711333192113"></a><a name="ul93711333192113"></a><ul id="ul93711333192113"><li>MySQL源数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议源数据库binlog保存时间越长越好，建议为3天。</li><li>源数据库expire_logs_days参数值为0，可能会导致同步失败。</li><li>增量同步时，必须设置MySQL源数据库的server_id。如果源数据库版本小于或等于MySQL5.6，server_id的取值范围在2－4294967296之间；如果源数据库版本大于或等于MySQL5.7，server_id的取值范围在1－4294967296之间。</li><li>源数据库中的库名不能包含：'&lt;`&gt;/\"以及非ASCII字符。</li><li>源数据库中的表名、视图名不能包含：'&lt;&gt;/\"以及非ASCII字符。</li><li>源数据库中的库名和库映射的名称不允许为ib_logfile。</li><li>不支持非MyISAM和非InnoDB的表同步到RDS。</li><li>数据库映射时，源库中存在视图、存储过程等对象，可能会导致<span id="text937219339211"><a name="text937219339211"></a><a name="text937219339211"></a>实时同步</span>失败。</li></ul>
</td>
</tr>
<tr id="row837213333212"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p12372143392116"><a name="p12372143392116"></a><a name="p12372143392116"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul23721633192118"></a><a name="ul23721633192118"></a><ul id="ul23721633192118"><li>目标数据库实例的运行状态必须正常，若数据库实例是主备实例，复制状态也必须正常。</li><li>目标数据库实例必须有足够的磁盘空间。</li><li>除了MySQL系统数据库之外，当目标库和源库同名时，目标数据库中若存在与源库同名的表，则表结构必须与源库保持一致。</li><li>目标数据库的字符集必须与源数据库一致。</li><li>目标数据库的时区设置必须与源数据库一致。</li><li>DRS同步时会有大量数据写入目标库，目标库max_allowed_packet 参数过小会导致无法写入，建议将目标库max_allowed_packet参数值设置为大于100MB。</li><li>同步的对象中包含引擎为MyISAM的表，则目标数据库sql_mode不能包含no_engine_substitution参数，否则可能会导致同步失败。</li><li>映射到目标库中的库名不能包含：“.”、 “&lt;”、“&gt;”、“”、和“'”。</li></ul>
</td>
</tr>
</tbody>
</table>


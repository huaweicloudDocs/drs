# DDM-\>Oracle<a name="drs_04_0119"></a>

## 使用技巧（需要人为配合）<a name="section449714073815"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1691943218231)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section1691943218231"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table88114333143"></a>
<table><thead align="left"><tr id="row581153310145"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p6811173316140"><a name="p6811173316140"></a><a name="p6811173316140"></a><strong id="b481283316141"><a name="b481283316141"></a><a name="b481283316141"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p13812533121416"><a name="p13812533121416"></a><a name="p13812533121416"></a><strong id="b13812163313148"><a name="b13812163313148"></a><a name="b13812163313148"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row15813533111413"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p10813183318143"><a name="p10813183318143"></a><a name="p10813183318143"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul98136337142"></a><a name="ul98136337142"></a><ul id="ul98136337142"><li><a href="#table13451741151419">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>源数据库中存在主键重复的数据时, 直接同步将导致目标库数据比源库少, 请务必检查并订正数据后启动同步。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li><li>数据类型不兼容时，可能引起同步失败。</li></ul>
</td>
</tr>
<tr id="row4813933151416"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p9813163318143"><a name="p9813163318143"></a><a name="p9813163318143"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1581343351414"></a><a name="ul1581343351414"></a><ul id="ul1581343351414"><li>增量同步过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>增量同步过程中，若需要对源库需要同步的表结构进行修改, 则用户必须在目标库同步修改表结构。</li><li>增量同步场景下，不支持源数据库进行恢复操作。</li><li>同步过程中不支持DDL操作。</li><li>创建任务后，不支持增加逻辑库或修改旧逻辑库关联新的RDS，否则会导致同步任务失败。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section86695405239"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table13451741151419"></a>
<table><thead align="left"><tr id="row1546144115146"><th class="cellrowborder" valign="top" width="18.35%" id="mcps1.2.3.1.1"><p id="p1146841151414"><a name="p1146841151414"></a><a name="p1146841151414"></a><strong id="b184614131416"><a name="b184614131416"></a><a name="b184614131416"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.65%" id="mcps1.2.3.1.2"><p id="p174612411146"><a name="p174612411146"></a><a name="p174612411146"></a><strong id="b1646134181410"><a name="b1646134181410"></a><a name="b1646134181410"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row8461641171413"><td class="cellrowborder" valign="top" width="18.35%" headers="mcps1.2.3.1.1 "><p id="p20465419144"><a name="p20465419144"></a><a name="p20465419144"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.65%" headers="mcps1.2.3.1.2 "><a name="ul1946741191416"></a><a name="ul1946741191416"></a><ul id="ul1946741191416"><li>源物理分片数据库帐户需要具备如下权限：SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</li></ul>
<a name="ul6461141121416"></a><a name="ul6461141121416"></a><ul id="ul6461141121416"><li>提供的目标数据库帐号必须具有每张表的如下权限：ALTER ANY INDEX, ALTER ANY TABLE, ALTER SESSION, COMMENT ANY TABLE, CREATE ANY INDEX, CREATE ANY TABLE, CREATE SESSION, DELETE ANY TABLE, DROP ANY TABLE, INSERT ANY TABLE, SELECT ANY TABLE, SELECT ANY DICTIONARY, SELECT ANY TRANSACTION, UPDATE ANY TABLE, ANALYZE ANY和RESOURCE。</li></ul>
</td>
</tr>
<tr id="row154614181415"><td class="cellrowborder" valign="top" width="18.35%" headers="mcps1.2.3.1.1 "><p id="p1946341101411"><a name="p1946341101411"></a><a name="p1946341101411"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.65%" headers="mcps1.2.3.1.2 "><a name="ul246941191416"></a><a name="ul246941191416"></a><ul id="ul246941191416"><li>支持源库数据同步。</li><li>源库表结构仅支持全量同步。</li><li>不支持同步表结构、索引、约束之外的数据库对象。</li></ul>
</td>
</tr>
<tr id="row1347114112141"><td class="cellrowborder" valign="top" width="18.35%" headers="mcps1.2.3.1.1 "><p id="p11471641191416"><a name="p11471641191416"></a><a name="p11471641191416"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.65%" headers="mcps1.2.3.1.2 "><a name="ul747184141414"></a><a name="ul747184141414"></a><ul id="ul747184141414"><li>源物理分片数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，binlog保存时间越长越好，建议为3天。</li><li>增量同步时，必须设置MySQL源数据库的server_id。如果源数据库版本小于或等于MySQL5.6，server_id的取值范围在2－4294967296之间；如果源数据库版本大于或等于MySQL5.7，server_id的取值范围在1－4294967296之间。</li><li>源分库分表中间件中的库名、表名不能包含：'&lt;&gt;/\以及非ASCII字符。</li><li>源物理分片数据库建议开启skip-name-resolve，减少连接超时的可能性。</li><li>源物理分片数据库的GTID状态建议为开启状态。</li><li>源物理分片数据库不支持枚举类型和set集合类型的<span id="text14481541181412"><a name="text14481541181412"></a><a name="text14481541181412"></a>实时同步</span>。</li><li>源数据库表名、字段名不能超过30个字符。</li><li>不支持同步无主键表。</li><li>源库中需要同步的数据库具有RESOURCE权限。</li><li>源库的timestamp列的默认值，需要在目标库的合理取值内，否则会导致同步失败。</li></ul>
</td>
</tr>
<tr id="row7481741131418"><td class="cellrowborder" valign="top" width="18.35%" headers="mcps1.2.3.1.1 "><p id="p7486415147"><a name="p7486415147"></a><a name="p7486415147"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.65%" headers="mcps1.2.3.1.2 "><a name="ul34819416148"></a><a name="ul34819416148"></a><ul id="ul34819416148"><li>目标数据库实例的运行状态必须正常。</li><li>目标数据库实例必须有足够的磁盘空间。</li><li>目标数据库的时区设置必须与源数据库一致。</li><li>目标库中需要同步的数据库（用户）具有RESOURCE权限。</li></ul>
</td>
</tr>
</tbody>
</table>


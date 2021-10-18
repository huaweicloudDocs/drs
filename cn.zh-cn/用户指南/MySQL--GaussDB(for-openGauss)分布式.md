# MySQL-\>GaussDB\(for openGauss\)分布式<a name="drs_04_0104"></a>

## 使用技巧（需要人为配合）<a name="section1172211417013"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section972314419010)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。
    -   由于MySQL固有特点限制，CPU资源紧张时，存储引擎为Tokudb的表，读取速度可能下降至10%。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section972314419010"></a>

针对一些无法预知或认为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table572454117016"></a>
<table><thead align="left"><tr id="row1772410414012"><th class="cellrowborder" valign="top" width="18.060000000000002%" id="mcps1.2.3.1.1"><p id="p57246419020"><a name="p57246419020"></a><a name="p57246419020"></a><strong id="b1172410419012"><a name="b1172410419012"></a><a name="b1172410419012"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.94%" id="mcps1.2.3.1.2"><p id="p187249411202"><a name="p187249411202"></a><a name="p187249411202"></a><strong id="b17724741906"><a name="b17724741906"></a><a name="b17724741906"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row187241341104"><td class="cellrowborder" valign="top" width="18.060000000000002%" headers="mcps1.2.3.1.1 "><p id="p1724144117017"><a name="p1724144117017"></a><a name="p1724144117017"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.94%" headers="mcps1.2.3.1.2 "><a name="ul1572417415011"></a><a name="ul1572417415011"></a><ul id="ul1572417415011"><li><a href="#table97255414015">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>不支持外键级联操作。</li><li>网络中断在30秒内恢复的，不影响实时同步，如果超过30秒，则会导致同步任务失败。</li><li>不支持源数据库进行恢复操作。</li><li>目标数据库与源数据库字符集不一致可能会导致同步后数据不一致或者同步失败。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li><li>数据类型不兼容时，可能引起同步失败。</li><li>源库表同步至目标库后分布方式为哈希分布，暂不支持复制分布。</li><li>源库为RDS for MySQL实例时，不支持带有TDE特性并建立具有加密功能表。</li></ul>
</td>
</tr>
<tr id="row172419411003"><td class="cellrowborder" valign="top" width="18.060000000000002%" headers="mcps1.2.3.1.1 "><p id="p672410411019"><a name="p672410411019"></a><a name="p672410411019"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.94%" headers="mcps1.2.3.1.2 "><a name="ul17724154119017"></a><a name="ul17724154119017"></a><ul id="ul17724154119017"><li>源库和目标库均相同的任务不允许出现重复同步的情况，如：A任务和B任务同时将源库的同一张表的实时同步到目标库的同一张表中，可能导致数据不一致和同步失败。</li><li>增量同步过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>增量同步过程中，不支持源库DDL的复制，若需要对源库需要同步的表结构进行修改, 则用户必须在目标库同步修改表结构，否则DDL相关的数据也将无法同步至目标库。</li><li>增量同步场景下，不支持源数据库进行恢复操作。</li><li>任务启动、任务全量同步阶段，不建议做删除类型的DDL操作，可能会引起任务失败。</li><li>不支持同步无主键表，若选择同步的表中存在无主键表，则同步失败。</li><li>不支持两阶段事务。</li><li>不支持暂停正在进行的同步任务。</li><li>不支持对同步结果进行数据对比。</li><li>不支持数据加工。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section472515411705"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table97255414015"></a>
<table><thead align="left"><tr id="row672511411407"><th class="cellrowborder" valign="top" width="18.42%" id="mcps1.2.3.1.1"><p id="p7725124112015"><a name="p7725124112015"></a><a name="p7725124112015"></a><strong id="b147258411507"><a name="b147258411507"></a><a name="b147258411507"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.58%" id="mcps1.2.3.1.2"><p id="p1972574116014"><a name="p1972574116014"></a><a name="p1972574116014"></a><strong id="b1272518414017"><a name="b1272518414017"></a><a name="b1272518414017"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row14725124117018"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p272518411708"><a name="p272518411708"></a><a name="p272518411708"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul7725164116015"></a><a name="ul7725164116015"></a><ul id="ul7725164116015"><li>源物理分片数据库帐户需要具备如下权限：SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</li></ul>
<a name="ul1272514411704"></a><a name="ul1272514411704"></a><ul id="ul1272514411704"><li>提供的目标库GaussDB(for openGauss)账户需要具备如下权限：<a name="ol672618411201"></a><a name="ol672618411201"></a><ol id="ol672618411201"><li>database权限要求：<p id="p17726341507"><a name="p17726341507"></a><a name="p17726341507"></a>需要具备database的create、connect权限。</p>
<p id="p187267411007"><a name="p187267411007"></a><a name="p187267411007"></a>授权语句：grant create,connect on database &lt;database&gt; to &lt;user&gt;;</p>
</li><li>schema权限要求：<p id="p872619411308"><a name="p872619411308"></a><a name="p872619411308"></a>需要具备schema的create、usage权限。</p>
<p id="p972617411409"><a name="p972617411409"></a><a name="p972617411409"></a>授权语句：grant create,usage on schema &lt;schema}&gt; to &lt;user&gt;;</p>
</li><li>table权限要求：<p id="p177268412016"><a name="p177268412016"></a><a name="p177268412016"></a>需要具备schema下所有table的DML权限。可使用以下两种方式授权：</p>
<p id="p15726174115017"><a name="p15726174115017"></a><a name="p15726174115017"></a>方式一：</p>
<p id="p372654116010"><a name="p372654116010"></a><a name="p372654116010"></a>给schema下所有table授权：grant select,update,insert,delete on all tables in schema &lt;schema&gt; to &lt;user&gt;;</p>
<p id="p197261841903"><a name="p197261841903"></a><a name="p197261841903"></a>方式二：</p>
<p id="p572612413017"><a name="p572612413017"></a><a name="p572612413017"></a>给schema下的指定table授权：grant select,update,insert,delete on table &lt;schema.table&gt; to &lt;user&gt;;</p>
</li></ol>
</li></ul>
</td>
</tr>
<tr id="row07264411109"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p1272644117010"><a name="p1272644117010"></a><a name="p1272644117010"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul87263417013"></a><a name="ul87263417013"></a><ul id="ul87263417013"><li>仅支持同步表，不支持同步存储过程等其他数据库对象。</li><li>仅支持同步有主键表，不支持同步无主键表。</li><li>增量同步不支持同步DDL。</li><li>不支持同步MySQL含虚拟列的表。</li></ul>
<a name="ul181372023125011"></a><a name="ul181372023125011"></a><ul id="ul181372023125011"><li>不支持的数据类型有：xml、geometry、point、lineString、polygon、geometrycollection、multipoint、multilinestring、multipolygon。</li><li>不支持非MyISAM和非InnoDB表的同步。</li></ul>
</td>
</tr>
<tr id="row1872612414013"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p572674111015"><a name="p572674111015"></a><a name="p572674111015"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul19726741103"></a><a name="ul19726741103"></a><ul id="ul19726741103"><li>源物理分片数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，binlog保存时间越长越好，建议为3天。</li><li>源数据库expire_logs_days参数值为0，可能会导致同步失败。</li><li>增量同步时，必须设置MySQL源数据库的server_id。MySQL5.7，server_id的取值范围在1－4294967296之间。</li><li>源数据库库名、表名不能包含：'&lt;&gt;/\以及非ASCII字符。</li></ul>
</td>
</tr>
<tr id="row272744119020"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p4727341409"><a name="p4727341409"></a><a name="p4727341409"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><a name="ul117274411407"></a><a name="ul117274411407"></a><ul id="ul117274411407"><li>目标数据库实例的运行状态必须正常。</li><li>目标数据库实例必须有足够的磁盘空间。</li><li>目标数据库的时区设置必须与源数据库一致。</li><li>任务配置的映射数据库必须在目标库已经存在。</li><li>目标库连接用户需要有指定database的CREATE、CONNECT、TEMPORARY权限。</li><li>如果同步的模式和表在目标库已存在，要求模式和表的OWNER必须是目标库连接用户。</li></ul>
</td>
</tr>
</tbody>
</table>


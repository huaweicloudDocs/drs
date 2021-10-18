# DDM-\>MySQL<a name="drs_04_0453"></a>

## 使用技巧（需要人为配合）<a name="section449714073815"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1691943218231)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。
    -   同步无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section1691943218231"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table1578599134712"></a>
<table><thead align="left"><tr id="row878613910470"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p16786199114718"><a name="p16786199114718"></a><a name="p16786199114718"></a><strong id="b177862916476"><a name="b177862916476"></a><a name="b177862916476"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p578629124716"><a name="p578629124716"></a><a name="p578629124716"></a><strong id="b67868919478"><a name="b67868919478"></a><a name="b67868919478"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row0786195476"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1978713914710"><a name="p1978713914710"></a><a name="p1978713914710"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1678769104713"></a><a name="ul1678769104713"></a><ul id="ul1678769104713"><li><a href="#table6301182794719">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>支持断点续传功能，在主机系统崩溃的情况下，对于无主键的表可能会出现重复插入数据的情况。</li><li>创建同步任务时，不允许同步任务将目标库设为只读。</li><li>暂不支持跨VPC场景的<span id="text1278711919478"><a name="text1278711919478"></a><a name="text1278711919478"></a>实时同步</span>。</li><li>源数据库中存在主键或唯一键重复的数据时, 直接同步将导致目标库数据比源库少, 请务必检查并订正数据后启动同步。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li><li>数据类型不兼容时，可能引起同步失败。</li><li>目标库为RDS for MySQL实例时，不支持带有TDE特性并建立具有加密功能表。</li></ul>
</td>
</tr>
<tr id="row1278714964718"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1578739114718"><a name="p1578739114718"></a><a name="p1578739114718"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul0787594478"></a><a name="ul0787594478"></a><ul id="ul0787594478"><li>同步过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>增量同步过程中，不允许对源库需要同步的表结构进行修改。</li><li>增量同步场景下，不支持源数据库进行恢复操作</li><li>同步过程中不支持DDL操作。</li><li>创建任务后，不支持增加逻辑库或修改旧逻辑库关联新的RDS，否则会导致同步任务失败。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section86695405239"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table6301182794719"></a>
<table><thead align="left"><tr id="row14302132744712"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p2302027164712"><a name="p2302027164712"></a><a name="p2302027164712"></a><strong id="b1730292724717"><a name="b1730292724717"></a><a name="b1730292724717"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p33021027154712"><a name="p33021027154712"></a><a name="p33021027154712"></a><strong id="b1330262712473"><a name="b1330262712473"></a><a name="b1330262712473"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row13021277476"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p123021227134711"><a name="p123021227134711"></a><a name="p123021227134711"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1430282704717"></a><a name="ul1430282704717"></a><ul id="ul1430282704717"><li>源物理分片数据库帐户需要具备如下权限：SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</li></ul>
<a name="ul183021227124718"></a><a name="ul183021227124718"></a><ul id="ul183021227124718"><li>提供的目标数据库帐号必须拥有如下权限：SELECT、CREATE、DROP、DELETE、INSERT、UPDATE。RDS for MySQL实例的root帐户默认已具备上述权限。</li></ul>
</td>
</tr>
<tr id="row1930216279479"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p530202704713"><a name="p530202704713"></a><a name="p530202704713"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1302102719475"></a><a name="ul1302102719475"></a><ul id="ul1302102719475"><li>全量同步支持数据、表结构和索引的同步。</li><li>源库不允许存在拆分键为timestamp类型的表。</li><li>源表的分库分表键要加到目标表的主键和唯一键中（也就是目标表的主键和唯一键中的列应该包含源表的分片列），避免数据冲突出现数据不一致问题。</li></ul>
</td>
</tr>
<tr id="row630352716475"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1930317275474"><a name="p1930317275474"></a><a name="p1930317275474"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1030310271472"></a><a name="ul1030310271472"></a><ul id="ul1030310271472"><li>MySQL源数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议源数据库binlog保存时间越长越好，建议为3天。</li><li>增量同步时，必须设置MySQL源数据库的server_id。如果源数据库版本小于或等于MySQL5.6，server_id的取值范围在2－4294967296之间；如果源数据库版本大于或等于MySQL5.7，server_id的取值范围在1－4294967296之间。</li><li>源分库分表中间件中的库名、表名不能包含：'&lt;&gt;/\以及非ASCII字符。</li><li>MySQL源数据库建议开启skip-name-resolve，减少连接超时的可能性。</li><li>源数据库GTID状态建议为开启状态。</li></ul>
</td>
</tr>
<tr id="row2303327144718"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p9303152764714"><a name="p9303152764714"></a><a name="p9303152764714"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul530322712477"></a><a name="ul530322712477"></a><ul id="ul530322712477"><li>目标数据库为自建MySQL。</li><li>目标数据库实例必须有足够的磁盘空间。</li><li>除了MySQL系统数据库之外，当目标库和源库同名时，目标数据库中若存在与源库同名的表，则表结构必须与源库保持一致。</li><li>目标数据库的字符集必须与源数据库一致。</li><li>目标数据库的时区设置必须与源数据库一致。</li><li>DRS同步时会有大量数据写入目标库，目标库max_allowed_packet 参数过小会导致无法写入，建议将目标库max_allowed_packet参数值设置为大于100MB。</li></ul>
</td>
</tr>
</tbody>
</table>


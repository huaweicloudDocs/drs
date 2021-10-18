# MySQL分库分表-\>DDM<a name="drs_04_0094"></a>

## 使用技巧（需要人为配合）<a name="section182303625619"></a>

-   如果您使用的是全量迁移模式（离线迁移），确保源和目标数据库无业务写入，保证迁移前后数据一致。

-   如果您使用的是全量+增量迁移模式（在线迁移），支持在源数据库有业务数据写入的情况下进行迁移，推荐**提前2-3天**启动任务，并配合如下使用技巧和对应场景的[操作要求](#section83714237916)，以确保顺利迁移。
    -   全量迁移

        基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行迁移任务，相对静态的数据，迁移时复杂度将会降低。

        -   全量迁移会对源数据库有一定的访问压力。
        -   迁移无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
        -   正在迁移的数据被其他事务长时间锁死，可能导致读数据超时。
        -   由于MySQL固有特点限制，CPU资源紧张时，存储引擎为Tokudb的表，读取速度可能下降至10%。

    -   数据对比

        建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。



## 操作要求<a name="section83714237916"></a>

针对一些无法预知或人为因素及环境突变导致迁移失败的情况，数据复制服务提供以下常见的操作限制，供您在迁移过程中参考。

**表 1**  操作要求

<a name="table153851183278"></a>
<table><thead align="left"><tr id="row1938513181279"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p53857182279"><a name="p53857182279"></a><a name="p53857182279"></a><strong id="b1538531818271"><a name="b1538531818271"></a><a name="b1538531818271"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p14385818162715"><a name="p14385818162715"></a><a name="p14385818162715"></a><strong id="b1138610183279"><a name="b1138610183279"></a><a name="b1138610183279"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row16386418162711"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1138618188273"><a name="p1138618188273"></a><a name="p1138618188273"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul11386121811275"></a><a name="ul11386121811275"></a><ul id="ul11386121811275"><li><a href="#table66924259274">表2</a>中的环境要求均不允许在迁移过程中修改，直至迁移结束。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建迁移任务。</li><li>数据类型不兼容时，可能引起迁移失败。</li></ul>
</td>
</tr>
<tr id="row1386151819272"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p7386101814278"><a name="p7386101814278"></a><a name="p7386101814278"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1838641842710"></a><a name="ul1838641842710"></a><ul id="ul1838641842710"><li>迁移过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>迁移过程中，不允许对源库需要迁移的表结构进行修改。</li><li>增量迁移场景下，不支持源数据库进行恢复操作。</li><li>选择表级对象迁移时，增量迁移过程中不建议对表进行重命名操作。</li><li>在任务启动、任务全量迁移阶段，不建议对源数据库做删除类型的DDL操作，这样可能会引起任务迁移失败。</li><li>建议将expire_log_day参数设置在合理的范围，确保恢复时断点处的binlog尚未过期，以保证服务中断后的顺利恢复。</li><li>如果源数据库为自建库，并且安装了Percona Server for MySQL 5.6.x或Percona Server for MySQL 5.7.x时，内存管理器必须使用Jemalloc库，以避免因系统表频繁查询带来的内存回收不及时，并最终导致数据库Out of Memory问题。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section1645253517920"></a>

实时迁移对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table66924259274"></a>
<table><thead align="left"><tr id="row1469222532715"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p7692132512271"><a name="p7692132512271"></a><a name="p7692132512271"></a><strong id="b1069212252273"><a name="b1069212252273"></a><a name="b1069212252273"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p1169242562710"><a name="p1169242562710"></a><a name="p1169242562710"></a><strong id="b16692132510278"><a name="b16692132510278"></a><a name="b16692132510278"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row196934250279"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p4693192517271"><a name="p4693192517271"></a><a name="p4693192517271"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul9693192502710"></a><a name="ul9693192502710"></a><ul id="ul9693192502710"><li><strong id="b869322516275"><a name="b869322516275"></a><a name="b869322516275"></a>全量迁移最小权限要求：</strong><a name="ul269315251276"></a><a name="ul269315251276"></a><ul id="ul269315251276"><li>源物理分片数据库帐户需要具备如下权限：SELECT、SHOW VIEW、EVENT。</li><li>目标中间件帐户需要具备以下基本权限：CREATE、DROP、ALTER、 INDEX、 INSERT、DELETE、 UPDATE、 SELECT， 同时必须具备扩展权限:全表Select权限。</li><li>目标中间件帐户必须具备对所迁移数据库的权限。</li></ul>
</li><li><strong id="b1569392532714"><a name="b1569392532714"></a><a name="b1569392532714"></a>全量+增量迁移最小权限要求：</strong><a name="ul86930257273"></a><a name="ul86930257273"></a><ul id="ul86930257273"><li>源物理分片数据库帐户需要具备如下权限：SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</li><li>目标中间件帐户需要具备以下基本权限：CREATE、DROP、ALTER、 INDEX、 INSERT、DELETE、 UPDATE、 SELECT， 同时必须具备扩展权限:：全表Select权限。</li><li>目标中间件帐户必须具备对所迁移数据库的权限。</li></ul>
</li></ul>
</td>
</tr>
<tr id="row369382518277"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p5693825182717"><a name="p5693825182717"></a><a name="p5693825182717"></a>迁移对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul11693152513276"></a><a name="ul11693152513276"></a><ul id="ul11693152513276"><li>目前只支持迁移源库的数据，不支持迁移源库表结构及其他数据库对象。</li><li>用户需要在目标库根据源端逻辑库的表结构，自行在目标库创建对应的表结构及索引。未在目标库创建的对象，视为用户不选择这个对象进行迁移。</li><li>源库在目标库创建的表结构， 必须与源库的表结构完全一致。</li><li>源库为DDM时，则不允许存在拆分键为timestamp类型的表。</li><li>不支持非MyISAM和非InnoDB表的迁移。</li></ul>
</td>
</tr>
<tr id="row166941525152712"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p069402512717"><a name="p069402512717"></a><a name="p069402512717"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul469419257277"></a><a name="ul469419257277"></a><ul id="ul469419257277"><li>增量迁移时，MySQL源数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>增量迁移时，在磁盘空间允许的情况下，建议源数据库binlog保存时间越长越好，建议为3天。</li><li>源数据库expire_logs_days参数值为0，可能会导致迁移失败。</li><li>增量迁移时，必须设置MySQL源数据库的server－id。如果源数据库版本小于或等于MySQL5.6，server－id的取值范围在2－4294967296之间；如果源数据库版本大于或等于MySQL5.7，server－id的取值范围在1－4294967296之间。</li><li>源分库分表中间件中的库名、表名不能包含：'&lt;&gt;/\以及非ASCII字符。</li><li>MySQL源数据库建议开启skip-name-resolve，减少连接超时的可能性。</li><li>源数据库GTID状态建议为开启状态。</li></ul>
</td>
</tr>
<tr id="row1694202520279"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1069412252271"><a name="p1069412252271"></a><a name="p1069412252271"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1069462552710"></a><a name="ul1069462552710"></a><ul id="ul1069462552710"><li>目标库若已存在数据，DRS在增量迁移过程中源库相同主键的数据将覆盖目标库已存在的数据，因此在迁移前需要用户自行判断数据是否需要清除，建议用户在迁移前自行清空目标库。</li><li>目标实例及关联RDS实例的运行状态必须正常，若关联RDS实例是主备实例，复制状态也必须正常。</li><li>目标库关联RDS实例必须有足够的磁盘空间。</li><li>目标库关联RDS数据库的字符集必须与源数据库一致。</li><li>目标库实例若选择将时间戳类型（TIMESTAMP，DATETIME）的列作为分片键，则源库数据在迁移到目标库之后，作为分片键的该时间戳类型列的秒精度将被丢弃。</li><li>目标数据库存在表的AUTO_INCREMENT值至少不能小于源库表的AUTO_INCREMENT值。</li></ul>
</td>
</tr>
</tbody>
</table>


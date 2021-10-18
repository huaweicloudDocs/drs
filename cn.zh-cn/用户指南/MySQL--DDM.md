# MySQL-\>DDM<a name="drs_04_0089"></a>

## 使用技巧（需要人为配合）<a name="section182303625619"></a>

-   如果您使用的是全量迁移模式（离线迁移），确保源和目标数据库无业务写入，保证迁移前后数据一致。

-   如果您使用的是全量+增量迁移模式（在线迁移），支持在源数据库有业务数据写入的情况下进行迁移，推荐**提前2-3天**启动任务，并配合如下使用技巧和对应场景的[操作要求](#section15921124810611)，以确保顺利迁移。
    -   全量迁移

        基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行迁移任务，相对静态的数据，迁移时复杂度将会降低。

        -   全量迁移会对源数据库有一定的访问压力。
        -   迁移无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
        -   正在迁移的数据被其他事务长时间锁死，可能导致读数据超时。
        -   由于MySQL固有特点限制，CPU资源紧张时，存储引擎为Tokudb的表，读取速度可能下降至10%。

    -   数据对比

        建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。



## 操作要求<a name="section15921124810611"></a>

针对一些无法预知或人为因素及环境突变导致迁移失败的情况，数据复制服务提供以下常见的操作限制，供您在迁移过程中参考。

**表 1**  操作要求

<a name="table18634822714"></a>
<table><thead align="left"><tr id="row116341129716"><th class="cellrowborder" valign="top" width="18.39%" id="mcps1.2.3.1.1"><p id="p16341421770"><a name="p16341421770"></a><a name="p16341421770"></a><strong id="b1863482374"><a name="b1863482374"></a><a name="b1863482374"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.61%" id="mcps1.2.3.1.2"><p id="p166359218710"><a name="p166359218710"></a><a name="p166359218710"></a><strong id="b13635421878"><a name="b13635421878"></a><a name="b13635421878"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row76351821877"><td class="cellrowborder" valign="top" width="18.39%" headers="mcps1.2.3.1.1 "><p id="p146351024713"><a name="p146351024713"></a><a name="p146351024713"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.61%" headers="mcps1.2.3.1.2 "><a name="ul66353220710"></a><a name="ul66353220710"></a><ul id="ul66353220710"><li><a href="#table37175131683">表2</a>中的环境要求均不允许在迁移过程中修改，直至迁移结束。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建迁移任务。</li><li>数据类型不兼容时，可能引起迁移失败。</li><li>不支持外键级联操作。</li><li>源库为RDS for MySQL实例时，不支持带有TDE特性并建立具有加密功能表。</li></ul>
</td>
</tr>
<tr id="row2635821779"><td class="cellrowborder" valign="top" width="18.39%" headers="mcps1.2.3.1.1 "><p id="p10635021670"><a name="p10635021670"></a><a name="p10635021670"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.61%" headers="mcps1.2.3.1.2 "><a name="ul13635152772"></a><a name="ul13635152772"></a><ul id="ul13635152772"><li>迁移过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>迁移过程中，不允许对源库需要迁移的表结构进行修改。</li><li>增量迁移场景下，不支持源数据库进行恢复操作。</li><li>选择表级对象迁移时，增量迁移过程中不建议对表进行重命名操作。</li><li>迁移过程中不支持DDL操作，这样可能会引起任务迁移失败。</li><li>建议将expire_log_day参数设置在合理的范围，确保恢复时断点处的binlog尚未过期，以保证服务中断后的顺利恢复。</li><li>如果源数据库为自建库，并且安装了Percona Server for MySQL 5.6.x或Percona Server for MySQL 5.7.x时，内存管理器必须使用Jemalloc库，以避免因系统表频繁查询带来的内存回收不及时，并最终导致数据库Out of Memory问题。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section1378915481671"></a>

实时迁移对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table37175131683"></a>
<table><thead align="left"><tr id="row14718121315818"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p17181013388"><a name="p17181013388"></a><a name="p17181013388"></a><strong id="b107183131687"><a name="b107183131687"></a><a name="b107183131687"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p167181813589"><a name="p167181813589"></a><a name="p167181813589"></a><strong id="b11718151319819"><a name="b11718151319819"></a><a name="b11718151319819"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row147181713289"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p167181135810"><a name="p167181135810"></a><a name="p167181135810"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul771810131686"></a><a name="ul771810131686"></a><ul id="ul771810131686"><li><strong id="b2718813684"><a name="b2718813684"></a><a name="b2718813684"></a>全量迁移最小权限要求：</strong><a name="ul19719513282"></a><a name="ul19719513282"></a><ul id="ul19719513282"><li>源数据库帐户需要具备如下权限：SELECT、SHOW VIEW、EVENT。</li><li>目标中间件帐户需要具备以下基本权限：CREATE、DROP、ALTER、 INDEX、 INSERT、DELETE、 UPDATE、 SELECT， 同时必须具备扩展权限：全表SELECT权限。</li><li>目标中间件帐户必须具备对所迁移数据库的权限。</li></ul>
</li><li><strong id="b11562172819596"><a name="b11562172819596"></a><a name="b11562172819596"></a>全量+增量迁移最小权限要求：</strong><a name="ul57197139810"></a><a name="ul57197139810"></a><ul id="ul57197139810"><li>源数据库帐户需要具备如下权限：SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</li><li>目标中间件帐户需要具备以下基本权限：CREATE、DROP、ALTER、 INDEX、 INSERT、DELETE、 UPDATE、 SELECT， 同时必须具备扩展权限：全表SELECT权限。</li><li>目标中间件帐户必须具备对所迁移数据库的权限。</li></ul>
</li></ul>
</td>
</tr>
<tr id="row6719313383"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p371911131886"><a name="p371911131886"></a><a name="p371911131886"></a>迁移对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul14719013889"></a><a name="ul14719013889"></a><ul id="ul14719013889"><li>目前只支持迁移源库的数据，不支持迁移源库表结构及其他数据库对象。</li><li>用户需要在目标库根据源端逻辑库的表结构，自行在目标库创建对应的表结构及索引。未在目标库创建的对象，视为用户不选择这个对象进行迁移。</li><li>源库在目标库创建的表结构， 必须与源库的表结构完全一致。</li></ul>
<a name="ul2071920131283"></a><a name="ul2071920131283"></a><ul id="ul2071920131283"><li>不支持非MyISAM和非InnoDB表的迁移。</li></ul>
</td>
</tr>
<tr id="row2720101319815"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p10720913884"><a name="p10720913884"></a><a name="p10720913884"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul67206134820"></a><a name="ul67206134820"></a><ul id="ul67206134820"><li>增量迁移时，MySQL源数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>增量迁移时，在磁盘空间允许的情况下，建议源数据库binlog保存时间越长越好，建议为3天。</li><li>源数据库expire_logs_days参数值为0，可能会导致迁移失败。</li><li>增量迁移时，必须设置MySQL源数据库的server－id。如果源数据库版本小于或等于MySQL5.6，server－id的取值范围在2－4294967296之间；如果源数据库版本大于或等于MySQL5.7，server－id的取值范围在1－4294967296之间。</li><li>源库中的库名、表名不能包含：'&lt;&gt;/\以及非ASCII字符。</li><li>MySQL源数据库建议开启skip-name-resolve，减少连接超时的可能性。</li><li>源数据库GTID状态建议为开启状态。</li></ul>
</td>
</tr>
<tr id="row147209131782"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1272017131387"><a name="p1272017131387"></a><a name="p1272017131387"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul4720513989"></a><a name="ul4720513989"></a><ul id="ul4720513989"><li>目标库若已存在数据，DRS在增量迁移过程中源库相同主键的数据将覆盖目标库已存在的数据，因此在迁移前需要用户自行判断数据是否需要清除，建议用户在迁移前自行清空目标库。</li><li>目标实例及关联RDS实例的运行状态必须正常，若关联RDS实例是主备实例，复制状态也必须正常。</li><li>目标库关联RDS实例必须有足够的磁盘空间。</li><li>目标库关联RDS数据库的字符集必须与源数据库一致。</li><li>目标库实例若选择将时间戳类型（TIMESTAMP，DATETIME）的列作为分片键，则源库数据在迁移到目标库之后，作为分片键的该时间戳类型列的秒精度将被丢弃。</li><li>目标数据库存在表的AUTO_INCREMENT值至少不能小于源库表的AUTO_INCREMENT值。</li></ul>
</td>
</tr>
</tbody>
</table>


# Oracle-\>Kafka<a name="drs_04_0109"></a>

## 使用技巧（需要人为配合）<a name="section98341051155812"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1691943218231)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section1691943218231"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table66383571197"></a>
<table><thead align="left"><tr id="row1639185711919"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p19639105721917"><a name="p19639105721917"></a><a name="p19639105721917"></a><strong id="b9639195791919"><a name="b9639195791919"></a><a name="b9639195791919"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p14639135712192"><a name="p14639135712192"></a><a name="p14639135712192"></a><strong id="b563995701913"><a name="b563995701913"></a><a name="b563995701913"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row6639145731911"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p166391357141914"><a name="p166391357141914"></a><a name="p166391357141914"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul06391157111911"></a><a name="ul06391157111911"></a><ul id="ul06391157111911"><li><a href="#table172037616201">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>如有中文、日文等特殊字符，业务连接Oracle数据库使用的编码需和Oracle数据库服务端编码一致，否则目标库会出现乱码。</li><li>Oracle中<span id="text3639195711916"><a name="text3639195711916"></a><a name="text3639195711916"></a>实时同步</span>到kafka后的字符集为UTF8。</li><li>对于Oracle RAC集群，建议使用scanip+ servicename方式创建任务，scanip具有更强的容错性，更好的负载能力，更快的同步体验。</li><li>增量同步不支持12c及以上版本的PDB数据库。</li><li>附加日志级别为all或者pk+ui。</li><li>日志中未出现的列在传递的消息中不会出现，表示该列未更新。</li></ul>
</td>
</tr>
<tr id="row5640155718195"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p2640175716196"><a name="p2640175716196"></a><a name="p2640175716196"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul11640157121916"></a><a name="ul11640157121916"></a><ul id="ul11640157121916"><li>同步过程中，不允许删除连接源和目标数据库的用户的用户名、密码、权限，或修改目标数据库的端口号。</li><li>选择表级对象同步时，增量同步过程中不建议对表进行重命名操作。</li><li>支持表级DDL操作。</li><li>任务再编辑增加新表时，请确保新增的表的事务都已提交，否则未提交的事务可能无法同步到目标库。建议在业务低峰期做增加表的操作。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section86695405239"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table172037616201"></a>
<table><thead align="left"><tr id="row1203196172011"><th class="cellrowborder" valign="top" width="18.3%" id="mcps1.2.3.1.1"><p id="p52035682014"><a name="p52035682014"></a><a name="p52035682014"></a><strong id="b1203136152012"><a name="b1203136152012"></a><a name="b1203136152012"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.69999999999999%" id="mcps1.2.3.1.2"><p id="p1620311612010"><a name="p1620311612010"></a><a name="p1620311612010"></a><strong id="b1020313682015"><a name="b1020313682015"></a><a name="b1020313682015"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row1203126192019"><td class="cellrowborder" valign="top" width="18.3%" headers="mcps1.2.3.1.1 "><p id="p22031632015"><a name="p22031632015"></a><a name="p22031632015"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.69999999999999%" headers="mcps1.2.3.1.2 "><a name="ul6203136192011"></a><a name="ul6203136192011"></a><ul id="ul6203136192011"><li>源数据库端：需要具有CREATE SESSION、SELECT ANY TRANSACTION、SELECT_CATALOG_ROLE、SELECT ANY DICTIONARY权限和EXECUTE_CATALOG_ROLE角色，若Oracle为12C及以上版本还需要LOGMINING权限。</li></ul>
</td>
</tr>
<tr id="row020313611203"><td class="cellrowborder" valign="top" width="18.3%" headers="mcps1.2.3.1.1 "><p id="p102038642013"><a name="p102038642013"></a><a name="p102038642013"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.69999999999999%" headers="mcps1.2.3.1.2 "><a name="ul920315662014"></a><a name="ul920315662014"></a><ul id="ul920315662014"><li>支持表<span id="text162038632012"><a name="text162038632012"></a><a name="text162038632012"></a>实时同步</span>，其他数据库对象暂不支持。</li><li>支持VARCHAR、VARCHAR2、NVARCHAR2、NUMBER、FLOAT、LONG、DATE、BINARY_FLOAT、BINARY_DOUBLE、CHAR、NCHAR、ROWID、TIMESTAMP、TIMESTAMP WITH TIME ZONE、TIMESTAMP WITH LOCAL TIME ZONE类型。</li><li>不支持接入的列类型：GEOMETRY以及自定义类型。</li><li>不支持同步但以过滤方式接入的列类型：BLOB、 CLOB、NCLOB、INTERVAL_YEAR_TO_MONTH、INTERVAL_DAY_TO_SECOND、UROWID、BFILE、XML、LONG、long raw。</li><li>支持同步但默认过滤的列类型：raw（同步数据为原始二进制数据）。</li><li>不支持默认值含有表达式的函数的表的同步。</li></ul>
</td>
</tr>
<tr id="row22049692013"><td class="cellrowborder" valign="top" width="18.3%" headers="mcps1.2.3.1.1 "><p id="p152048610205"><a name="p152048610205"></a><a name="p152048610205"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.69999999999999%" headers="mcps1.2.3.1.2 "><a name="ul42041363208"></a><a name="ul42041363208"></a><ul id="ul42041363208"><li>库名、表名不支持的字符有：非ASCII字符、“. ”、 “&gt;”、 “&lt;”、 “\”、 “`”、 “|”、 “,”、 “? ”、 “! ”、 “"”和 “'”。</li><li>同步过程中，要求源数据库打开归档日志。</li><li>源数据库不允许含有空库。</li><li>目前仅支持如下字符集：ZHS16GBK、AL32UTF8、UTF8、US7ASCII、WE8MSWIN1252。</li><li>源库为rac时，不支持增加、减少节点数量。</li><li>源库为rac时，如果需要使用scanip，需要drs node能够连接全部节点的vip，否则无法通过连接检查。</li><li>DRS仅要求源数据库Oracle的补全日志级别为pk + ui。<p id="p920410642013"><a name="p920410642013"></a><a name="p920410642013"></a>但由于大数据的增量数据入库时，会存在不支持的update语句，导致需要使用Delete+Insert的方式刷新增量数据，比如Hive。那么，会存在要求Oracle的补全日志级别为ALL的情况。</p>
<p id="p1920415619201"><a name="p1920415619201"></a><a name="p1920415619201"></a>所以，只有特殊数据库要求Oracle开启全列补齐日志，这个要求是由最终入库的目标数据库引擎特点决定的，通常来说是跑批类数据库（<span id="text3774120151417"><a name="text3774120151417"></a><a name="text3774120151417"></a>GaussDB(DWS)</span>）和大数据类数据库（Hive）。</p>
</li></ul>
</td>
</tr>
<tr id="row1420456172012"><td class="cellrowborder" valign="top" width="18.3%" headers="mcps1.2.3.1.1 "><p id="p32042061204"><a name="p32042061204"></a><a name="p32042061204"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.69999999999999%" headers="mcps1.2.3.1.2 "><a name="ul02047619207"></a><a name="ul02047619207"></a><ul id="ul02047619207"><li>目标库为普通Kafka。</li></ul>
</td>
</tr>
</tbody>
</table>


# Oracle-\>GaussDB\(for openGauss\)主备版<a name="drs_04_0111"></a>

## 操作要求<a name="zh-cn_topic_0000001121238797_section1610153915412"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="zh-cn_topic_0000001121238797_table16590152102819"></a>
<table><thead align="left"><tr id="zh-cn_topic_0000001121238797_row115684518285"><th class="cellrowborder" valign="top" width="18.18%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0000001121238797_p65689515282"><a name="zh-cn_topic_0000001121238797_p65689515282"></a><a name="zh-cn_topic_0000001121238797_p65689515282"></a><strong id="zh-cn_topic_0000001121238797_b756820520280"><a name="zh-cn_topic_0000001121238797_b756820520280"></a><a name="zh-cn_topic_0000001121238797_b756820520280"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.82000000000001%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0000001121238797_p125681522813"><a name="zh-cn_topic_0000001121238797_p125681522813"></a><a name="zh-cn_topic_0000001121238797_p125681522813"></a><strong id="zh-cn_topic_0000001121238797_b65698522811"><a name="zh-cn_topic_0000001121238797_b65698522811"></a><a name="zh-cn_topic_0000001121238797_b65698522811"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="zh-cn_topic_0000001121238797_row20569759283"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0000001121238797_p19569259286"><a name="zh-cn_topic_0000001121238797_p19569259286"></a><a name="zh-cn_topic_0000001121238797_p19569259286"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="zh-cn_topic_0000001121238797_ul1456918582810"></a><a name="zh-cn_topic_0000001121238797_ul1456918582810"></a><ul id="zh-cn_topic_0000001121238797_ul1456918582810"><li><a href="#zh-cn_topic_0000001121238797_table164271936282">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>不建议在数据库中使用非精确数值类型做主键，该特性影响 DRS 增量场景下对 UPDATE、DELETE语句的同步，同时也会导致内容比对不可用。主键支持的类型可参考<a href="https://support.huaweicloud.com/productdesc-drs/drs_08_0002.html#section6" target="_blank" rel="noopener noreferrer">Oracle数据库-&gt;GaussDB(for openGauss)数据库映射关系</a>。</li><li>增量同步时，BLOB末尾的0x00、CLOB末尾的空格会被截断。</li><li>当Oracle字符集是WE8MSWIN1252时，CLOB列同步到目标库可能出现乱码，建议先修改源库字符集为AL32UTF8再同步数据。</li></ul>
</td>
</tr>
<tr id="zh-cn_topic_0000001121238797_row1656918519281"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0000001121238797_p75695514283"><a name="zh-cn_topic_0000001121238797_p75695514283"></a><a name="zh-cn_topic_0000001121238797_p75695514283"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="zh-cn_topic_0000001121238797_ul205691350288"></a><a name="zh-cn_topic_0000001121238797_ul205691350288"></a><ul id="zh-cn_topic_0000001121238797_ul205691350288"><li>由于无主键表缺乏行的唯一性标志，网络不稳定时涉及少量重试，表数据存在少量不一致的可能性。</li><li>如果源库和目标库字符集不一致，如源库是ZHS16GBK，目标库是UTF8，由于ZHS16GBK字符集单个中文字符占用2个字节，而UTF8字符集单个中文字符占用3个字节，可能会导致CHAR或VARCHAR类型数据同步到目标库后超出字段定义长度，所以客户需要根据实际情况对目标库CHAR和VARCHAR类型字段长度进行扩充（如扩大为源库的1.5倍）。</li><li>对于全量同步中的目标数据库表对象，不能进行写入操作，否则会导致数据不一致。</li><li>同步过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>增量同步过程中，支持部分DDL操作。<a name="ul182043364312"></a><a name="ul182043364312"></a><ul id="ul182043364312"><li>表级同步支持alter&nbsp;table&nbsp;add&nbsp;column、alter&nbsp;table&nbsp;drop&nbsp;column、alter&nbsp;table&nbsp;rename&nbsp;column、alter&nbsp;table&nbsp;modify&nbsp;column以及truncate&nbsp;table的基本DDL，不支持默认值等的修改。</li><li>库级同步支持alter table add column、alter table drop column、alter table rename column、alter table modify column以及truncate table</li></ul>
</li><li>全量同步分为表结构同步（含索引）、数据同步两个阶段，任务中只要有一个表的结构在目标库中创建成功即进入数据同步阶段。若同步完成产生失败表，再启动时将只同步数据，不同步表结构信息，用户必须手动在目标库中建表。</li><li>全量同步分区表的结构时会将该对象转为非分区的普通表。</li><li>全量同步表结构时只支持字符串或数字类型的普通默认值约束，不支持函数、序列等类型的默认值约束。</li><li>增量同步阶段，修改抓取任务的启动位点主要用于重新同步数据。<a name="zh-cn_topic_0000001121238797_ul1817102943318"></a><a name="zh-cn_topic_0000001121238797_ul1817102943318"></a><ul id="zh-cn_topic_0000001121238797_ul1817102943318"><li>修改抓取位点之后，上一次对象级对比结果不会展示出来。</li><li>单独修改抓取任务的启动位点，会把该位点同步到回放任务的启动位点上，即回放任务的启动位点和抓取任务的启动位点一致，不影响用户单独修改回放任务的启动位点。</li></ul>
</li><li>当Oracle数据库为19c 版本，增量同步时必须打开全部PDB。</li><li>全量和增量同步不支持 Oracle 12c以上版本的STRING扩展数据类型(EXTENDED DATA TYPE)。</li><li>全量和增量同步不支持隐藏列（UNUSED, INVISIBLE）。</li><li>增量同步可选XStream、LogMiner增量日志读取模式，XStream所支持的数据类型更广。开启Xstream接口要求Oracle用户拥有Oracle GoldenGate的license许可，相关要求可参考<a href="https://docs.oracle.com/cd/E11882_01/server.112/e16545/xstrm_intro.htm#XSTRM72545" target="_blank" rel="noopener noreferrer">《Oracle数据库介绍》</a>。</li><li>任务再编辑增加新表时，请确保新增的表的事务都已提交，否则未提交的事务可能无法同步到目标库。建议在业务低峰期做增加表的操作。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="zh-cn_topic_0000001121238797_section165311339195419"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="zh-cn_topic_0000001121238797_table164271936282"></a>
<table><thead align="left"><tr id="zh-cn_topic_0000001121238797_row7570175192811"><th class="cellrowborder" valign="top" width="18.18%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0000001121238797_p1157095122810"><a name="zh-cn_topic_0000001121238797_p1157095122810"></a><a name="zh-cn_topic_0000001121238797_p1157095122810"></a><strong id="zh-cn_topic_0000001121238797_b115708522811"><a name="zh-cn_topic_0000001121238797_b115708522811"></a><a name="zh-cn_topic_0000001121238797_b115708522811"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.82000000000001%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0000001121238797_p165701053285"><a name="zh-cn_topic_0000001121238797_p165701053285"></a><a name="zh-cn_topic_0000001121238797_p165701053285"></a><strong id="zh-cn_topic_0000001121238797_b15570954289"><a name="zh-cn_topic_0000001121238797_b15570954289"></a><a name="zh-cn_topic_0000001121238797_b15570954289"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="zh-cn_topic_0000001121238797_row357018512289"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0000001121238797_p55705502818"><a name="zh-cn_topic_0000001121238797_p55705502818"></a><a name="zh-cn_topic_0000001121238797_p55705502818"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="zh-cn_topic_0000001121238797_ul14570653282"></a><a name="zh-cn_topic_0000001121238797_ul14570653282"></a><ul id="zh-cn_topic_0000001121238797_ul14570653282"><li>源数据库端：<a name="ul10114111002010"></a><a name="ul10114111002010"></a><ul id="ul10114111002010"><li>全量+增量和增量同步时需要具有CREATE SESSION、SELECT ANY DICTIONARY、EXECUTE_CATALOG_ROLE、SELECT ANY TRANSACTION权限和SELECT ANY TABLE权限，若Oracle为12c及以上版本还需要LOGMINING权限。全量同步时需要具有CREATE SESSION、SELECT ANY DICTIONARY、SELECT ANY TABLE和FLASHBACK ANY TABLE权限。</li><li>12c 以上版本 PDB 数据库同步时，需要为用户赋予如下权限：<p id="p1967452219333"><a name="p1967452219333"></a><a name="p1967452219333"></a>在CDB下创建C##前缀的容器数据库用户赋予CREATE SESSION、SELECT ANY DICTIONARY、SELECT ANY TABLE、LOGMINING、EXECUTE_CATALOG_ROLE权限和SET CONTAINER权限（GRANT&nbsp;SET&nbsp;CONTAINER&nbsp;TO&nbsp;C##USERNAME&nbsp;CONTAINER=&nbsp;ALL;）。</p>
<p id="p721274311526"><a name="p721274311526"></a><a name="p721274311526"></a>在PDB下为C##前缀用户赋予以下权限（其中RESTRICTED SESSION、SELECT ON SYS.COL$、 SELECT ON SYS.OBJ$权限需要单独赋予）：</p>
<p id="p11808629123117"><a name="p11808629123117"></a><a name="p11808629123117"></a>全量+增量和增量同步时需要具有RESTRICTED SESSION、CREATE SESSION、SELECT ANY DICTIONARY、EXECUTE_CATALOG_ROLE、SELECT ANY TRANSACTION、SELECT ANY TABLE、LOGMINING、SELECT ON SYS.COL$、SELECT ON SYS.OBJ$。全量同步时需要具有RESTRICTED SESSION、CREATE SESSION、SELECT ANY DICTIONARY、SELECT ANY TABLE、FLASHBACK ANY TABLE、SELECT ON SYS.COL$、SELECT ON SYS.OBJ$。</p>
</li></ul>
</li><li>源数据库端：增量同步时，源库Oracle需要打开pk/uk级别或all级别的SUPPLEMENTAL LOG，且日志模式需要设置为归档模式。</li><li>目标数据库端必须同时拥有以下权限：<a name="ul141507123018"></a><a name="ul141507123018"></a><ul id="ul141507123018"><li>库级权限：需要使用root或其他有Sysadmin角色的DATABASE用户登录postgres基库，赋予用户DATABASE的CREATE、CONNECT权限。</li><li>SCHEMA级权限：需要使用 root、或其他有Sysadmin角色的DATABASE用户、或目标数据库的OWNER用户登入目标数据库，赋予用户SCHEMA的CREATE、USAGE权限。</li><li>表级权限：需要使用 root、或其他有Sysadmin角色的DATABASE用户、或目标数据库的OWNER用户登入目标数据库 ，赋予用户SCHEMA下所有表的SELECT，UPDATE，INSERT和DELETE权限。</li></ul>
</li></ul>
</td>
</tr>
<tr id="zh-cn_topic_0000001121238797_row457010532816"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0000001121238797_p19570556281"><a name="zh-cn_topic_0000001121238797_p19570556281"></a><a name="zh-cn_topic_0000001121238797_p19570556281"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="zh-cn_topic_0000001121238797_ul157019517282"></a><a name="zh-cn_topic_0000001121238797_ul157019517282"></a><ul id="zh-cn_topic_0000001121238797_ul157019517282"><li>全量同步时支持表、普通索引、主键与唯一约束、数据的同步。增量同步时支持表的实时同步。</li><li>全量阶段不支持bfile、xml、sdo_geometry、urowid和自定义类型。增量阶段不支持bfile、xml、sdo_geometry、urowid、INTERVAL和自定义类型。</li><li>timestamp和interval day to second类型支持的最大精度是6。</li><li>全量同步结构迁移不支持位图索引、倒排索引、函数索引。</li><li>增量同步时，源端或者目标端数据库异常会触发任务失败，数据库恢复后重试启动任务时触发全局启动，此时会忽略原有抓取或回放组件的状态，同时回放也会按照抓取的中断点位再启动。</li><li>增量同步LOB类型仅支持BasicFiles属性，不支持SecureFiles属性，支持的LOB类型大小限10M以内。</li><li>对于TIMESTAMP WITH TIME ZONE类型，根据目标库时区做转换后不得大于“9999-12-31 23:59:59.999999”。</li><li>源库支持to_date和sys_guid函数做默认值。将函数作为default值时，需要目标库也有相同功能的函数。对于目标库不存在对应函数的情况，默认值函数可能会被置空。</li><li>不支持默认值含有表达式的函数的表的同步。</li><li>不支持同步源库中的临时表。</li></ul>
</td>
</tr>
<tr id="zh-cn_topic_0000001121238797_row2570955289"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0000001121238797_p1857016517286"><a name="zh-cn_topic_0000001121238797_p1857016517286"></a><a name="zh-cn_topic_0000001121238797_p1857016517286"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="zh-cn_topic_0000001121238797_ul1457065112819"></a><a name="zh-cn_topic_0000001121238797_ul1457065112819"></a><ul id="zh-cn_topic_0000001121238797_ul1457065112819"><li>库名、表名等数据库对象名称支持英文字符、“#”、“$”、“_”等符号， DRS 不支持非ASCII字符、“. ”、 “&gt;”、 “&lt;”、 “\”、 “`”、 “|”、 “,”、 “? ”、 “! ”、 “"”和 “'”等字符。对象名同步到目标库后会转换成小写，未避免同步失败，选择的源库表中不能存在表名称字母相同但大小写不同的表。</li><li>增量同步如果选择XStream读取方式，源库XStream的开关ENABLE_GOLDENGATE_REPLICATION在同步过程中需保持打开。</li><li>目前仅支持如下字符集：ZHS16GBK、AL32UTF8、UTF8、US7ASCII、WE8MSWIN1252。</li></ul>
</td>
</tr>
<tr id="zh-cn_topic_0000001121238797_row357117510283"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0000001121238797_p6571205122814"><a name="zh-cn_topic_0000001121238797_p6571205122814"></a><a name="zh-cn_topic_0000001121238797_p6571205122814"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="zh-cn_topic_0000001121238797_ul1857165182815"></a><a name="zh-cn_topic_0000001121238797_ul1857165182815"></a><ul id="zh-cn_topic_0000001121238797_ul1857165182815"><li>目标库必须是本云<span id="zh-cn_topic_0000001121238797_text14871193214126"><a name="zh-cn_topic_0000001121238797_text14871193214126"></a><a name="zh-cn_topic_0000001121238797_text14871193214126"></a>GaussDB(for openGauss)</span>主备版实例。</li><li>同步时，需要手动在目标数据库端创建与源数据库对应的全部以小写字母命名的数据库。</li><li>增量同步的表要禁用外键，因为DRS并行回放会使得不同表之间的写入顺序和源库不一致，可能会触发外键约束限制，造成同步失败。</li></ul>
</td>
</tr>
</tbody>
</table>


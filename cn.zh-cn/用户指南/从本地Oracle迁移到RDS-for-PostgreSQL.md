# 从本地Oracle迁移到RDS for PostgreSQL<a name="drs_07_0010"></a>

数据复制服务支持本地自建的Oracle数据库迁移至本云RDS for PostgreSQL实例。

数据复制服务目前可以实现Oracle数据库的全量迁移 ，可选择通过公网网络或VPN、专线网络实现。

本小节将介绍通过公网网络方式进行 Oracle-\>RDS for PostgreSQL数据迁移的任务配置流程。

## 迁移限制<a name="section136232036173620"></a>

数据复制服务在使用上有一些固定的限制，用来提高数据迁移的稳定性和安全性。在进行正式的数据迁移之前，请先阅读以确保各存储引擎已满足使用限制条件。

对于Oracle-\>RDS for PostgreSQL的迁移，使用限制请参见[表1](#table20677749204218)。

**表 1**  迁移限制

<a name="table20677749204218"></a>
<table><thead align="left"><tr id="row13678749194218"><th class="cellrowborder" valign="top" width="23.05%" id="mcps1.2.3.1.1"><p id="p1167811496428"><a name="p1167811496428"></a><a name="p1167811496428"></a><strong id="b191071715448"><a name="b191071715448"></a><a name="b191071715448"></a>功能</strong></p>
</th>
<th class="cellrowborder" valign="top" width="76.95%" id="mcps1.2.3.1.2"><p id="p19678749114218"><a name="p19678749114218"></a><a name="p19678749114218"></a><strong id="b12108197144412"><a name="b12108197144412"></a><a name="b12108197144412"></a>限制条件</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row186781495427"><td class="cellrowborder" valign="top" width="23.05%" headers="mcps1.2.3.1.1 "><p id="p14678114914420"><a name="p14678114914420"></a><a name="p14678114914420"></a>权限限制</p>
</td>
<td class="cellrowborder" valign="top" width="76.95%" headers="mcps1.2.3.1.2 "><a name="ul176811528154415"></a><a name="ul176811528154415"></a><ul id="ul176811528154415"><li>源数据库端：需要具有DBA权限。</li><li>目标数据库端：待迁移db的读写权限。</li></ul>
</td>
</tr>
<tr id="row267834914212"><td class="cellrowborder" valign="top" width="23.05%" headers="mcps1.2.3.1.1 "><p id="p1267864914217"><a name="p1267864914217"></a><a name="p1267864914217"></a>源数据库配置</p>
</td>
<td class="cellrowborder" valign="top" width="76.95%" headers="mcps1.2.3.1.2 "><a name="ul2222240132515"></a><a name="ul2222240132515"></a><ul id="ul2222240132515"><li>由于PostgreSQL数据库比Oralce数据库多了一层schema结构，在视图创建语句中as子句中不能包含db.table的形式，否则视图迁移会失败。<p id="p388952512110"><a name="p388952512110"></a><a name="p388952512110"></a>示例：将以下的语句一需要改写成语句二。</p>
<p id="p11418749105817"><a name="p11418749105817"></a><a name="p11418749105817"></a>语句一：</p>
<pre class="codeblock" id="codeblock19809121835918"><a name="codeblock19809121835918"></a><a name="codeblock19809121835918"></a>create view v1 as select id from db1.t1;</pre>
<p id="p2105174525915"><a name="p2105174525915"></a><a name="p2105174525915"></a>语句二：</p>
<pre class="codeblock" id="codeblock39361626135914"><a name="codeblock39361626135914"></a><a name="codeblock39361626135914"></a>create view v1 as select id from t1;</pre>
</li><li>不支持函数索引迁移。<p id="p4915102616212"><a name="p4915102616212"></a><a name="p4915102616212"></a>示例：</p>
<pre class="codeblock" id="codeblock20193617210"><a name="codeblock20193617210"></a><a name="codeblock20193617210"></a>create index idx_t on t(substr(dt, 1, 8));</pre>
</li><li>timestamp和interval day to second类型支持的最大精度是6。</li><li>数据类型不支持bfile、xmltype、sdo_geometry和自定义类型。</li><li>源库不能存在只是大小写不同的表。</li><li>库名不支持的字符有：&lt;.&gt;\。</li><li>表名不支持的字符有：&lt;."&gt;\。</li></ul>
</td>
</tr>
<tr id="row9678134914217"><td class="cellrowborder" valign="top" width="23.05%" headers="mcps1.2.3.1.1 "><p id="p26781849144214"><a name="p26781849144214"></a><a name="p26781849144214"></a>目标数据库配置</p>
</td>
<td class="cellrowborder" valign="top" width="76.95%" headers="mcps1.2.3.1.2 "><a name="ul16279174412364"></a><a name="ul16279174412364"></a><ul id="ul16279174412364"><li>目标库必须是本云RDS for PostgreSQL增强版实例。</li><li>迁移前，需要手动在目标数据库端创建一个与源数据库名对应的全部以小写字母命名的数据库，且待迁移的对象不存在于该创建的数据库中。</li><li>目标数据库中不能存在与源数据库转换成小写后相同的对象名。</li></ul>
</td>
</tr>
<tr id="row16678349184211"><td class="cellrowborder" valign="top" width="23.05%" headers="mcps1.2.3.1.1 "><p id="p2678114984210"><a name="p2678114984210"></a><a name="p2678114984210"></a>迁移操作</p>
</td>
<td class="cellrowborder" valign="top" width="76.95%" headers="mcps1.2.3.1.2 "><a name="ul5950142213318"></a><a name="ul5950142213318"></a><ul id="ul5950142213318"><li>目前仅支持全量迁移。</li><li>单个迁移任务每次只能迁移一个库（owner）的数据，多个数据库的迁移需要创建多个任务。</li><li>支持表、视图、索引、约束、数据的迁移，其他数据库对象暂不支持，如存储过程等。</li><li>不支持分区表的迁移。</li><li>表、视图等对象名迁移到目标库后会转换成小写，如ABC和abc。</li><li>对于迁移中的数据库对象，在迁移期间，源库和目标库都不能进行写入操作，否则会导致数据不一致。</li><li>源库和目标库时区设置必须一致。</li><li>如有中文、日文等特殊字符，业务连接Oracle使用的编码需和Oracle服务端编码一致，否则目标库会出现乱码。</li><li>在迁移任务未结束前，不能修改源库所有用户、密码和用户权限等信息。</li></ul>
</td>
</tr>
</tbody>
</table>

## 数据类型映射关系<a name="section157291712135812"></a>

由于Oracle数据库和PostgreSQL数据库的数据类型不是一一对应的，所以数据复制服务在进行迁移时，会根据两种数据库类型进行对应的数据类型映射，具体的数据类型映射关系请参见[表2](#table165608589112)。

**表 2**  数据类型映射关系

<a name="table165608589112"></a>
<table><thead align="left"><tr id="row756111589112"><th class="cellrowborder" valign="top" width="33.373337333733375%" id="mcps1.2.4.1.1"><p id="p165611358111"><a name="p165611358111"></a><a name="p165611358111"></a><strong id="b1583916251735"><a name="b1583916251735"></a><a name="b1583916251735"></a>Oracle数据库</strong></p>
</th>
<th class="cellrowborder" valign="top" width="33.29332933293329%" id="mcps1.2.4.1.2"><p id="p35613581312"><a name="p35613581312"></a><a name="p35613581312"></a><strong id="b58748251736"><a name="b58748251736"></a><a name="b58748251736"></a>PostgreSQL数据库</strong></p>
</th>
<th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.3"><p id="p456119584110"><a name="p456119584110"></a><a name="p456119584110"></a><strong id="b1887611251632"><a name="b1887611251632"></a><a name="b1887611251632"></a>是否支持映射</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row135611358513"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p20703359132217"><a name="p20703359132217"></a><a name="p20703359132217"></a>CHAR</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p8703759162220"><a name="p8703759162220"></a><a name="p8703759162220"></a>CHAR</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p156119582118"><a name="p156119582118"></a><a name="p156119582118"></a>支持</p>
</td>
</tr>
<tr id="row156112581818"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p15703105982217"><a name="p15703105982217"></a><a name="p15703105982217"></a>VARCHAR</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p67031559122220"><a name="p67031559122220"></a><a name="p67031559122220"></a>VARCHAR</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p31499411279"><a name="p31499411279"></a><a name="p31499411279"></a>支持</p>
</td>
</tr>
<tr id="row2056110588111"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p197039597225"><a name="p197039597225"></a><a name="p197039597225"></a>VARCHAR2</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p87031959132216"><a name="p87031959132216"></a><a name="p87031959132216"></a>VARCHAR2</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p7401114213277"><a name="p7401114213277"></a><a name="p7401114213277"></a>支持</p>
</td>
</tr>
<tr id="row135619585117"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p17043591221"><a name="p17043591221"></a><a name="p17043591221"></a>NCHAR</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p6704559192216"><a name="p6704559192216"></a><a name="p6704559192216"></a>NCHAR</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p1691154319278"><a name="p1691154319278"></a><a name="p1691154319278"></a>支持</p>
</td>
</tr>
<tr id="row205616581316"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p1970475913229"><a name="p1970475913229"></a><a name="p1970475913229"></a>NVARCHAR2</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p4704359102219"><a name="p4704359102219"></a><a name="p4704359102219"></a>NVARCHAR2</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p18488154572716"><a name="p18488154572716"></a><a name="p18488154572716"></a>支持</p>
</td>
</tr>
<tr id="row456113582120"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p1170419596223"><a name="p1170419596223"></a><a name="p1170419596223"></a>NUMBER</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p770410593224"><a name="p770410593224"></a><a name="p770410593224"></a>NUMBER</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p186613461273"><a name="p186613461273"></a><a name="p186613461273"></a>支持</p>
</td>
</tr>
<tr id="row35612581317"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p147042593222"><a name="p147042593222"></a><a name="p147042593222"></a>BINARY_FLOAT</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p1170475916226"><a name="p1170475916226"></a><a name="p1170475916226"></a>BINARY_FLOAT</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p16876184713274"><a name="p16876184713274"></a><a name="p16876184713274"></a>支持</p>
</td>
</tr>
<tr id="row656110581916"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p11704859122210"><a name="p11704859122210"></a><a name="p11704859122210"></a>BINARY_DOUBLE</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p1705155992217"><a name="p1705155992217"></a><a name="p1705155992217"></a>BINARY_DOUBLE</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p1014174942715"><a name="p1014174942715"></a><a name="p1014174942715"></a>支持</p>
</td>
</tr>
<tr id="row14561458515"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p6705145902214"><a name="p6705145902214"></a><a name="p6705145902214"></a>FLOAT</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p14705175913228"><a name="p14705175913228"></a><a name="p14705175913228"></a>FLOAT</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p5123195092711"><a name="p5123195092711"></a><a name="p5123195092711"></a>支持</p>
</td>
</tr>
<tr id="row105611558714"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p470565911224"><a name="p470565911224"></a><a name="p470565911224"></a>DATE</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p137056594225"><a name="p137056594225"></a><a name="p137056594225"></a>DATE</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p022410516279"><a name="p022410516279"></a><a name="p022410516279"></a>支持</p>
</td>
</tr>
<tr id="row35624587120"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p20705205916223"><a name="p20705205916223"></a><a name="p20705205916223"></a>TIMESTAMP</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p1470535952217"><a name="p1470535952217"></a><a name="p1470535952217"></a>TIMESTAMP</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p1835513525277"><a name="p1835513525277"></a><a name="p1835513525277"></a>支持</p>
</td>
</tr>
<tr id="row456210584116"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p1070511599227"><a name="p1070511599227"></a><a name="p1070511599227"></a>INTERVAL</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p870520598223"><a name="p870520598223"></a><a name="p870520598223"></a>INTERVAL</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p1551175310272"><a name="p1551175310272"></a><a name="p1551175310272"></a>支持</p>
</td>
</tr>
<tr id="row55621758811"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p167068596222"><a name="p167068596222"></a><a name="p167068596222"></a>BLOB</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p16706459202218"><a name="p16706459202218"></a><a name="p16706459202218"></a>BYTEA</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p1626815551275"><a name="p1626815551275"></a><a name="p1626815551275"></a>支持</p>
</td>
</tr>
<tr id="row1562658117"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p1670620593227"><a name="p1670620593227"></a><a name="p1670620593227"></a>CLOB</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p570619597225"><a name="p570619597225"></a><a name="p570619597225"></a>CLOB</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p7501155722715"><a name="p7501155722715"></a><a name="p7501155722715"></a>支持</p>
</td>
</tr>
<tr id="row05621581118"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p20708115913226"><a name="p20708115913226"></a><a name="p20708115913226"></a>NCLOB</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p9708135910221"><a name="p9708135910221"></a><a name="p9708135910221"></a>TEXT</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p1655085872718"><a name="p1655085872718"></a><a name="p1655085872718"></a>支持</p>
</td>
</tr>
<tr id="row25625581115"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p970815593226"><a name="p970815593226"></a><a name="p970815593226"></a>LONG</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p37083593225"><a name="p37083593225"></a><a name="p37083593225"></a>TEXT</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p14760659192717"><a name="p14760659192717"></a><a name="p14760659192717"></a>支持</p>
</td>
</tr>
<tr id="row1056285811112"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p9574531122520"><a name="p9574531122520"></a><a name="p9574531122520"></a>LONG_RAW</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p826420313259"><a name="p826420313259"></a><a name="p826420313259"></a>BYTEA</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p189114010286"><a name="p189114010286"></a><a name="p189114010286"></a>支持</p>
</td>
</tr>
<tr id="row1856210581910"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p137791241152518"><a name="p137791241152518"></a><a name="p137791241152518"></a>RAW</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p32355322514"><a name="p32355322514"></a><a name="p32355322514"></a>BYTEA</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p209902102813"><a name="p209902102813"></a><a name="p209902102813"></a>支持</p>
</td>
</tr>
<tr id="row363712102614"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p883513992610"><a name="p883513992610"></a><a name="p883513992610"></a>ROWID</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p2063761172611"><a name="p2063761172611"></a><a name="p2063761172611"></a>CHAR</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p93181238289"><a name="p93181238289"></a><a name="p93181238289"></a>支持</p>
</td>
</tr>
<tr id="row43911518122615"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p14391101872610"><a name="p14391101872610"></a><a name="p14391101872610"></a>UROWID</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p10391171812616"><a name="p10391171812616"></a><a name="p10391171812616"></a>VARCHAR</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p1523114510281"><a name="p1523114510281"></a><a name="p1523114510281"></a>支持</p>
</td>
</tr>
<tr id="row8500194217266"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p170875982216"><a name="p170875982216"></a><a name="p170875982216"></a>XMLTYPE</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p1550010422261"><a name="p1550010422261"></a><a name="p1550010422261"></a>-</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p19501442102613"><a name="p19501442102613"></a><a name="p19501442102613"></a>不支持</p>
</td>
</tr>
<tr id="row19567345112610"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p145679455265"><a name="p145679455265"></a><a name="p145679455265"></a>BFILE</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p1556724522614"><a name="p1556724522614"></a><a name="p1556724522614"></a>-</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p18567114518267"><a name="p18567114518267"></a><a name="p18567114518267"></a>不支持</p>
</td>
</tr>
<tr id="row5244448132615"><td class="cellrowborder" valign="top" width="33.373337333733375%" headers="mcps1.2.4.1.1 "><p id="p17709185912222"><a name="p17709185912222"></a><a name="p17709185912222"></a>SDO_GEOMETRY</p>
</td>
<td class="cellrowborder" valign="top" width="33.29332933293329%" headers="mcps1.2.4.1.2 "><p id="p524524832616"><a name="p524524832616"></a><a name="p524524832616"></a>-</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p5245114862610"><a name="p5245114862610"></a><a name="p5245114862610"></a>不支持</p>
</td>
</tr>
</tbody>
</table>

## 前提条件<a name="section12806144412541"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   参见[申请须知](https://support.huaweicloud.com/qs-drs/drs_online_migration.html)。

## 迁移步骤<a name="section12716329897"></a>

1.  在“在线迁移管理“页面，单击“创建迁移任务“，进入创建迁移任务页面。
2.  在“迁移实例”页面，填选任务名称、通知收件人信息、描述、迁移实例信息，单击“下一步”。

    **图 1**  迁移任务信息<a name="fig1473012110109"></a>  
    ![](figures/迁移任务信息-2.png "迁移任务信息-2")

    **表 3**  任务和描述

    <a name="table8146244204420"></a>
    <table><thead align="left"><tr id="row55731924204420"><th class="cellrowborder" valign="top" width="18.42%" id="mcps1.2.3.1.1"><p id="p17991967204420"><a name="p17991967204420"></a><a name="p17991967204420"></a><strong id="b1611223511352"><a name="b1611223511352"></a><a name="b1611223511352"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="81.58%" id="mcps1.2.3.1.2"><p id="p48063227204420"><a name="p48063227204420"></a><a name="p48063227204420"></a><strong id="b3002268111352"><a name="b3002268111352"></a><a name="b3002268111352"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row807311204420"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p65392260204420"><a name="p65392260204420"></a><a name="p65392260204420"></a>任务名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p62281730204420"><a name="p62281730204420"></a><a name="p62281730204420"></a>任务名称在4位到64位之间，必须以字母开头，不区分大小写，可以包含字母、数字、中划线或下划线，不能包含其他的特殊字符。</p>
    </td>
    </tr>
    <tr id="row1080215433911"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p158027493912"><a name="p158027493912"></a><a name="p158027493912"></a>通知收件人</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p38891258184013"><a name="p38891258184013"></a><a name="p38891258184013"></a>该项为可选参数，开启之后，需要填写手机号码或者邮箱作为指定收件人。当迁移任务状态异常时，系统将发送通知给指定收件人。</p>
    <div class="note" id="note158461433104913"><a name="note158461433104913"></a><a name="note158461433104913"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p138461333114917"><a name="p138461333114917"></a><a name="p138461333114917"></a>收到确认短信或邮件之后，需要在48小时内处理，否则该功能订阅无效。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row157731032102814"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p1677373232818"><a name="p1677373232818"></a><a name="p1677373232818"></a>时延阈值</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p6681185532914"><a name="p6681185532914"></a><a name="p6681185532914"></a>源数据库和目标数据库之间的同步有时会存在一个时间差，称为时延，单位为秒。</p>
    <p id="p75251915133018"><a name="p75251915133018"></a><a name="p75251915133018"></a>时延阈值设置是指时延超过一定的值后（时间阈值范围为1—3600s），DRS可以发送告警通知给指定收件人。告警通知将在时延稳定超过设定的阈值6min后发送，避免出现由于时延波动反复发送告警通知的情况。</p>
    <div class="note" id="note47298209309"><a name="note47298209309"></a><a name="note47298209309"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p2875121535713"><a name="p2875121535713"></a><a name="p2875121535713"></a>设置时间阈值之前，需要填写收件人手机号或邮箱。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row23664659204420"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p37789232204420"><a name="p37789232204420"></a><a name="p37789232204420"></a>描述</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p41028970204420"><a name="p41028970204420"></a><a name="p41028970204420"></a>描述不能超过256位，且不能包含!&lt;&gt;&amp;'\"特殊字符。</p>
    </td>
    </tr>
    </tbody>
    </table>

    **图 2**  迁移实例信息-Oracle<a name="fig6487192516156"></a>  
    ![](figures/迁移实例信息-Oracle.png "迁移实例信息-Oracle")

    **表 4**  迁移实例信息

    <a name="table54580728204436"></a>
    <table><thead align="left"><tr id="row39932329204436"><th class="cellrowborder" valign="top" width="23.87%" id="mcps1.2.3.1.1"><p id="p13293221204436"><a name="p13293221204436"></a><a name="p13293221204436"></a><strong id="b2587841611355"><a name="b2587841611355"></a><a name="b2587841611355"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.13%" id="mcps1.2.3.1.2"><p id="p3009113204436"><a name="p3009113204436"></a><a name="p3009113204436"></a><strong id="b1577696211355"><a name="b1577696211355"></a><a name="b1577696211355"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row05147381129"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p951443871218"><a name="p951443871218"></a><a name="p951443871218"></a>数据流动方向</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p11514173891212"><a name="p11514173891212"></a><a name="p11514173891212"></a>选择入云。</p>
    <p id="p1983838136"><a name="p1983838136"></a><a name="p1983838136"></a>入云指目标端数据库为华为云关系型数据库。</p>
    </td>
    </tr>
    <tr id="row0414184610580"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1414046115813"><a name="p1414046115813"></a><a name="p1414046115813"></a>源数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p168249357197"><a name="p168249357197"></a><a name="p168249357197"></a>选择Oracle。</p>
    </td>
    </tr>
    <tr id="row42411630204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p12790028204436"><a name="p12790028204436"></a><a name="p12790028204436"></a>目标数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1969552512018"><a name="p1969552512018"></a><a name="p1969552512018"></a>选择PostgreSQL。</p>
    </td>
    </tr>
    <tr id="row62907306204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p62327044204436"><a name="p62327044204436"></a><a name="p62327044204436"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p34229323253"><a name="p34229323253"></a><a name="p34229323253"></a>默认为公网网络类型，支持公网网络和VPN、专线网络。</p>
    <p id="p2932133722411"><a name="p2932133722411"></a><a name="p2932133722411"></a>您可以根据实际情况选用合适的网络方式，此处以公网网络方式为示例。</p>
    </td>
    </tr>
    <tr id="row658644204515"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p53350183204515"><a name="p53350183204515"></a><a name="p53350183204515"></a>目标数据库实例</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p26397538204515"><a name="p26397538204515"></a><a name="p26397538204515"></a>用户所创建的关系型数据库实例。</p>
    </td>
    </tr>
    <tr id="row1781142655112"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p128192616518"><a name="p128192616518"></a><a name="p128192616518"></a>迁移模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><div class="p" id="p1114513594359"><a name="p1114513594359"></a><a name="p1114513594359"></a>全量：该模式为数据库一次性迁移，适用于可中断业务的<span class="keyword" id="keyword8520910122110"><a name="keyword8520910122110"></a><a name="keyword8520910122110"></a>数据库迁移</span>场景，全量迁移将用户选择的数据库对象和数据一次性迁移至目标端数据库。<div class="note" id="note1989394717302"><a name="note1989394717302"></a><a name="note1989394717302"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p12614191914218"><a name="p12614191914218"></a><a name="p12614191914218"></a>如果用户只进行全量迁移时，建议停止对源数据库的操作，否则迁移过程中源数据库产生的新数据不会同步到目标数据库。</p>
    </div></div>
    </div>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，迁移实例创建成功后，填选源库信息和目标库信息，建议您单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，勾选协议，单击“下一步“。

    **图 3**  源库信息配置-Oracle<a name="fig7958531468"></a>  
    ![](figures/源库信息配置-Oracle.png "源库信息配置-Oracle")

    **表 5**  源库信息

    <a name="table5827152923"></a>
    <table><thead align="left"><tr id="row48273219210"><th class="cellrowborder" valign="top" width="22.869999999999997%" id="mcps1.2.3.1.1"><p id="p198276214213"><a name="p198276214213"></a><a name="p198276214213"></a><strong id="b98275220212"><a name="b98275220212"></a><a name="b98275220212"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="77.13%" id="mcps1.2.3.1.2"><p id="p1282713218211"><a name="p1282713218211"></a><a name="p1282713218211"></a><strong id="b168271421523"><a name="b168271421523"></a><a name="b168271421523"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row198277210215"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p68272021227"><a name="p68272021227"></a><a name="p68272021227"></a>IP地址或域名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p696045254811"><a name="p696045254811"></a><a name="p696045254811"></a>源数据库的IP地址或域名。</p>
    </td>
    </tr>
    <tr id="row1982742821"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p3827162426"><a name="p3827162426"></a><a name="p3827162426"></a>端口</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p1082792823"><a name="p1082792823"></a><a name="p1082792823"></a>源数据库服务端口，可输入范围为1~65535间的整数。</p>
    </td>
    </tr>
    <tr id="row188271221621"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p16827121429"><a name="p16827121429"></a><a name="p16827121429"></a>数据库服务名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p1282702525"><a name="p1282702525"></a><a name="p1282702525"></a>数据库服务名（Service Name/SID）指定了客户端可以通过其连接到Oracle数据库。</p>
    <p id="p34591096106"><a name="p34591096106"></a><a name="p34591096106"></a>配置该项信息时，选填Service Name或者SID中任何一种均可，具体的名称需要与所选的类型对应。</p>
    <p id="p188910613418"><a name="p188910613418"></a><a name="p188910613418"></a>您可以通过如下方法获取具体的数据库服务名，查询数据库服务名称时需要使用具备DBA权限的用户进行查询：</p>
    <a name="ul1185073217520"></a><a name="ul1185073217520"></a><ul id="ul1185073217520"><li>查看Service Name：使用如下语句中任何一种均可。<a name="ul563302616"></a><a name="ul563302616"></a><ul id="ul563302616"><li>语句一<pre class="codeblock" id="codeblock634110220129"><a name="codeblock634110220129"></a><a name="codeblock634110220129"></a>select value from v$parameter where name like '%service_name%';</pre>
    </li><li>语句二<pre class="codeblock" id="codeblock1736711012134"><a name="codeblock1736711012134"></a><a name="codeblock1736711012134"></a>show parameter service_name;</pre>
    </li></ul>
    </li><li>查看SID：<pre class="codeblock" id="codeblock933642420138"><a name="codeblock933642420138"></a><a name="codeblock933642420138"></a>select instance_name from V$instance;</pre>
    </li></ul>
    </td>
    </tr>
    <tr id="row16827162722"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p128271529210"><a name="p128271529210"></a><a name="p128271529210"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p1754762917167"><a name="p1754762917167"></a><a name="p1754762917167"></a>源数据库的用户名。</p>
    </td>
    </tr>
    <tr id="row178118576471"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p181195714474"><a name="p181195714474"></a><a name="p181195714474"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p2826124491610"><a name="p2826124491610"></a><a name="p2826124491610"></a>源数据库的用户名所对应的密码。</p>
    </td>
    </tr>
    <tr id="row1798013414810"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p59804420484"><a name="p59804420484"></a><a name="p59804420484"></a>SSL安全连接</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p10548132911617"><a name="p10548132911617"></a><a name="p10548132911617"></a>通过该功能，用户可以选择是否开启对迁移链路的加密，如果开启，需要用户上传SSL CA根证书。</p>
    </td>
    </tr>
    </tbody>
    </table>

    **图 4**  目标库信息配置-PostgreSQL<a name="fig348042394017"></a>  
    ![](figures/目标库信息配置-PostgreSQL.png "目标库信息配置-PostgreSQL")

    **表 6**  目标库信息

    <a name="table12827621220"></a>
    <table><thead align="left"><tr id="row28279213213"><th class="cellrowborder" valign="top" width="23%" id="mcps1.2.3.1.1"><p id="p10827621127"><a name="p10827621127"></a><a name="p10827621127"></a><strong id="b18277211214"><a name="b18277211214"></a><a name="b18277211214"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="77%" id="mcps1.2.3.1.2"><p id="p118271621920"><a name="p118271621920"></a><a name="p118271621920"></a><strong id="b48274219213"><a name="b48274219213"></a><a name="b48274219213"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row198271021525"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p11827172021"><a name="p11827172021"></a><a name="p11827172021"></a>数据库实例名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p382752323"><a name="p382752323"></a><a name="p382752323"></a>默认为创建迁移任务时选择的关系型数据库实例，不可进行修改。</p>
    </td>
    </tr>
    <tr id="row19827021723"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p138271521229"><a name="p138271521229"></a><a name="p138271521229"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p38271228213"><a name="p38271228213"></a><a name="p38271228213"></a>目标数据库对应的数据库用户名。</p>
    </td>
    </tr>
    <tr id="row16827721222"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p1682742623"><a name="p1682742623"></a><a name="p1682742623"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p121331113174115"><a name="p121331113174115"></a><a name="p121331113174115"></a>目标数据库对应的数据库密码。</p>
    <p id="p19827328211"><a name="p19827328211"></a><a name="p19827328211"></a>数据库用户名和密码将被系统加密暂存，直至该任务删除后清除。</p>
    </td>
    </tr>
    </tbody>
    </table>

4.  在“设定迁移“页面，设置迁移对象，单击“下一步“。

    **图 5**  设定迁移-Oracle<a name="fig46205265911"></a>  
    ![](figures/设定迁移-Oracle.png "设定迁移-Oracle")

    **表 7**  迁移对象

    <a name="table165921932111919"></a>
    <table><thead align="left"><tr id="row165921632141911"><th class="cellrowborder" valign="top" width="16%" id="mcps1.2.3.1.1"><p id="p1759233261916"><a name="p1759233261916"></a><a name="p1759233261916"></a><strong id="b1783318515228"><a name="b1783318515228"></a><a name="b1783318515228"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="84%" id="mcps1.2.3.1.2"><p id="p159273271920"><a name="p159273271920"></a><a name="p159273271920"></a><strong id="b10555114922418"><a name="b10555114922418"></a><a name="b10555114922418"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row559273214193"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p14592132171916"><a name="p14592132171916"></a><a name="p14592132171916"></a>迁移对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p884981051017"><a name="p884981051017"></a><a name="p884981051017"></a>目前迁移对象仅支持自定义对象，选择的粒度为视图和表，迁移对象最多只能选择一个数据库。 数据库对象迁移成功之后，在目标数据库中以小写的名称进行保存。</p>
    <div class="note" id="note6192135932115"><a name="note6192135932115"></a><a name="note6192135932115"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p161921759152114"><a name="p161921759152114"></a><a name="p161921759152114"></a>若所选的数据库进行迁移时，由于视图、表等对象可能与其他数据库的视图、表存在依赖关系，若所依赖的视图或表未迁移，则会导致迁移失败。建议您在迁移之前进行确认。</p>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

5.  在“预检查“页面，进行迁移任务预校验，校验是否可进行迁移。
    -   查看检查结果，如有失败的检查项，需要修复失败项后，单击“重新校验”按钮重新进行迁移任务预校验。

        预检查失败项处理建议请参见《数据复制服务用户指南》中的“[预检查失败项修复方法](https://support.huaweicloud.com/usermanual-drs/drs_precheck.html)”。

        **图 6**  预检查-Oracle<a name="fig237882315489"></a>  
        ![](figures/预检查-Oracle.png "预检查-Oracle")


    -   预检查完成后，且预检查通过率为100%时，单击“下一步”。

        >![](public_sys-resources/icon-note.gif) **说明：**   
        >所有检查项结果均成功时，若存在告警，需要阅读并确认告警详情后才可以继续执行下一步操作。  


6.  在“任务确认“页面，设置迁移任务的启动时间，并确认迁移任务信息无误后，勾选协议，单击“启动任务“，提交迁移任务。

    **图 7**  任务确认-Oracle<a name="fig2736101920515"></a>  
    ![](figures/任务确认-Oracle.png "任务确认-Oracle")

    迁移任务的启动时间可以根据业务需求，设置为“立即启动”或“稍后启动”。

    预计迁移任务启动后，会对源数据库和目标数据库的性能产生影响，建议选择业务低峰期，合理设置迁移任务的启动时间。

7.  迁移任务提交后，您可在“在线迁移管理“页面，查看并管理自己的任务。
    -   您可查看任务提交后的状态，状态请参见[任务状态](zh-cn_topic_0082317249.md)。
    -   在任务列表的右上角，单击![](figures/kwx318612-GAUSS-DBaaS-image-a8fbc7b6-eab2-4798-b522-174e36341a92-3.png)刷新列表，可查看到最新的任务状态。

8.  迁移任务创建成功后，请参见《数据复制服务快速入门》的[使用流程](https://support.huaweicloud.com/qs-drs/drs_02_0001.html)，进行完整的数据业务割接。


# 低版本迁移至MySQL 8.0，应该注意哪些问题<a name="drs_04_0030"></a>

MySQL 8.0较MySQL 5.7增加了一些新的特性，并在性能表现上存在差异。迁移前，需要做兼容性分析并给出解决方案。可以从兼容性、系统变量等方面考虑。

-   兼容性分析：

    针对MySQL8.0社区版与MySQL5.7社区版进行分析，包括以下两方面：

    1.  不影响迁移，但使用方法出现差异。

        <a name="table772141625111"></a>
        <table><tbody><tr id="row4995131612517"><td class="cellrowborder" valign="top" width="13.120000000000001%"><p id="p129952016145113"><a name="p129952016145113"></a><a name="p129952016145113"></a>兼容性</p>
        </td>
        <td class="cellrowborder" valign="top" width="28.110000000000003%"><p id="p1899513161516"><a name="p1899513161516"></a><a name="p1899513161516"></a>检查项</p>
        </td>
        <td class="cellrowborder" valign="top" width="10.71%"><p id="p13995141625118"><a name="p13995141625118"></a><a name="p13995141625118"></a>作用</p>
        </td>
        <td class="cellrowborder" valign="top" width="7.920000000000001%"><p id="p39950163517"><a name="p39950163517"></a><a name="p39950163517"></a>状态</p>
        </td>
        <td class="cellrowborder" valign="top" width="40.14%"><p id="p1999551612514"><a name="p1999551612514"></a><a name="p1999551612514"></a>解决方案</p>
        </td>
        </tr>
        <tr id="row49962016205112"><td class="cellrowborder" rowspan="8" valign="top" width="13.120000000000001%"><p id="p599691655116"><a name="p599691655116"></a><a name="p599691655116"></a>数据类型或函数</p>
        </td>
        <td class="cellrowborder" valign="top" width="28.110000000000003%"><p id="p10996191613519"><a name="p10996191613519"></a><a name="p10996191613519"></a>ENCODE()函数</p>
        </td>
        <td class="cellrowborder" valign="top" width="10.71%"><p id="p19996141620517"><a name="p19996141620517"></a><a name="p19996141620517"></a>加密</p>
        </td>
        <td class="cellrowborder" valign="top" width="7.920000000000001%"><p id="p1999651665111"><a name="p1999651665111"></a><a name="p1999651665111"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top" width="40.14%"><p id="p17996111613513"><a name="p17996111613513"></a><a name="p17996111613513"></a>AES_ENCRYPT()函数代替</p>
        </td>
        </tr>
        <tr id="row18996101611518"><td class="cellrowborder" valign="top"><p id="p79961716115116"><a name="p79961716115116"></a><a name="p79961716115116"></a>DECODE()函数</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p12996151655117"><a name="p12996151655117"></a><a name="p12996151655117"></a>解密</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p139961616115119"><a name="p139961616115119"></a><a name="p139961616115119"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p1699601617516"><a name="p1699601617516"></a><a name="p1699601617516"></a>AES_DECRYPT()函数代替</p>
        </td>
        </tr>
        <tr id="row499671655110"><td class="cellrowborder" valign="top"><p id="p1999641610511"><a name="p1999641610511"></a><a name="p1999641610511"></a>ENCRYPT()函数</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p20996171617511"><a name="p20996171617511"></a><a name="p20996171617511"></a>加密</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p1299611611511"><a name="p1299611611511"></a><a name="p1299611611511"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p189962016205118"><a name="p189962016205118"></a><a name="p189962016205118"></a>SHA2()函数代替</p>
        </td>
        </tr>
        <tr id="row0996216105114"><td class="cellrowborder" valign="top"><p id="p17996111617519"><a name="p17996111617519"></a><a name="p17996111617519"></a>DES_ENCRYPT()函数</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p1199619167514"><a name="p1199619167514"></a><a name="p1199619167514"></a>加密</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p159971216135117"><a name="p159971216135117"></a><a name="p159971216135117"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p899710168517"><a name="p899710168517"></a><a name="p899710168517"></a>AES_ENCRYPT()函数代替</p>
        </td>
        </tr>
        <tr id="row199718164518"><td class="cellrowborder" valign="top"><p id="p129978169516"><a name="p129978169516"></a><a name="p129978169516"></a>DES_DECRYPT()函数</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p699721665113"><a name="p699721665113"></a><a name="p699721665113"></a>解密</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p299710169514"><a name="p299710169514"></a><a name="p299710169514"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p9997151611513"><a name="p9997151611513"></a><a name="p9997151611513"></a>AES_DECRYPT()函数代替</p>
        </td>
        </tr>
        <tr id="row1899741611517"><td class="cellrowborder" valign="top"><p id="p799781605112"><a name="p799781605112"></a><a name="p799781605112"></a>JSON_APPEND()函数</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p79978161519"><a name="p79978161519"></a><a name="p79978161519"></a>增加json元素</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p199710168516"><a name="p199710168516"></a><a name="p199710168516"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p14997101635114"><a name="p14997101635114"></a><a name="p14997101635114"></a>JSON_ARRAY_APPEND()函数代替</p>
        </td>
        </tr>
        <tr id="row299871665117"><td class="cellrowborder" valign="top"><p id="p1299861655116"><a name="p1299861655116"></a><a name="p1299861655116"></a>PASSWORD()函数</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p11998151615119"><a name="p11998151615119"></a><a name="p11998151615119"></a>修改用户密码</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p1399891610514"><a name="p1399891610514"></a><a name="p1399891610514"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p79989166515"><a name="p79989166515"></a><a name="p79989166515"></a>ALTER USER user IDENTIFIED BY 'auth_string';</p>
        </td>
        </tr>
        <tr id="row4998201613519"><td class="cellrowborder" valign="top"><p id="p3998161665114"><a name="p3998161665114"></a><a name="p3998161665114"></a>JSON_MERGE()函数</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p399801625112"><a name="p399801625112"></a><a name="p399801625112"></a>将多个json合并为一个</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p0998816205117"><a name="p0998816205117"></a><a name="p0998816205117"></a>废弃</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p20998101619511"><a name="p20998101619511"></a><a name="p20998101619511"></a>JSON_MERGE_PERSERVE()函数代替</p>
        </td>
        </tr>
        <tr id="row12998416165114"><td class="cellrowborder" valign="top" width="13.120000000000001%"><p id="p8998151615117"><a name="p8998151615117"></a><a name="p8998151615117"></a>SQL MODE</p>
        </td>
        <td class="cellrowborder" valign="top" width="28.110000000000003%"><p id="p159983160510"><a name="p159983160510"></a><a name="p159983160510"></a>NO_AUTO_CREATE_USER、DB2, MAXDB, MSSQL, MYSQL323, MYSQL40, ORACLE, POSTGRESQL, NO_FIELD_OPTIONS, NO_KEY_OPTIONS, NO_TABLE_OPTIONS</p>
        </td>
        <td class="cellrowborder" valign="top" width="10.71%"><p id="p14998201616514"><a name="p14998201616514"></a><a name="p14998201616514"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top" width="7.920000000000001%"><p id="p7998416155111"><a name="p7998416155111"></a><a name="p7998416155111"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top" width="40.14%"><p id="p1799851616518"><a name="p1799851616518"></a><a name="p1799851616518"></a>-</p>
        </td>
        </tr>
        <tr id="row9999181617514"><td class="cellrowborder" valign="top" width="13.120000000000001%"><p id="p1299921618515"><a name="p1299921618515"></a><a name="p1299921618515"></a>外键约束长度</p>
        </td>
        <td class="cellrowborder" valign="top" width="28.110000000000003%"><p id="p5999131618515"><a name="p5999131618515"></a><a name="p5999131618515"></a>外键约束名称不能超过64个字符</p>
        </td>
        <td class="cellrowborder" valign="top" width="10.71%"><p id="p699913162518"><a name="p699913162518"></a><a name="p699913162518"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top" width="7.920000000000001%"><p id="p199911615513"><a name="p199911615513"></a><a name="p199911615513"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top" width="40.14%"><p id="p1099911619516"><a name="p1099911619516"></a><a name="p1099911619516"></a>SELECT TABLE_SCHEMA, TABLE_NAME FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME IN (SELECT LEFT(SUBSTR(ID,INSTR(ID,'/')+1), INSTR(SUBSTR(ID,INSTR(ID,'/')+1),'_ibfk_')-1) FROM INFORMATION_SCHEMA.INNODB_SYS_FOREIGN WHERE LENGTH(SUBSTR(ID,INSTR(ID,'/')+1))&gt;64);</p>
        <p id="p19999171665116"><a name="p19999171665116"></a><a name="p19999171665116"></a>使用ALTER TABLE调整长度</p>
        </td>
        </tr>
        <tr id="row10999716125117"><td class="cellrowborder" rowspan="7" valign="top" width="13.120000000000001%"><p id="p149996163514"><a name="p149996163514"></a><a name="p149996163514"></a>features</p>
        </td>
        <td class="cellrowborder" valign="top" width="28.110000000000003%"><p id="p0999141611517"><a name="p0999141611517"></a><a name="p0999141611517"></a>GRANT创建用户</p>
        </td>
        <td class="cellrowborder" valign="top" width="10.71%"><p id="p1499971635116"><a name="p1499971635116"></a><a name="p1499971635116"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top" width="7.920000000000001%"><p id="p17999316155112"><a name="p17999316155112"></a><a name="p17999316155112"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top" width="40.14%"><p id="p1999911167516"><a name="p1999911167516"></a><a name="p1999911167516"></a>CREATE USER</p>
        </td>
        </tr>
        <tr id="row1999941615119"><td class="cellrowborder" valign="top"><p id="p9999116125116"><a name="p9999116125116"></a><a name="p9999116125116"></a>GRANT修改用户信息</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p13999616125119"><a name="p13999616125119"></a><a name="p13999616125119"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p15999191625118"><a name="p15999191625118"></a><a name="p15999191625118"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p73801452201714"><a name="p73801452201714"></a><a name="p73801452201714"></a>ALTER USER</p>
        </td>
        </tr>
        <tr id="row999901610510"><td class="cellrowborder" valign="top"><p id="p199991316155113"><a name="p199991316155113"></a><a name="p199991316155113"></a>IDENTIFIED BY PASSWORD 'auth_string'</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p189991516165116"><a name="p189991516165116"></a><a name="p189991516165116"></a>设置密码</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p15999116195114"><a name="p15999116195114"></a><a name="p15999116195114"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p2999181625118"><a name="p2999181625118"></a><a name="p2999181625118"></a>IDENTIFIED WITH auth_plugin AS 'auth_string'</p>
        </td>
        </tr>
        <tr id="row89991716195110"><td class="cellrowborder" valign="top"><p id="p40171705113"><a name="p40171705113"></a><a name="p40171705113"></a>SQL语句中的\N</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p708171518"><a name="p708171518"></a><a name="p708171518"></a>NULL</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p60817165115"><a name="p60817165115"></a><a name="p60817165115"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p10817105115"><a name="p10817105115"></a><a name="p10817105115"></a>NULL代替</p>
        </td>
        </tr>
        <tr id="row50117155110"><td class="cellrowborder" valign="top"><p id="p16091719512"><a name="p16091719512"></a><a name="p16091719512"></a>PROCEDURE ANALYSE()语法</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p14081716516"><a name="p14081716516"></a><a name="p14081716516"></a>对MySQL字段值进行统计分析后给出建议的字段类型</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p808174519"><a name="p808174519"></a><a name="p808174519"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p1709176517"><a name="p1709176517"></a><a name="p1709176517"></a>-</p>
        </td>
        </tr>
        <tr id="row9081775112"><td class="cellrowborder" valign="top"><p id="p170101725118"><a name="p170101725118"></a><a name="p170101725118"></a>空间函数</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p602175513"><a name="p602175513"></a><a name="p602175513"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p20151711511"><a name="p20151711511"></a><a name="p20151711511"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p1301717165112"><a name="p1301717165112"></a><a name="p1301717165112"></a>-</p>
        </td>
        </tr>
        <tr id="row0014176518"><td class="cellrowborder" valign="top"><p id="p130317165118"><a name="p130317165118"></a><a name="p130317165118"></a>mysql_install_db</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p140191711518"><a name="p140191711518"></a><a name="p140191711518"></a>初始化</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p9001715510"><a name="p9001715510"></a><a name="p9001715510"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p8012177515"><a name="p8012177515"></a><a name="p8012177515"></a>mysqld --initialize或--initialize-insecure</p>
        </td>
        </tr>
        </tbody>
        </table>

    2.  影响迁移，需要提前做检查。

        <a name="table2907846165118"></a>
        <table><tbody><tr id="row74134715516"><td class="cellrowborder" valign="top" width="10.73%"><p id="p343470517"><a name="p343470517"></a><a name="p343470517"></a>兼容性</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.99%"><p id="p11444725115"><a name="p11444725115"></a><a name="p11444725115"></a>检查项</p>
        </td>
        <td class="cellrowborder" valign="top" width="8.75%"><p id="p14247115118"><a name="p14247115118"></a><a name="p14247115118"></a>作用</p>
        </td>
        <td class="cellrowborder" valign="top" width="6.49%"><p id="p1351479518"><a name="p1351479518"></a><a name="p1351479518"></a>状态</p>
        </td>
        <td class="cellrowborder" valign="top" width="32.83%"><p id="p1551447155119"><a name="p1551447155119"></a><a name="p1551447155119"></a>解决方案</p>
        </td>
        <td class="cellrowborder" valign="top" width="18.21%"><p id="p135184715111"><a name="p135184715111"></a><a name="p135184715111"></a>原始用法</p>
        </td>
        </tr>
        <tr id="row652474519"><td class="cellrowborder" valign="top" width="10.73%"><p id="p65104710519"><a name="p65104710519"></a><a name="p65104710519"></a>保留关键字</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.99%"><p id="p85104718515"><a name="p85104718515"></a><a name="p85104718515"></a>cume_dist、dense_rank、empty、except、first_value、grouping、groups、json_table、lag、last_value、lateral、lead、nth_value、ntile、of、over、percent_rank、rank、recursive、row_number、system、window</p>
        </td>
        <td class="cellrowborder" valign="top" width="8.75%"><p id="p4594725113"><a name="p4594725113"></a><a name="p4594725113"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top" width="6.49%"><p id="p6554717512"><a name="p6554717512"></a><a name="p6554717512"></a>新增</p>
        </td>
        <td class="cellrowborder" valign="top" width="32.83%"><p id="p45124725112"><a name="p45124725112"></a><a name="p45124725112"></a>SET sql_mode = 'ANSI_QUOTES'</p>
        </td>
        <td class="cellrowborder" valign="top" width="18.21%"><p id="p105104715120"><a name="p105104715120"></a><a name="p105104715120"></a>名称：数据库、表、索引、列、alias、view、存储过程、分区、表空间</p>
        </td>
        </tr>
        <tr id="row14554716511"><td class="cellrowborder" valign="top" width="10.73%"><p id="p19594713512"><a name="p19594713512"></a><a name="p19594713512"></a>字符集</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.99%"><p id="p125114735115"><a name="p125114735115"></a><a name="p125114735115"></a>UTF8MB3</p>
        </td>
        <td class="cellrowborder" valign="top" width="8.75%"><p id="p1551947205119"><a name="p1551947205119"></a><a name="p1551947205119"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top" width="6.49%"><p id="p165134795118"><a name="p165134795118"></a><a name="p165134795118"></a>废弃</p>
        </td>
        <td class="cellrowborder" valign="top" width="32.83%"><p id="p195144717511"><a name="p195144717511"></a><a name="p195144717511"></a>使用UTF8MB4代替</p>
        </td>
        <td class="cellrowborder" valign="top" width="18.21%"><p id="p05114712516"><a name="p05114712516"></a><a name="p05114712516"></a>-</p>
        </td>
        </tr>
        <tr id="row155164719516"><td class="cellrowborder" valign="top" width="10.73%"><p id="p1657471518"><a name="p1657471518"></a><a name="p1657471518"></a>分区表</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.99%"><p id="p2051547155117"><a name="p2051547155117"></a><a name="p2051547155117"></a>不得出现不支持本地分区的存储引擎的分区表</p>
        </td>
        <td class="cellrowborder" valign="top" width="8.75%"><p id="p195174785120"><a name="p195174785120"></a><a name="p195174785120"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top" width="6.49%"><p id="p18574710517"><a name="p18574710517"></a><a name="p18574710517"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top" width="32.83%"><p id="p35164719513"><a name="p35164719513"></a><a name="p35164719513"></a>SELECT TABLE_SCHEMA, TABLE_NAME FROM INFORMATION_SCHEMA.TABLES WHERE ENGINE NOT IN ('innodb', 'ndbcluster') AND CREATE_OPTIONS LIKE '%partitioned%';</p>
        <p id="p551347175111"><a name="p551347175111"></a><a name="p551347175111"></a>可按照下述两种方式解决：</p>
        <p id="p185447125117"><a name="p185447125117"></a><a name="p185447125117"></a>（1）ALTER TABLE table_name ENGINE=INNODB;</p>
        <p id="p195184712513"><a name="p195184712513"></a><a name="p195184712513"></a>（2）ALTER TABLE table_name REMOVE PARTITIONING;</p>
        </td>
        <td class="cellrowborder" valign="top" width="18.21%"><p id="p35647195116"><a name="p35647195116"></a><a name="p35647195116"></a>不支持MyISAM</p>
        </td>
        </tr>
        <tr id="row196747155120"><td class="cellrowborder" valign="top" width="10.73%"><p id="p761747195116"><a name="p761747195116"></a><a name="p761747195116"></a>语法</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.99%"><p id="p1861947205112"><a name="p1861947205112"></a><a name="p1861947205112"></a>group by … asc/desc</p>
        </td>
        <td class="cellrowborder" valign="top" width="8.75%"><p id="p166347105116"><a name="p166347105116"></a><a name="p166347105116"></a>升序/降序</p>
        </td>
        <td class="cellrowborder" valign="top" width="6.49%"><p id="p36174765120"><a name="p36174765120"></a><a name="p36174765120"></a>移除</p>
        </td>
        <td class="cellrowborder" valign="top" width="32.83%"><p id="p3654719510"><a name="p3654719510"></a><a name="p3654719510"></a>使用order by子句代替</p>
        </td>
        <td class="cellrowborder" valign="top" width="18.21%"><p id="p16347195116"><a name="p16347195116"></a><a name="p16347195116"></a>view、function等</p>
        </td>
        </tr>
        <tr id="row19620477519"><td class="cellrowborder" rowspan="2" valign="top" width="10.73%"><p id="p16694795116"><a name="p16694795116"></a><a name="p16694795116"></a>名称长度</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.99%"><p id="p96174775118"><a name="p96174775118"></a><a name="p96174775118"></a>view的列名称不能超过64个字符</p>
        </td>
        <td class="cellrowborder" valign="top" width="8.75%"><p id="p8634714511"><a name="p8634714511"></a><a name="p8634714511"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top" width="6.49%"><p id="p11624710516"><a name="p11624710516"></a><a name="p11624710516"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top" width="32.83%"><p id="p11624712511"><a name="p11624712511"></a><a name="p11624712511"></a>alter处理</p>
        </td>
        <td class="cellrowborder" valign="top" width="18.21%"><p id="p11611475516"><a name="p11611475516"></a><a name="p11611475516"></a>最多255个字符</p>
        </td>
        </tr>
        <tr id="row76144795113"><td class="cellrowborder" valign="top"><p id="p46747115116"><a name="p46747115116"></a><a name="p46747115116"></a>enum或set元素的总长度不能超过255个字符</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p368473514"><a name="p368473514"></a><a name="p368473514"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p156194719517"><a name="p156194719517"></a><a name="p156194719517"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p0618471510"><a name="p0618471510"></a><a name="p0618471510"></a>用户处理</p>
        </td>
        <td class="cellrowborder" valign="top"><p id="p106104755115"><a name="p106104755115"></a><a name="p106104755115"></a>最大64K</p>
        </td>
        </tr>
        <tr id="row3674714517"><td class="cellrowborder" valign="top" width="10.73%"><p id="p12694719511"><a name="p12694719511"></a><a name="p12694719511"></a>大小写</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.99%"><p id="p4714725114"><a name="p4714725114"></a><a name="p4714725114"></a>lower_case_table_names</p>
        </td>
        <td class="cellrowborder" valign="top" width="8.75%"><p id="p67047185113"><a name="p67047185113"></a><a name="p67047185113"></a>mysql设置字母大小写是否敏感</p>
        </td>
        <td class="cellrowborder" valign="top" width="6.49%"><p id="p5704710517"><a name="p5704710517"></a><a name="p5704710517"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top" width="32.83%"><p id="p171547175119"><a name="p171547175119"></a><a name="p171547175119"></a>升级过程中，如果设置该参数为1，则必须确保schema和table名称必须是小写的</p>
        <p id="p87174715119"><a name="p87174715119"></a><a name="p87174715119"></a>SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME != LOWER(TABLE_NAME) AND TABLE_TYPE = 'BASE TABLE';</p>
        <p id="p1571747115112"><a name="p1571747115112"></a><a name="p1571747115112"></a>SELECT SCHEMA_NAME FROM INFORMATION_SCHEMA.SCHEMATA WHERE SCHEMA_NAME != LOWER(SCHEMA_NAME);</p>
        </td>
        <td class="cellrowborder" valign="top" width="18.21%"><p id="p1671347205111"><a name="p1671347205111"></a><a name="p1671347205111"></a>-</p>
        </td>
        </tr>
        <tr id="row197164718516"><td class="cellrowborder" valign="top" width="10.73%"><p id="p2071447125110"><a name="p2071447125110"></a><a name="p2071447125110"></a>触发器</p>
        </td>
        <td class="cellrowborder" valign="top" width="22.99%"><p id="p971547165119"><a name="p971547165119"></a><a name="p971547165119"></a>是否有空定义或者无效的创建上下文</p>
        </td>
        <td class="cellrowborder" valign="top" width="8.75%"><p id="p14744715518"><a name="p14744715518"></a><a name="p14744715518"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top" width="6.49%"><p id="p571147165116"><a name="p571147165116"></a><a name="p571147165116"></a>-</p>
        </td>
        <td class="cellrowborder" valign="top" width="32.83%"><p id="p2754725112"><a name="p2754725112"></a><a name="p2754725112"></a>show triggers查看，检测character_set_client、 collation_connection、Database Collation属性</p>
        </td>
        <td class="cellrowborder" valign="top" width="18.21%"><p id="p0764745117"><a name="p0764745117"></a><a name="p0764745117"></a>-</p>
        </td>
        </tr>
        </tbody>
        </table>



-   系统变量默认值变更

    针对社区版MySQL5.7与8.0版本的默认值作对比，默认值不影响迁移，但对迁移后的业务会产生影响。

    <a name="table27641576596"></a>
    <table><tbody><tr id="row775785597"><td class="cellrowborder" rowspan="2" valign="top"><p id="p18757845916"><a name="p18757845916"></a><a name="p18757845916"></a>序号</p>
    </td>
    <td class="cellrowborder" rowspan="2" valign="top"><p id="p9751584597"><a name="p9751584597"></a><a name="p9751584597"></a>parameter/option</p>
    </td>
    <td class="cellrowborder" colspan="2" valign="top"><p id="p1875178185913"><a name="p1875178185913"></a><a name="p1875178185913"></a>community</p>
    </td>
    <td class="cellrowborder" rowspan="2" valign="top"><p id="p1475385595"><a name="p1475385595"></a><a name="p1475385595"></a>作用</p>
    </td>
    <td class="cellrowborder" rowspan="2" valign="top"><p id="p1075583595"><a name="p1075583595"></a><a name="p1075583595"></a>备注</p>
    </td>
    </tr>
    <tr id="row87519885913"><td class="cellrowborder" valign="top"><p id="p075128195917"><a name="p075128195917"></a><a name="p075128195917"></a>原默认值</p>
    </td>
    <td class="cellrowborder" valign="top"><p id="p77513810596"><a name="p77513810596"></a><a name="p77513810596"></a>新默认值</p>
    </td>
    </tr>
    <tr id="row157618835911"><td class="cellrowborder" colspan="6" valign="top"><p id="p117618805911"><a name="p117618805911"></a><a name="p117618805911"></a>Server</p>
    </td>
    </tr>
    <tr id="row13764885911"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p10761584599"><a name="p10761584599"></a><a name="p10761584599"></a>1</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p67608195915"><a name="p67608195915"></a><a name="p67608195915"></a>character_set_server</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1976789591"><a name="p1976789591"></a><a name="p1976789591"></a>latin1</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p776198175910"><a name="p776198175910"></a><a name="p776198175910"></a>utf8mb4</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p5768817595"><a name="p5768817595"></a><a name="p5768817595"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p137611825912"><a name="p137611825912"></a><a name="p137611825912"></a>和源保持一致</p>
    </td>
    </tr>
    <tr id="row7761988595"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p97612815597"><a name="p97612815597"></a><a name="p97612815597"></a>2</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p20769811594"><a name="p20769811594"></a><a name="p20769811594"></a>collation_server</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p476188145910"><a name="p476188145910"></a><a name="p476188145910"></a>latin1_swedish_ci</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p4778818598"><a name="p4778818598"></a><a name="p4778818598"></a>utf8mb4_0900_ai_ci</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p17758185910"><a name="p17758185910"></a><a name="p17758185910"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p107719811596"><a name="p107719811596"></a><a name="p107719811596"></a>和源保持一致</p>
    </td>
    </tr>
    <tr id="row77713885917"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p11771983596"><a name="p11771983596"></a><a name="p11771983596"></a>3</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p13771845919"><a name="p13771845919"></a><a name="p13771845919"></a>explicit_defaults_for_timestamp</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p187708105915"><a name="p187708105915"></a><a name="p187708105915"></a>OFF</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p87710810597"><a name="p87710810597"></a><a name="p87710810597"></a>ON</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p15778835917"><a name="p15778835917"></a><a name="p15778835917"></a>更新某一行时是否更新timestamp列</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p16771285591"><a name="p16771285591"></a><a name="p16771285591"></a>和源保持一致</p>
    </td>
    </tr>
    <tr id="row107718175911"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p4775812599"><a name="p4775812599"></a><a name="p4775812599"></a>4</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p127714805917"><a name="p127714805917"></a><a name="p127714805917"></a>optimizer_trace_max_mem_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p5771811593"><a name="p5771811593"></a><a name="p5771811593"></a>16KB</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1877181597"><a name="p1877181597"></a><a name="p1877181597"></a>1MB</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p97716814599"><a name="p97716814599"></a><a name="p97716814599"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p4782812599"><a name="p4782812599"></a><a name="p4782812599"></a>和源保持一致</p>
    </td>
    </tr>
    <tr id="row5781813593"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p107898195913"><a name="p107898195913"></a><a name="p107898195913"></a>5</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p6780817598"><a name="p6780817598"></a><a name="p6780817598"></a>validate_password_check_user_name</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1678481598"><a name="p1678481598"></a><a name="p1678481598"></a>OFF</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p978178155911"><a name="p978178155911"></a><a name="p978178155911"></a>ON</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1578181595"><a name="p1578181595"></a><a name="p1578181595"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1078688593"><a name="p1078688593"></a><a name="p1078688593"></a>和源保持一致</p>
    </td>
    </tr>
    <tr id="row1178689594"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p37818875916"><a name="p37818875916"></a><a name="p37818875916"></a>6</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p8784815919"><a name="p8784815919"></a><a name="p8784815919"></a>back_log</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1678283593"><a name="p1678283593"></a><a name="p1678283593"></a>-1 (autosize) changed from : back_log = 50 + (max_connections / 5)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p197820835913"><a name="p197820835913"></a><a name="p197820835913"></a>-1 (autosize) changed to : back_log = max_connections</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p15781384595"><a name="p15781384595"></a><a name="p15781384595"></a>在MySQL暂时停止回答新请求之前的短时间内多少个请求可以被存在堆栈中。</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p2781587593"><a name="p2781587593"></a><a name="p2781587593"></a>和源保持一致</p>
    </td>
    </tr>
    <tr id="row5783845915"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p12789835918"><a name="p12789835918"></a><a name="p12789835918"></a>7</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p17781486596"><a name="p17781486596"></a><a name="p17781486596"></a>max_allowed_packet</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p207819885920"><a name="p207819885920"></a><a name="p207819885920"></a>4194304 (4MB)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1379178175917"><a name="p1379178175917"></a><a name="p1379178175917"></a>67108864 (64MB)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p18791089593"><a name="p18791089593"></a><a name="p18791089593"></a>限制Server接受的数据包大小</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1779686598"><a name="p1779686598"></a><a name="p1779686598"></a>按默认值</p>
    </td>
    </tr>
    <tr id="row979108185913"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p8795814591"><a name="p8795814591"></a><a name="p8795814591"></a>8</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p16790845919"><a name="p16790845919"></a><a name="p16790845919"></a>max_error_count</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p37913810599"><a name="p37913810599"></a><a name="p37913810599"></a>64</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p179983596"><a name="p179983596"></a><a name="p179983596"></a>1024</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p27916814595"><a name="p27916814595"></a><a name="p27916814595"></a>控制显示告警的个数</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1279488591"><a name="p1279488591"></a><a name="p1279488591"></a>和源保持一致</p>
    </td>
    </tr>
    <tr id="row079118125918"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p2791385594"><a name="p2791385594"></a><a name="p2791385594"></a>9</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p137968135920"><a name="p137968135920"></a><a name="p137968135920"></a>event_scheduler</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p2797855911"><a name="p2797855911"></a><a name="p2797855911"></a>OFF</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p5791083594"><a name="p5791083594"></a><a name="p5791083594"></a>ON</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p16794855920"><a name="p16794855920"></a><a name="p16794855920"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p11794875914"><a name="p11794875914"></a><a name="p11794875914"></a>和源保持一致</p>
    </td>
    </tr>
    <tr id="row379168195913"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p12797835919"><a name="p12797835919"></a><a name="p12797835919"></a>10</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p12801865919"><a name="p12801865919"></a><a name="p12801865919"></a>table_open_cache</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p188015845917"><a name="p188015845917"></a><a name="p188015845917"></a>2000</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p14802810595"><a name="p14802810595"></a><a name="p14802810595"></a>4000</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p6801983599"><a name="p6801983599"></a><a name="p6801983599"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p208015818598"><a name="p208015818598"></a><a name="p208015818598"></a>和源保持一致</p>
    </td>
    </tr>
    <tr id="row68058145910"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p78015819597"><a name="p78015819597"></a><a name="p78015819597"></a>11</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p18802819598"><a name="p18802819598"></a><a name="p18802819598"></a>log_error_verbosity</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p7802814594"><a name="p7802814594"></a><a name="p7802814594"></a>3 (Notes)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p7809845918"><a name="p7809845918"></a><a name="p7809845918"></a>2 (Warning)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1480181598"><a name="p1480181598"></a><a name="p1480181598"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p38068135917"><a name="p38068135917"></a><a name="p38068135917"></a>按默认值</p>
    </td>
    </tr>
    <tr id="row180208135913"><td class="cellrowborder" colspan="6" valign="top"><p id="p1380887599"><a name="p1380887599"></a><a name="p1380887599"></a>INNODB</p>
    </td>
    </tr>
    <tr id="row168048195916"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p080885591"><a name="p080885591"></a><a name="p080885591"></a>1</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p580198135920"><a name="p580198135920"></a><a name="p580198135920"></a>innodb_undo_tablespaces</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p48015875919"><a name="p48015875919"></a><a name="p48015875919"></a>0</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p880382591"><a name="p880382591"></a><a name="p880382591"></a>2</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1801880597"><a name="p1801880597"></a><a name="p1801880597"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p8809817598"><a name="p8809817598"></a><a name="p8809817598"></a>按默认值</p>
    </td>
    </tr>
    <tr id="row9803895919"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p681980598"><a name="p681980598"></a><a name="p681980598"></a>2</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p19817819594"><a name="p19817819594"></a><a name="p19817819594"></a>innodb_undo_log_truncate</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p168118895913"><a name="p168118895913"></a><a name="p168118895913"></a>OFF</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p2812820593"><a name="p2812820593"></a><a name="p2812820593"></a>ON</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1981208145917"><a name="p1981208145917"></a><a name="p1981208145917"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p3811982596"><a name="p3811982596"></a><a name="p3811982596"></a>按默认值</p>
    </td>
    </tr>
    <tr id="row2817805918"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p381188185917"><a name="p381188185917"></a><a name="p381188185917"></a>3</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p19811982598"><a name="p19811982598"></a><a name="p19811982598"></a>innodb_flush_method</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p6811815597"><a name="p6811815597"></a><a name="p6811815597"></a>NULL</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p281680596"><a name="p281680596"></a><a name="p281680596"></a>fsync (Unix),</p>
    <p id="p68118125917"><a name="p68118125917"></a><a name="p68118125917"></a>unbuffered (Windows)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p148110855917"><a name="p148110855917"></a><a name="p148110855917"></a>控制innodb数据文件及redo log的打开、刷写模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p148114815591"><a name="p148114815591"></a><a name="p148114815591"></a>按hwsql默认值O_DIRECT</p>
    </td>
    </tr>
    <tr id="row781158155911"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p17814818596"><a name="p17814818596"></a><a name="p17814818596"></a>4</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p12818811595"><a name="p12818811595"></a><a name="p12818811595"></a>innodb_autoinc_lock_mode</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1181198205917"><a name="p1181198205917"></a><a name="p1181198205917"></a>1 (consecutive)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p881198165910"><a name="p881198165910"></a><a name="p881198165910"></a>2 (interleaved)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p188117815913"><a name="p188117815913"></a><a name="p188117815913"></a>控制着在向有auto_increment 列的表插入数据时，相关锁的行为；</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p2811687597"><a name="p2811687597"></a><a name="p2811687597"></a>和源保持一致</p>
    </td>
    </tr>
    <tr id="row9811081595"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p5815825916"><a name="p5815825916"></a><a name="p5815825916"></a>5</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p19812812591"><a name="p19812812591"></a><a name="p19812812591"></a>innodb_flush_neighbors</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p3819813599"><a name="p3819813599"></a><a name="p3819813599"></a>1 (enable)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p158114812598"><a name="p158114812598"></a><a name="p158114812598"></a>0 (disable)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p17829812590"><a name="p17829812590"></a><a name="p17829812590"></a>从缓冲池刷新页面是否也刷新相同范围内的其他脏页。</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p118220815916"><a name="p118220815916"></a><a name="p118220815916"></a>和源保持一致</p>
    </td>
    </tr>
    <tr id="row138217810592"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1982148155917"><a name="p1982148155917"></a><a name="p1982148155917"></a>6</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p98258155914"><a name="p98258155914"></a><a name="p98258155914"></a>innodb_max_dirty_pages_pct_lwm</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p10823805913"><a name="p10823805913"></a><a name="p10823805913"></a>0 (%)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p78210812597"><a name="p78210812597"></a><a name="p78210812597"></a>10 (%)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p14828814598"><a name="p14828814598"></a><a name="p14828814598"></a>影响innodb刷新脏页行为</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p482684591"><a name="p482684591"></a><a name="p482684591"></a>按默认值</p>
    </td>
    </tr>
    <tr id="row48215819598"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p78298175916"><a name="p78298175916"></a><a name="p78298175916"></a>7</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p48211865918"><a name="p48211865918"></a><a name="p48211865918"></a>innodb_max_dirty_pages_pct</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p14822835910"><a name="p14822835910"></a><a name="p14822835910"></a>75 (%)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p158216805916"><a name="p158216805916"></a><a name="p158216805916"></a>90 (%)</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p19828818595"><a name="p19828818595"></a><a name="p19828818595"></a>影响innodb刷新脏页行为</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p682148185918"><a name="p682148185918"></a><a name="p682148185918"></a>按默认值</p>
    </td>
    </tr>
    <tr id="row8822812598"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p482680594"><a name="p482680594"></a><a name="p482680594"></a>PERFORMANCE SCHEMA</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1382108125917"><a name="p1382108125917"></a><a name="p1382108125917"></a>整体是不是开的</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p12826815592"><a name="p12826815592"></a><a name="p12826815592"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p582486597"><a name="p582486597"></a><a name="p582486597"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p58220818593"><a name="p58220818593"></a><a name="p58220818593"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p382128195912"><a name="p382128195912"></a><a name="p382128195912"></a>和源保持一致</p>
    </td>
    </tr>
    <tr id="row108288205910"><td class="cellrowborder" colspan="6" valign="top"><p id="p6828855915"><a name="p6828855915"></a><a name="p6828855915"></a>REPLICATION</p>
    </td>
    </tr>
    <tr id="row1283198165910"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p19838816595"><a name="p19838816595"></a><a name="p19838816595"></a>1</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p4835835914"><a name="p4835835914"></a><a name="p4835835914"></a>log_bin</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p3837810594"><a name="p3837810594"></a><a name="p3837810594"></a>OFF</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1283208135916"><a name="p1283208135916"></a><a name="p1283208135916"></a>ON</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p7838811592"><a name="p7838811592"></a><a name="p7838811592"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p12831389599"><a name="p12831389599"></a><a name="p12831389599"></a>默认打开</p>
    </td>
    </tr>
    <tr id="row48317813593"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p4837805912"><a name="p4837805912"></a><a name="p4837805912"></a>2</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p18310813597"><a name="p18310813597"></a><a name="p18310813597"></a>server_id</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p198398115919"><a name="p198398115919"></a><a name="p198398115919"></a>0</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p88368195915"><a name="p88368195915"></a><a name="p88368195915"></a>1</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p88320819590"><a name="p88320819590"></a><a name="p88320819590"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p183483593"><a name="p183483593"></a><a name="p183483593"></a>如果是0，则设为1</p>
    </td>
    </tr>
    <tr id="row19835845915"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p58388125913"><a name="p58388125913"></a><a name="p58388125913"></a>3</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p8838875916"><a name="p8838875916"></a><a name="p8838875916"></a>log-slave-updates</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p9831287592"><a name="p9831287592"></a><a name="p9831287592"></a>OFF</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p6831889593"><a name="p6831889593"></a><a name="p6831889593"></a>ON</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p19831189594"><a name="p19831189594"></a><a name="p19831189594"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p148338175910"><a name="p148338175910"></a><a name="p148338175910"></a>默认打开</p>
    </td>
    </tr>
    <tr id="row883178125914"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p483181597"><a name="p483181597"></a><a name="p483181597"></a>4</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p6838835918"><a name="p6838835918"></a><a name="p6838835918"></a>expire_log_days</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p198416895912"><a name="p198416895912"></a><a name="p198416895912"></a>0</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p18419813594"><a name="p18419813594"></a><a name="p18419813594"></a>30</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1984786597"><a name="p1984786597"></a><a name="p1984786597"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p15847815593"><a name="p15847815593"></a><a name="p15847815593"></a>按默认值1</p>
    </td>
    </tr>
    <tr id="row284883595"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1084381591"><a name="p1084381591"></a><a name="p1084381591"></a>5</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p10845875917"><a name="p10845875917"></a><a name="p10845875917"></a>master-info-repository</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p13848818597"><a name="p13848818597"></a><a name="p13848818597"></a>FILE</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p4843895915"><a name="p4843895915"></a><a name="p4843895915"></a>TABLE</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p48418155914"><a name="p48418155914"></a><a name="p48418155914"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1284158145917"><a name="p1284158145917"></a><a name="p1284158145917"></a>默认TABLE</p>
    </td>
    </tr>
    <tr id="row484188115913"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p118416815911"><a name="p118416815911"></a><a name="p118416815911"></a>6</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p284108155913"><a name="p284108155913"></a><a name="p284108155913"></a>relay-log-info-repository</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p138718845918"><a name="p138718845918"></a><a name="p138718845918"></a>FILE</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p118738115914"><a name="p118738115914"></a><a name="p118738115914"></a>TABLE</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p7881186597"><a name="p7881186597"></a><a name="p7881186597"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p17882819591"><a name="p17882819591"></a><a name="p17882819591"></a>默认TABLE</p>
    </td>
    </tr>
    <tr id="row168914855918"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p7897818594"><a name="p7897818594"></a><a name="p7897818594"></a>7</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p8897815917"><a name="p8897815917"></a><a name="p8897815917"></a>transaction-write-set-extraction</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p13891783595"><a name="p13891783595"></a><a name="p13891783595"></a>OFF</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1289158135915"><a name="p1289158135915"></a><a name="p1289158135915"></a>XXHASH64</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p16891089593"><a name="p16891089593"></a><a name="p16891089593"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p88988135917"><a name="p88988135917"></a><a name="p88988135917"></a>按默认值</p>
    </td>
    </tr>
    <tr id="row48918812594"><td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p198916845915"><a name="p198916845915"></a><a name="p198916845915"></a>8</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p10891819595"><a name="p10891819595"></a><a name="p10891819595"></a>slave_rows_search_algorithms</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1789118115914"><a name="p1789118115914"></a><a name="p1789118115914"></a>INDEX_SCAN, TABLE_SCAN</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p1089586596"><a name="p1089586596"></a><a name="p1089586596"></a>INDEX_SCAN, HASH_SCAN</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p138912875911"><a name="p138912875911"></a><a name="p138912875911"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="16.666666666666664%"><p id="p58919818595"><a name="p58919818595"></a><a name="p58919818595"></a>按默认值</p>
    </td>
    </tr>
    </tbody>
    </table>

-   移除系统变量

    针对社区版MySQL 5.7与8.0进行分析，移除系统变量不影响迁移。

    <a name="table18442304115"></a>
    <table><tbody><tr id="row784219305116"><td class="cellrowborder" valign="top" width="100%"><p id="p1384110301516"><a name="p1384110301516"></a><a name="p1384110301516"></a>移除变量</p>
    </td>
    </tr>
    <tr id="row158422305112"><td class="cellrowborder" valign="top" width="100%"><p id="p68421301117"><a name="p68421301117"></a><a name="p68421301117"></a>innodb_locks_unsafe_for_binlog</p>
    </td>
    </tr>
    <tr id="row2842630812"><td class="cellrowborder" valign="top" width="100%"><p id="p78422301218"><a name="p78422301218"></a><a name="p78422301218"></a>log_builtin_as_identified_by_password</p>
    </td>
    </tr>
    <tr id="row18423301619"><td class="cellrowborder" valign="top" width="100%"><p id="p184213301711"><a name="p184213301711"></a><a name="p184213301711"></a>old_passwords</p>
    </td>
    </tr>
    <tr id="row188429301512"><td class="cellrowborder" valign="top" width="100%"><p id="p1084219301315"><a name="p1084219301315"></a><a name="p1084219301315"></a>query_cache_limit</p>
    </td>
    </tr>
    <tr id="row178421309110"><td class="cellrowborder" valign="top" width="100%"><p id="p1084203017112"><a name="p1084203017112"></a><a name="p1084203017112"></a>query_cache_min_res_unit</p>
    </td>
    </tr>
    <tr id="row7842133018115"><td class="cellrowborder" valign="top" width="100%"><p id="p6842930612"><a name="p6842930612"></a><a name="p6842930612"></a>query_cache_size</p>
    </td>
    </tr>
    <tr id="row3842230414"><td class="cellrowborder" valign="top" width="100%"><p id="p58429301819"><a name="p58429301819"></a><a name="p58429301819"></a>query_cache_type</p>
    </td>
    </tr>
    <tr id="row1184219303117"><td class="cellrowborder" valign="top" width="100%"><p id="p684210302111"><a name="p684210302111"></a><a name="p684210302111"></a>query_cache_wlock_invalidate</p>
    </td>
    </tr>
    <tr id="row4842193019110"><td class="cellrowborder" valign="top" width="100%"><p id="p5842183017117"><a name="p5842183017117"></a><a name="p5842183017117"></a>ndb_cache_check_time</p>
    </td>
    </tr>
    <tr id="row1184211306110"><td class="cellrowborder" valign="top" width="100%"><p id="p884210301013"><a name="p884210301013"></a><a name="p884210301013"></a>ignore_db_dirs</p>
    </td>
    </tr>
    <tr id="row484283020110"><td class="cellrowborder" valign="top" width="100%"><p id="p1684220302114"><a name="p1684220302114"></a><a name="p1684220302114"></a>tx_isolation</p>
    </td>
    </tr>
    <tr id="row20842530819"><td class="cellrowborder" valign="top" width="100%"><p id="p19842163012111"><a name="p19842163012111"></a><a name="p19842163012111"></a>tx_read_only</p>
    </td>
    </tr>
    <tr id="row12843730310"><td class="cellrowborder" valign="top" width="100%"><p id="p4842930117"><a name="p4842930117"></a><a name="p4842930117"></a>sync_frm</p>
    </td>
    </tr>
    <tr id="row1584323019111"><td class="cellrowborder" valign="top" width="100%"><p id="p38435302011"><a name="p38435302011"></a><a name="p38435302011"></a>secure_auth</p>
    </td>
    </tr>
    <tr id="row98431230215"><td class="cellrowborder" valign="top" width="100%"><p id="p14843630314"><a name="p14843630314"></a><a name="p14843630314"></a>multi_range_count</p>
    </td>
    </tr>
    <tr id="row98436306111"><td class="cellrowborder" valign="top" width="100%"><p id="p12843103020119"><a name="p12843103020119"></a><a name="p12843103020119"></a>log_error_verbosity</p>
    </td>
    </tr>
    <tr id="row2843730517"><td class="cellrowborder" valign="top" width="100%"><p id="p1884317307110"><a name="p1884317307110"></a><a name="p1884317307110"></a>sql_log_bin</p>
    </td>
    </tr>
    <tr id="row0843133013112"><td class="cellrowborder" valign="top" width="100%"><p id="p2843183012119"><a name="p2843183012119"></a><a name="p2843183012119"></a>metadata_locks_cache_size</p>
    </td>
    </tr>
    <tr id="row178430302119"><td class="cellrowborder" valign="top" width="100%"><p id="p284313309113"><a name="p284313309113"></a><a name="p284313309113"></a>metadata_locks_hash_instances</p>
    </td>
    </tr>
    <tr id="row3843830611"><td class="cellrowborder" valign="top" width="100%"><p id="p3843143017112"><a name="p3843143017112"></a><a name="p3843143017112"></a>date_format</p>
    </td>
    </tr>
    <tr id="row148436301117"><td class="cellrowborder" valign="top" width="100%"><p id="p14843530012"><a name="p14843530012"></a><a name="p14843530012"></a>datetime_format</p>
    </td>
    </tr>
    <tr id="row17843133018118"><td class="cellrowborder" valign="top" width="100%"><p id="p1843130114"><a name="p1843130114"></a><a name="p1843130114"></a>time_format</p>
    </td>
    </tr>
    <tr id="row15843193016120"><td class="cellrowborder" valign="top" width="100%"><p id="p15843130012"><a name="p15843130012"></a><a name="p15843130012"></a>max_tmp_tables</p>
    </td>
    </tr>
    <tr id="row178434307116"><td class="cellrowborder" valign="top" width="100%"><p id="p198431730717"><a name="p198431730717"></a><a name="p198431730717"></a>ignore_builtin_innodb</p>
    </td>
    </tr>
    <tr id="row2843103018112"><td class="cellrowborder" valign="top" width="100%"><p id="p2843123017116"><a name="p2843123017116"></a><a name="p2843123017116"></a>innodb_support_xa</p>
    </td>
    </tr>
    <tr id="row384317301714"><td class="cellrowborder" valign="top" width="100%"><p id="p1984315301617"><a name="p1984315301617"></a><a name="p1984315301617"></a>innodb_undo_logs</p>
    </td>
    </tr>
    <tr id="row19844130219"><td class="cellrowborder" valign="top" width="100%"><p id="p1784319301713"><a name="p1784319301713"></a><a name="p1784319301713"></a>innodb_undo_tablespaces</p>
    </td>
    </tr>
    <tr id="row78441230111"><td class="cellrowborder" valign="top" width="100%"><p id="p284415305116"><a name="p284415305116"></a><a name="p284415305116"></a>internal_tmp_disk_storage_engine</p>
    </td>
    </tr>
    </tbody>
    </table>



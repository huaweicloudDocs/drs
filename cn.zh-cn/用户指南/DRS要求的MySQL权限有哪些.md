# DRS要求的MySQL权限有哪些<a name="drs_04_0034"></a>

DRS在迁移、同步、灾备过程中，对帐号有一定的权限要求，本章节主要介绍MySQL引擎的权限要求。

## 权限要求<a name="section5229125810718"></a>

-   源和目标库的连接账号需要具有登录权限，如果没有该账号，可以通过如下方式创建，以user1为例。

    参考语句：**CREATE USER**  'user1'@'host'  **IDENTIFIED BY**  'password';

-   DRS的实时迁移、实时同步、实时灾备功能的权限要求，[表1 权限要求](#table1991581978)中以user1为例提供参考语句。

    **表 1**  权限要求及参考语句

    <a name="table1991581978"></a>
    <table><thead align="left"><tr id="row19151211679"><th class="cellrowborder" valign="top" width="9.53095309530953%" id="mcps1.2.4.1.1"><p id="p39159110711"><a name="p39159110711"></a><a name="p39159110711"></a>功能模块</p>
    </th>
    <th class="cellrowborder" valign="top" width="42.06420642064206%" id="mcps1.2.4.1.2"><p id="p139151113713"><a name="p139151113713"></a><a name="p139151113713"></a>源/业务数据库</p>
    </th>
    <th class="cellrowborder" valign="top" width="48.4048404840484%" id="mcps1.2.4.1.3"><p id="p09151114713"><a name="p09151114713"></a><a name="p09151114713"></a>目标/灾备数据库</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row13915911872"><td class="cellrowborder" valign="top" width="9.53095309530953%" headers="mcps1.2.4.1.1 "><p id="p20915915718"><a name="p20915915718"></a><a name="p20915915718"></a>实时迁移</p>
    </td>
    <td class="cellrowborder" valign="top" width="42.06420642064206%" headers="mcps1.2.4.1.2 "><p id="p98881754482"><a name="p98881754482"></a><a name="p98881754482"></a><strong id="b11888145410814"><a name="b11888145410814"></a><a name="b11888145410814"></a>全量迁移权限要求：</strong></p>
    <p id="p188882542820"><a name="p188882542820"></a><a name="p188882542820"></a>SELECT、SHOW VIEW、EVENT。</p>
    <p id="p16818249189"><a name="p16818249189"></a><a name="p16818249189"></a>参考语句：<strong id="b177155954715"><a name="b177155954715"></a><a name="b177155954715"></a>GRANT</strong> SELECT, SHOW VIEW, EVENT <strong id="b1070503134815"><a name="b1070503134815"></a><a name="b1070503134815"></a>ON</strong> *.* <strong id="b143671079488"><a name="b143671079488"></a><a name="b143671079488"></a>TO</strong> 'user1';</p>
    <p id="p1988914541285"><a name="p1988914541285"></a><a name="p1988914541285"></a><strong id="b1788915541885"><a name="b1788915541885"></a><a name="b1788915541885"></a>全量+增量迁移权限要求：</strong></p>
    <p id="p1088913541989"><a name="p1088913541989"></a><a name="p1088913541989"></a>SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</p>
    <a name="ul327172591218"></a><a name="ul327172591218"></a><ul id="ul327172591218"><li>其中，REPLICATION SLAVE、REPLICATION CLIENT是全局权限，必须单独开启。参考语句如下：<p id="p2606555171212"><a name="p2606555171212"></a><a name="p2606555171212"></a><strong id="b185962019456"><a name="b185962019456"></a><a name="b185962019456"></a>GRANT</strong> REPLICATION SLAVE, REPLICATION CLIENT <strong id="b3721346455"><a name="b3721346455"></a><a name="b3721346455"></a>ON</strong> *.* <strong id="b1830814615457"><a name="b1830814615457"></a><a name="b1830814615457"></a>TO</strong> 'user1';</p>
    </li><li>SELECT、SHOW VIEW、EVENT、LOCK TABLES是非全局权限，参考语句如下：<p id="p17656615101311"><a name="p17656615101311"></a><a name="p17656615101311"></a><strong id="b13712165819443"><a name="b13712165819443"></a><a name="b13712165819443"></a>GRANT</strong> SELECT, SHOW VIEW, EVENT, LOCK TABLES <strong id="b0564952144415"><a name="b0564952144415"></a><a name="b0564952144415"></a>ON</strong> [待迁移数据库].* <strong id="b81451255184418"><a name="b81451255184418"></a><a name="b81451255184418"></a>TO</strong> 'user1';</p>
    </li></ul>
    </td>
    <td class="cellrowborder" valign="top" width="48.4048404840484%" headers="mcps1.2.4.1.3 "><p id="p228318401793"><a name="p228318401793"></a><a name="p228318401793"></a><strong id="b12833401195"><a name="b12833401195"></a><a name="b12833401195"></a>全量迁移权限要求：</strong></p>
    <p id="p22841340897"><a name="p22841340897"></a><a name="p22841340897"></a>SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、INDEX、EVENT、CREATE VIEW、CREATE ROUTINE、TRIGGER、WITH GRANT OPTION。</p>
    <p id="p17582555141815"><a name="p17582555141815"></a><a name="p17582555141815"></a>参考语句：<strong id="b255681324813"><a name="b255681324813"></a><a name="b255681324813"></a>GRANT</strong> SELECT, CREATE, ALTER, DROP, DELETE, INSERT, UPDATE, INDEX, EVENT, CREATE VIEW, CREATE ROUTINE, TRIGGER <strong id="b17992004820"><a name="b17992004820"></a><a name="b17992004820"></a>ON</strong> *.* <strong id="b149912415483"><a name="b149912415483"></a><a name="b149912415483"></a>TO</strong> 'user1' <strong id="b121861130134813"><a name="b121861130134813"></a><a name="b121861130134813"></a>WITH GRANT OPTION</strong>;</p>
    <p id="p12284240398"><a name="p12284240398"></a><a name="p12284240398"></a><strong id="b42841240798"><a name="b42841240798"></a><a name="b42841240798"></a>全量+增量迁移权限要求：</strong></p>
    <p id="p1228410401916"><a name="p1228410401916"></a><a name="p1228410401916"></a>SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、INDEX、EVENT、CREATE VIEW、CREATE ROUTINE、TRIGGER、WITH GRANT OPTION。</p>
    <p id="p6549101711911"><a name="p6549101711911"></a><a name="p6549101711911"></a>参考语句：<strong id="b119333234714"><a name="b119333234714"></a><a name="b119333234714"></a>GRANT</strong> SELECT, CREATE, ALTER, DROP, DELETE, INSERT, UPDATE, INDEX, EVENT, CREATE VIEW, CREATE ROUTINE, TRIGGER <strong id="b55043612474"><a name="b55043612474"></a><a name="b55043612474"></a>ON</strong> [待迁移数据库].* <strong id="b9206743184713"><a name="b9206743184713"></a><a name="b9206743184713"></a>TO</strong> 'user1' <strong id="b5632164919476"><a name="b5632164919476"></a><a name="b5632164919476"></a>WITH GRANT OPTION</strong>;</p>
    </td>
    </tr>
    <tr id="row29152011871"><td class="cellrowborder" valign="top" width="9.53095309530953%" headers="mcps1.2.4.1.1 "><p id="p391531878"><a name="p391531878"></a><a name="p391531878"></a>实时同步</p>
    </td>
    <td class="cellrowborder" valign="top" width="42.06420642064206%" headers="mcps1.2.4.1.2 "><p id="p12915011714"><a name="p12915011714"></a><a name="p12915011714"></a>SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT。</p>
    <a name="ul18326201910346"></a><a name="ul18326201910346"></a><ul id="ul18326201910346"><li>其中，REPLICATION SLAVE、REPLICATION CLIENT是全局权限，必须单独开启。参考语句如下：<p id="p133271419143417"><a name="p133271419143417"></a><a name="p133271419143417"></a><strong id="b13937123719446"><a name="b13937123719446"></a><a name="b13937123719446"></a>GRANT</strong> REPLICATION SLAVE, REPLICATION CLIENT <strong id="b316844019441"><a name="b316844019441"></a><a name="b316844019441"></a>ON</strong> *.* <strong id="b1540144214448"><a name="b1540144214448"></a><a name="b1540144214448"></a>TO</strong> 'user1';</p>
    </li><li>SELECT、SHOW VIEW、EVENT、LOCK TABLES是非全局权限，参考语句如下：<p id="p332711920342"><a name="p332711920342"></a><a name="p332711920342"></a><strong id="b7197833124417"><a name="b7197833124417"></a><a name="b7197833124417"></a>GRANT</strong> SELECT, SHOW VIEW, EVENT, LOCK TABLES <strong id="b71441129134419"><a name="b71441129134419"></a><a name="b71441129134419"></a>ON</strong> [待同步数据库].* <strong id="b43391625144412"><a name="b43391625144412"></a><a name="b43391625144412"></a>TO</strong> 'user1';</p>
    </li></ul>
    </td>
    <td class="cellrowborder" valign="top" width="48.4048404840484%" headers="mcps1.2.4.1.3 "><p id="p1328320580107"><a name="p1328320580107"></a><a name="p1328320580107"></a>SELECT、CREATE、DROP、DELETE、INSERT、UPDATE。</p>
    <p id="p1969421313346"><a name="p1969421313346"></a><a name="p1969421313346"></a>参考语句：<strong id="b1593345816468"><a name="b1593345816468"></a><a name="b1593345816468"></a>GRANT</strong> SELECT, CREATE, DROP, DELETE, INSERT, UPDATE <strong id="b0628132916445"><a name="b0628132916445"></a><a name="b0628132916445"></a>ON</strong> [待同步数据库].* TO 'user1';</p>
    </td>
    </tr>
    <tr id="row1915711671"><td class="cellrowborder" valign="top" width="9.53095309530953%" headers="mcps1.2.4.1.1 "><p id="p19151011576"><a name="p19151011576"></a><a name="p19151011576"></a>实时灾备</p>
    </td>
    <td class="cellrowborder" valign="top" width="42.06420642064206%" headers="mcps1.2.4.1.2 "><p id="p1991519114720"><a name="p1991519114720"></a><a name="p1991519114720"></a>SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、TRIGGER、SHOW VIEW、EVENT、INDEX、LOCK TABLES、CREATE VIEW、 CREATE ROUTINE、 ALTER ROUTINE、 CREATE USER、RELOAD、REPLICATION SLAVE、REPLICATION CLIENT、WITH GRANT OPTION。</p>
    <p id="p66173240352"><a name="p66173240352"></a><a name="p66173240352"></a>参考语句：<strong id="b3847161415446"><a name="b3847161415446"></a><a name="b3847161415446"></a>GRANT</strong> SELECT,CREATE,ALTER,DROP,DELETE,INSERT,UPDATE,TRIGGER,SHOW VIEW,EVENT,INDEX,LOCK TABLES,CREATE VIEW,CREATE ROUTINE,ALTER ROUTINE,CREATE USER,RELOAD,REPLICATION SLAVE,REPLICATION CLIENT <strong id="b13277111816444"><a name="b13277111816444"></a><a name="b13277111816444"></a>ON</strong> *.* <strong id="b1649811210443"><a name="b1649811210443"></a><a name="b1649811210443"></a>TO</strong> 'user1';</p>
    </td>
    <td class="cellrowborder" valign="top" width="48.4048404840484%" headers="mcps1.2.4.1.3 "><p id="p1915619715"><a name="p1915619715"></a><a name="p1915619715"></a>SELECT、CREATE、ALTER、DROP、DELETE、INSERT、UPDATE、TRIGGER、SHOW VIEW、EVENT、INDEX、LOCK TABLES、CREATE VIEW、 CREATE ROUTINE、 ALTER ROUTINE、 CREATE USER、RELOAD、REPLICATION SLAVE、REPLICATION CLIENT、WITH GRANT OPTION。</p>
    <p id="p1984311355350"><a name="p1984311355350"></a><a name="p1984311355350"></a>参考语句：<strong id="b8268913182517"><a name="b8268913182517"></a><a name="b8268913182517"></a>GRANT</strong> SELECT,CREATE,ALTER,DROP,DELETE,INSERT,UPDATE,TRIGGER,SHOW VIEW,EVENT,INDEX,LOCK TABLES,CREATE VIEW,CREATE ROUTINE,ALTER ROUTINE,CREATE USER,RELOAD,REPLICATION SLAVE,REPLICATION CLIENT <strong id="b10017364448"><a name="b10017364448"></a><a name="b10017364448"></a>ON</strong> *.* <strong id="b02682137252"><a name="b02682137252"></a><a name="b02682137252"></a>TO</strong> 'user1'@'%' <strong id="b4268161312258"><a name="b4268161312258"></a><a name="b4268161312258"></a>WITH GRANT OPTION</strong>;</p>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >请在以上参考语句后执行**flush privileges;**使授权生效。


-   用户迁移权限要求

    用户迁移时，当源数据库为非阿里云数据库时，帐户需要有mysql.user的SELECT权限，源数据库为阿里云数据库，则帐户需要同时具有mysql.user和mysql.user\_view的SELECT权限。

    参考语句：

    **GRANT SELECT ON**  mysql.user  **TO**  'user1'@'_host_' ;

    **GRANT SELECT ON**  mysql.user\_view  **TO**  'user1';

    目标数据库帐户需要有mysql库的SELECT，INSERT，UPDATE，DELETE, WITH GRANT OPTION权限。

    参考语句：**GRANT SELECT, INSERT, UPDATE, DELETE ON**  \*.\*  **TO**  'u1'  **WITH GRANT OPTION**;


## 授权操作说明<a name="section624418395495"></a>

-   创建用户

    操作方式：

    **CREATE USER**  '_username_'@'_host_'  **IDENTIFIED BY**  '_password_';

    ·         username：待创建的账号。

    ·         host：允许该账号登录的主机，如果允许该账号从任意主机登录数据库，可以使用%。

    ·         password：账号的密码。

    例如：授予drsmigration账号具备所有数据库和表的所有权限，并允许从任意主机登录数据库，命令如下。

    **CREATE USER**  '_drsmigration_'@'%'  **IDENTIFIED BY**  '_Drs123456_';

-   授予相应权限

    操作方式：

    **GRANT** _privileges_ **ON** _databasename.tablename_ **TO**  '_username_'@'_host_'  **WITH GRANT OPTION**;

    **flush privileges;**

    ·         privileges：授予该账号的操作权限，如SELECT、INSERT、UPDATE等，如果要授予该账号所有权限，则使用ALL

    ·         databasename：数据库名。如果要授予该账号具备所有数据库的操作权限，则使用\*。

    ·         tablename：表名。如果要授予该账号具备所有表的操作权限，则使用\*。

    ·         username：待授权的账号。

    ·         host：允许该账号登录的主机，如果允许该账号从任意主机登录，则使用%。

    ·         WITH GRANT OPTION：授予该账号使用GRANT命令的权限，该参数为可选。

    例如：创建一个账号，账号名为drsmigration，密码为Drs123456，并允许从任意主机登录数据库，命令如下。

    GRANT ALL ON \*.\* TO 'drsmigration'@'%';



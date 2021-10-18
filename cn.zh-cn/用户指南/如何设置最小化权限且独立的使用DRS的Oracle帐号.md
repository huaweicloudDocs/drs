# 如何设置最小化权限且独立的使用DRS的Oracle帐号<a name="drs_04_0023"></a>

源数据库为Oracle的全量迁移至少需要CREATE SESSION, SELECT ANY TRANSACTION, SELECT ANY TABLE, SELECT ANY DICTIONARY权限（当目标库为PostgreSQL时，还需要SELECT ANY SEQUENCE权限），源数据库为Oracle的增量迁移还需要日志解析权限。本小节主要介绍如何使用DRS设置最小化权限且独立的Oracle帐号的具体操作。

-   全量迁移模式。
    1.  创建一个用户用于迁移，此处以User1为例。

        参考命令：CREATE USER  _User1_  IDENTIFIED BY  _pwd_

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >其中User1为用户名，pwd为密码。

    2.  使用sys用户或者具有DBA权限的用户执行以下语句对User1用户赋予需要的权限。

        参考命令：GRANT CREATE SESSION, SELECT ANY TRANSACTION, SELECT ANY TABLE, SELECT ANY DICTIONARY TO  _User1_


-   全量+增量迁移模式。
    1.  创建一个用户用于迁移，此处以User1为例。

        参考命令：CREATE USER  _User1_  IDENTIFIED BY  _pwd_

    2.  使用sys用户或者具有DBA权限的用户执行以下语句对User1用户赋予需要的权限。

        参考命令：GRANT CREATE SESSION, SELECT ANY TRANSACTION, SELECT ANY TABLE, SELECT ANY DICTIONARY TO  _User1_

    3.  使用sys用户或者具有DBA权限的用户执行以下语句对User1用户赋予日志解析权限。
        -   Oracle版本小于12C。

            参考命令：GRANT EXECUTE\_CATALOG\_ROLE TO  _User1_

        -   Oracle版本大于等于12C。

            参考命令：GRANT EXECUTE\_CATALOG\_ROLE TO  _User1_

            参考命令：GRANT LOGMINING TO  _User1_





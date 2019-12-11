# MySQL迁移中Definer强制转化后如何维持原业务用户权限体系<a name="drs_16_0003"></a>

Definer的使用主要应用在视图、存储过程、触发器、事件等对象里，Definer并不会限制对象被调用的权限，但会限制对象访问数据库的权限。本场景下，用户在MySQL迁移过程中选择了“所有Definer迁移到该用户下“，则源库用户体系下其他用户账号在完成用户迁移后，如果用户迁移和权限授权都执行成功，则无需授权便可继续使用原业务（使用DRS用户迁移功能可以实现用户、权限、密码迁移），否则如果想在原来的用户权限体系下延用原业务，则需要进行授权后才具有Definer相关数据库对象的访问使用权限，从而保证原业务正常。

本章节主要介绍如何通过数据库命令行对用户账号进行授权的方法。

1.  确保新用户（Definer统一使用指定账号）具备足够的权限执行视图、存储过程等相关SQL。
2.  通过MySQL官方客户端或者其它工具登录目标数据库。
3.  通过如下命令查看需要授权的用户user当前权限详情。

    ```
    show grants for  'user'@'host';
    ```

4.  为了保证原业务不报错，使用如下命令给用户user授予涉及的数据库对象缺失的操作权限。

    ```
    grant select,insert,update,delete on db_name.* to 'user'@'host';
    ```

    一般情况下，访问数据库的权限包括：SELECT、CREATE、DROP、DELETE、INSERT、UPDATE、INDEX、EVENT、CREATE VIEW、CREATE ROUTINE、TRIGGER、EXECUTE。您需要根据具体的数据库对象查看缺少哪些权限，再进行授权操作。

    对于存储过程和函数，必须保证用户user对其有拥有EXECUTE权限，授权SQL命令如下：

    ```
    grant execute on db_name.function_name to 'user'@'host';
    ```

5.  使用授权后的用户账号访问目标库对象，无异常报错表示授权成功。需要注意：在java项目工程中调用存储过程、函数如果出现 Java.sql.SQLException: User does not have access to metadata required to determine stored procedure parameter types. If rights can not be granted, configure connection with "noAccessToProcedureBodies=true" to have driver generate parameters that represent INOUT strings irregardless of actual parametertypes，则需要单独执行用户user对mysql.proc库的授权：

    ```
    grant select on mysql.proc to 'user'@'host';
    ```



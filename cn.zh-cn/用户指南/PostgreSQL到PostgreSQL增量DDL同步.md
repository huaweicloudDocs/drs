# PostgreSQL到PostgreSQL增量DDL同步<a name="drs_03_0088"></a>

本小结介绍PostgreSQL-\>RDS for PostgreSQL实时同步，通过在源库创建触发器和函数获取源库的DDL信息，然后在DRS增量实时同步阶段实现DDL操作的同步。

## 前提条件<a name="section1519195118446"></a>

-   当前支持的DDL操作包含CREATE SCHEMA/TABLE（仅库级同步支持）、DROP TABLE 、ALTER TABLE（包含ADD COLUMN、DROP COLUMN、ALTER COLUMN、RENAME COLUMN、ADD CONSTRAINT、DROP CONSTRAINT、RENAME）。

    >![](public_sys-resources/icon-caution.gif) **注意：** 
    >RENAME表名之后，向更改名称后的表插入新的数据时，DRS不会同步新的数据到目标库。


-   源库和目标库版本不同时，请使用源库和目标库都兼容的SQL语句执行DDL操作。例如：源库为pg11，目标库为pg12，要将源库表的列类型从char修改为int时，请使用如下语句：

    ```
    alter table tablename alter column columnname type int USING columnname::int;
    ```


-   执行如下操作步骤前，请检查待同步的源数据库public模式下，是否存在名为hwdrs\_ddl\_info的表、名为hwdrs\_ddl\_function\(\)的函数、名为hwdrs\_ddl\_event的触发器。如存在，请将其删除。
-   库级同步时，如创建无主键表，请执行如下命令，将无主键表复制属性设置为full。

    ```
    alter table tablename replica identity full;
    ```


## 操作步骤<a name="section1231125915462"></a>

1.  使用拥有创建事件触发器权限的用户连接要同步的数据库。
2.  <a name="li1087504164812"></a>执行如下语句，创建存储DDL信息的表。

    ```
    CREATE TABLE public.hwdrs_ddl_info
    (
      id                             bigserial primary key,
      ddl                            text COLLATE pg_catalog."default",
      username                       varchar(64),  
      txid                           varchar(16), 
      tag                            varchar(24),  
      database                       varchar(64),  
      schema                         varchar(64), 
      client_address                 varchar(64),
      client_port                    integer,
      event_time                     timestamp
    );
    ```

3.  <a name="li78731843114813"></a>执行如下语句，创建函数。

    ```
    CREATE OR REPLACE FUNCTION public.hwdrs_ddl_function()
        RETURNS event_trigger
        LANGUAGE plpgsql
        SECURITY DEFINER
    AS $BODY$
        declare ddl text;
        declare real_num int;
        declare min_id int;
        declare max_num int := 50000;
    begin
     
      if (tg_tag = 'CREATE TABLE' or tg_tag = 'ALTER TABLE' or tg_tag = 'DROP TABLE' or tg_tag = 'CREATE SCHEMA') then
     
          select current_query() into ddl;
         
          insert into public.hwdrs_ddl_info(id, ddl, username, txid, tag, database, schema, client_address, client_port, event_time)
          values(default, ddl, current_user, cast(txid_current() as varchar(16)), tg_tag, current_database(), current_schema,  inet_client_addr(), inet_client_port(), current_timestamp);
    
          select count(id) into real_num from public.hwdrs_ddl_info;
    			
          select min(id) into min_id from public.hwdrs_ddl_info;
    
          if real_num > max_num then
            delete from public.hwdrs_ddl_info where id = min_id;
          end if;
      end if;
     
    end;
    $BODY$;
    ```

4.  执行以下语句，将步骤[2](#li1087504164812)中创建表的所有者改为DRS连接源库的用户。

    ```
    ALTER TABLE public.hwdrs_ddl_info OWNER TO username;
    ```

5.  执行以下语句，将步骤[3](#li78731843114813)中创建函数的所有者改为DRS连接源库的用户。

    ```
    ALTER FUNCTION public.hwdrs_ddl_function() OWNER TO username;
    ```

6.  执行以下语句，创建DDL事件触发器。

    ```
    CREATE EVENT TRIGGER hwdrs_ddl_event ON ddl_command_end EXECUTE PROCEDURE public.hwdrs_ddl_function();
    ```

7.  执行以下语句，将创建的事件触发器设置为enable。

    ```
    ALTER EVENT TRIGGER hwdrs_ddl_event ENABLE ALWAYS;
    ```

8.  返回数据复制服务控制台，创建PostgreSQL-\>RDS for PostgreSQL的同步任务。
9.  待同步任务结束后，请执行下语句删除创建的表、函数、触发器。

    ```
    DROP EVENT trigger hwdrs_ddl_event;
    DROP FUNCTION public.hwdrs_ddl_function();
    DROP TABLE public.hwdrs_ddl_info;
    ```



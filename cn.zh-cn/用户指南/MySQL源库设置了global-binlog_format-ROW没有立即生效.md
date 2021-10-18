# MySQL源库设置了global binlog\_format = ROW没有立即生效<a name="drs_16_0002"></a>

使用DRS进行MySQL的迁移或同步时，必须确保源库的binlog\_format是ROW格式的，否则就会导致任务失败甚至数据丢失。在源库设置了global级别的binlog\_format=ROW之后，还需要中断之前所有的业务连接，因为设置之前的连接使用的还是非ROW格式的binlog写入。

## 安全设置global级binlog\_format=ROW的步骤<a name="section6336179202711"></a>

1.  通过MySQL官方客户端或者其它工具登录源数据库。
2.  在源数据库上执行全局参数设置命令。

    ```
    set global binlog_format = ROW;
    ```

3.  在源数据库上执行如下命令确认上面操作已执行成功。

    ```
    select @@global.binlog_format;
    ```

4.  您可以通过如下两种方式确保修改后的源库binlog\_format格式立即生效。

    **方法一：**

    1.  选择一个非业务的时间段，中断当前数据库上的所有业务连接。

        1.  通过如下命令查询当前数据库上的所有业务连接\(所有的binlog Dump连接及当前连接除外\)。

            ```
            show processlist;
            ```

        2.  中断上面查出的所有业务连接。

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >在上述操作未结束之前，请不要创建或者启动迁移任务，否则会导致数据不一致。

    2.  为了避免源库binlog\_format格式因为数据库重启失效，请在源库的启动配置文件\(my.ini或my.cnf等\)中添加或修改配置参数binlog\_format并保存。

        ```
        binlog_format=ROW
        ```

    **方法二：**

    1.  为了避免源库binlog\_format格式因为数据库重启失效，请在源库的启动配置文件\(my.ini或my.cnf等\)中添加或修改配置参数binlog\_format并保存。

        ```
        binlog_format=ROW
        ```

    2.  确保上述配置参数binlog\_format添加或修改成功后，选择一个非业务时间段，重启源数据库即可。



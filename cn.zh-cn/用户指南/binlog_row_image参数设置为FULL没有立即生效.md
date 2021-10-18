# binlog\_row\_image参数设置为FULL没有立即生效<a name="drs_16_0010"></a>

使用DRS进行MySQL迁移时，必须确保源库的binlog\_row\_image参数设置为FULL，否则就会导致任务失败。在源库设置了binlog\_row\_image=FULL之后，为防止继续生成非全镜像日志导致任务失败，需选择一个非业务时间段，重启源数据库。

## 设置binlog\_row\_image为FULL步骤<a name="section187731655936"></a>

-   如果源数据库为云上RDS实例，可通过RDS管理界面的参数配置，将binlog\_row\_image修改为FULL，完成修改后重启源数据库即可。
-   如果源数据库为本地自建库，请参考如下步骤修复。
    1.  登录MySQL源数据库所在服务器。
    2.  手动修改my.cnf配置文件，将binlog\_row\_image参数值修改为FULL后保存。

        ```
        binlog_row_image=full
        ```

    3.  为防止继续生成非全镜像日志导致任务失败，需选择一个非业务时间段，重启源数据库即可



# 如何批量导出、导入事件（event）和触发器（trigger）<a name="drs_14_0006"></a>

在进行MySQL到MySQL的迁移时，若任务结束后发现迁移日志中提示迁移事件和触发器失败，可手动迁移。

本小节主要介绍批量导出导入事件和触发器的具体操作。

1.  从源库批量导出触发器。
    1.  <a name="li4714141420"></a>在源库执行以下语句，获取TRIGGER\_SCHEMA和TRIGGER\_NAME。

        ```
        SELECT TRIGGER_SCHEMA,TRIGGER_NAME  FROM INFORMATION_SCHEMA.TRIGGERS WHERE TRIGGER_SCHEMA in ('DB1','DB2','DB3') order by TRIGGER_NAME;
        ```

        上述语句中，DB1，DB2，DB3分别表示从源库待迁移到目标库的数据库。

    2.  在源库执行如下语句，从字段SQL Original Statement中获取源库创建触发器的语句。

        ```
        SHOW CREATE TRIGGER TRIGGER_SCHEMA.TRIGGER_NAME \G;
        ```

        上述语句中，TRIGGER\_SCHEMA.TRIGGER\_NAME填写的为[1.a](#li4714141420)中查询到的TRIGGER\_SCHEMA和TRIGGER\_NAME具体值。

2.  从源库批量导出事件。
    1.  <a name="li149211574819"></a>在源库执行以下语句，获取EVENT\_SCHEMA和EVENT\_NAME。

        ```
        SELECT EVENT_SCHEMA,EVENT_NAME  FROM INFORMATION_SCHEMA.EVENTS WHERE EVENT_SCHEMA in ('DB1','DB2','DB3') order by EVENT_NAME;
        ```

        上述语句中，DB1，DB2，DB3分别表示从源库待迁移到目标库的数据库。

    2.  在源库执行如下语句，从字段SQL Original Statement中获取源库创建事件的语句。

        ```
        SHOW CREATE EVENT EVENT_SCHEMA.EVENT_NAME \G;
        ```

        上述语句中，EVENT\_SCHEMA.EVENT\_NAME填写的为[2.a](#li149211574819)中查询到的EVENT\_SCHEMA和EVENT\_NAME具体值。

3.  导入触发器和事件。

    在目标库重新执行从源库导出的创建触发器和创建事件语句。



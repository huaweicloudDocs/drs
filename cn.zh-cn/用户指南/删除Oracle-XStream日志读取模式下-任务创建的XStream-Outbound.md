# 删除Oracle XStream日志读取模式下，任务创建的XStream Outbound<a name="drs_16_1135"></a>

对于Oracle-GaussDB\(for openGauss\)的实时同步，如果用户使用了XStream日志读取模式，需要在任务结束后，手动删除源库中由DRS任务创建的SXtream outbound，避免因为Oracle没有自动清理未被XStream Outbound消费过的归档日志而导致的磁盘占满问题。

## 操作步骤<a name="section153388558153"></a>

1.  <a name="li426114302332"></a>在源库执行以下sql语句，检查是否存在DRS任务创建的XStream Outbound。

    ```
    SELECT SERVER_NAME, 
           CONNECT_USER, 
           CAPTURE_USER,
           CAPTURE_NAME,
           SOURCE_DATABASE,
           QUEUE_OWNER,
           QUEUE_NAME
    FROM DBA_XSTREAM_OUTBOUND;
    ```

    DRS创建的XStream outbound的SERVER\_NAME名字命名格式为：”DRS\_”+大写任务ID，其中的大写的任务ID中的中划线会被转置为下划线，如：“DRS\_04981F62\_84A4\_4974\_A5D5\_772ED2DF63AC”。

2.  如果存在，执行以下sql语句删除XStream Outbound。其中的_<xstream SERVER\_NAME\>_为步骤[1](#li426114302332)中查询到的SERVER\_NAME。

    ```
    BEGIN DBMS_XSTREAM_ADM.DROP_OUTBOUND(server_name => '<xstream SERVER_NAME>');END; 
    ```



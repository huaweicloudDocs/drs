# GaussDB\(for openGauss\)主备版为源强制结束任务<a name="drs_03_1132"></a>

本小节介绍GaussDB\(for openGauss\)主备版为源的同步链接在强制结束任务后如何清理源库流复制槽。

## 前提条件<a name="section131903017311"></a>

由于普通用户没有执行execute direct操作的权限，删除流复制槽需要联系GaussDB\(for openGauss\)运维人员执行以下操作。

## 操作步骤<a name="section429621210368"></a>

1.  使用DRS同步任务测试连接时的用户登录GaussDB\(for openGauss\)主备版实例。
2.  <a name="li4276143622720"></a>执行如下语句，查询同步任务选择的database对象所对应的流复制槽名称。

    ```
    select slot_name from pg_replication_slots where database = 'database';
    ```

    >![](public_sys-resources/icon-notice.gif) **须知：** 
    >其中_database_为DRS同步任务中选择同步的database。

3.  执行如下语句，删除对应的流复制槽

    ```
    select * from pg_drop_replication_slot('slot_name');
    ```

    >![](public_sys-resources/icon-notice.gif) **须知：** 
    >其中_slot\_name_为步骤[2](#li4276143622720)中查询的流复制槽名称。

4.  执行如下语句，查询流复制槽是否成功删除

    ```
    select slot_name from pg_replication_slots where database = 'database';
    ```

    查询结果为空表示DRS同步任务对应的流复制槽已成功删除。



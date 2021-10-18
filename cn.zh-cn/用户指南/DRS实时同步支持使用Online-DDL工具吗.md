# DRS实时同步支持使用Online DDL工具吗<a name="drs_16_1124"></a>

DRS MySQL到MySQL的表级增量同步支持使用Online DDL工具进行加减列的操作，需注意以下几点：

-   因为DRS同步机制和工具的冲突，在同步任务的“设置同步”页面，选择对象同步范围时，不能勾选“增量DDL“项。
-   使用Online DDL工具进行加列操作时，需先在目标库执行，然后在源库执行。
-   使用Online DDL工具进行减列操作时，需先在源库执行，再在目标库执行。

常见Online DDL工具：

-   pt-online-schema-change
-   gh-ost


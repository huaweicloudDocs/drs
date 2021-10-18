# 源库参数lower\_case\_table\_names=1时，为什么不允许迁移包含大写字母的库或者表<a name="drs_14_0002"></a>

## 场景描述<a name="section13413293214"></a>

当源库参数lower\_case\_table\_names=1时，无法迁移包含大写字母的库或者表。

## 问题分析<a name="section158342053102414"></a>

当源库的lower\_case\_table\_names 参数值为1时，MySQL会将库名或者表名转换成小写再进行查找。若存在以大写字母形式创建的库或者表，那么在lower\_case\_table\_names参数值为1的情况下，MySQL将无法找到这个库或表，报告查询失败。也就是说，若lower\_case\_table\_names的参数值为1时，大写字母的库或表很可能是不可访问的。

## 解决方案<a name="section12404371141"></a>

目前针对该情况，分别提供如下解决方案：

## 方法一<a name="section368715355510"></a>

修改源库lower\_case\_table\_names的参数值为0 \(即大小写敏感\)，并且保证源库与目标库的该参数值一致。

## 方法二<a name="section11708411011"></a>

若无法永久修改lower\_case\_table\_names，可临时将源库lower\_case\_table\_names修改为0，然后执行如下操作。

-   对于表，可以使用如下语句将表名转换为小写：

    ```
    alter table `BigTab` rename to `bigtab`
    ```

-   对于库，则需要导出后，修改库名为小写，再进行导入。

>![](public_sys-resources/icon-caution.gif) **注意：** 
>修改库名或表名之后，需要维护权限的一致性，以免影响应用访问。

## 方法三<a name="section19677328181017"></a>

对象选择时不迁移该库或者该表。


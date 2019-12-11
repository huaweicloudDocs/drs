# 使用定时启动任务失败，迁移日志提示can not get agency token<a name="drs_16_0123"></a>

使用定时启动任务功能时，如果使用的是子账号，需要使用“账户委托“，否则任务启动失败，迁移日志报：can not get agency token。

## 解决方案<a name="section12404371141"></a>

目前针对该情况，分别提供如下解决方案：

-   方法一：使用主账号重新创建任务，启动方式选择“定时启动“。
-   方法二：使用主账号在子账号所在的用户组添加sercuity administrator权限后，重新创建任务，启动方式选择“定时启动“。添加权限的具体操作请参见：[创建用户并授权使用DRS](https://support.huaweicloud.com/usermanual-drs/drs_08_0012.html)。
-   方法三：重新创建任务，启动方式选择“立即启动“。


# 创建用户并授权使用DRS<a name="drs_08_0012"></a>

本章节通过简单的用户组授权方法，将DRS服务的策略授予用户组，并将用户添加至用户组中，从而使用户拥有对应的DRS权限，操作流程如[图1](#fig158351985619)所示。

## 示例流程<a name="section3327121975615"></a>

**图 1**  给用户授权DRS权限流程<a name="fig158351985619"></a>  
![](figures/给用户授权DRS权限流程.jpg "给用户授权DRS权限流程")

1.  <a name="li1658301914563"></a>[创建用户组并授权](https://support.huaweicloud.com/usermanual-iam/iam_03_0001.html)

    在IAM控制台创建用户组，并授予数据复制服务管理员权限“DRS Administrator“权限。

2.  [创建用户](https://support.huaweicloud.com/usermanual-iam/iam_02_0001.html)

    在IAM控制台创建用户，并将其加入[1](#li1658301914563)中创建的用户组。

3.  [用户登录](https://support.huaweicloud.com/usermanual-iam/iam_01_0552.html)并验证权限

    新创建的用户登录控制台，切换至授权区域，验证权限：

    -   在“服务列表”中选择数据复制服务，进入DRS主界面，单击右上角“创建迁移任务”，尝试购创建迁移任务，如果创建迁移任务（假设当前权限仅包含“DRS Administrator“），表示“DRS Administrator“已生效。
    -   在“服务列表”中选择数据复制服务（假设当前策略仅包含“DRS Administrator“）的任一服务，若提示权限不足，表示“DRS Administrator“已生效。



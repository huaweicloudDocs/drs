# 创建用户并授权使用DRS<a name="drs_08_0012"></a>

如果您需要对您所拥有的DRS进行精细的权限管理，您可以通过[企业管理](https://support.huaweicloud.com/zh-cn/usermanual-em/em-topic_02.html)或[统一身份认证服务](https://support.huaweicloud.com/usermanual-iam/iam_01_0001.html)（Identity and Access Management，简称IAM）实现。

-   通过企业管理实现的具体操作，请您参考[项目管理](https://support.huaweicloud.com/zh-cn/usermanual-em/em-topic_02.html)。
-   通过IAM实现的具体操作，您可以：
    -   根据企业的业务组织，在您的华为云帐号中，给企业中不同职能部门的员工创建IAM用户，让员工拥有唯一安全凭证，并使用DRS资源。
    -   根据企业用户的职能，设置不同的访问权限，以达到用户之间的权限隔离。
    -   将DRS资源委托给更专业、高效的其他华为云帐号或者云服务，这些帐号或者云服务可以根据权限进行代运维。


如果华为云帐号已经能满足您的要求，不需要创建独立的IAM用户，您可以跳过本章节，不影响您使用DRS服务的其它功能。

本章节为您介绍通过IAM对用户授权的方法，操作流程如[图1](#fig158351985619)所示。

## 前提条件<a name="section64352220313"></a>

给用户组授权之前，请您了解用户组可以添加的DRS权限，并结合实际需求进行选择，DRS支持的系统权限，请参见：[DRS系统权限](https://support.huaweicloud.com/productdesc-drs/drs_01_0201.html)。若您需要对除DRS之外的其它服务授权，IAM支持服务的所有权限请参见[权限策略](https://support.huaweicloud.com/usermanual-permissions/iam_01_0001.html)。

## 示例流程<a name="section3327121975615"></a>

**图 1**  给用户授权DRS权限流程<a name="fig158351985619"></a>  
![](figures/给用户授权DRS权限流程.jpg "给用户授权DRS权限流程")

1.  <a name="li1658301914563"></a>[创建用户组并授权](https://support.huaweicloud.com/usermanual-iam/iam_03_0001.html)

    在IAM控制台创建用户组，并授予数据复制服务管理员权限“DRS Administrator“权限。

2.  [创建用户](https://support.huaweicloud.com/usermanual-iam/iam_02_0001.html)

    在IAM控制台创建用户，并将其加入[1](#li1658301914563)中创建的用户组。

3.  [用户登录](https://support.huaweicloud.com/usermanual-iam/iam_01_0552.html)并验证权限

    新创建的用户登录控制台，切换至授权区域验证权限，操作如下：

    在“服务列表”中选择数据复制服务，进入DRS主界面，单击右上角“创建迁移任务”，尝试创建迁移任务，如果可以创建迁移任务（假设当前权限仅包含“DRS Administrator“），就表示“DRS Administrator“权限已生效。



# 自建OBS桶备份迁移场景<a name="drs_04_0003"></a>

用户可以将本地Microsoft SQL Server数据库备份文件上传到OBS桶，然后通过下载OBS桶里的备份文件，对已有Microsoft SQL Server实例进行备份数据迁移。

## 前提条件<a name="section129322505507"></a>

-   准备OBS桶。
-   准备Microsoft SQL Server备份文件。 约束条件如下：
    -   备份文件上传到自建OBS桶的后缀名必须为“.bak”。
    -   备份文件名称长度为：1-128个字符长度。
    -   备份文件名称组成为：字母，数字，下划线，中划线，且必须是以字母开头。
    -   备份文件大小：低于迁移的目标数据库申请空间大小的85%。
    -   备份文件必须上传至自建OBS桶的根目录下。


## 操作步骤<a name="section766512154519"></a>

1.  获取迁移目标库RDS实例ID。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >如果您已将备份文件上传至OBS，请直接从[7](#li08181716145312)开始执行。  

2.  获取OBS Browser。

    获取OBS Browser相关操作请参考[启动OBS Browser](https://support.huaweicloud.com/clientogw-obs/zh-cn_topic_0045829056.html)。

3.  创建访问密钥（AK 和 SK）。

    创建访问密钥先关操作请参考[创建访问密钥](https://support.huaweicloud.com/clientogw-obs/zh-cn_topic_0045829057.html)。

4.  登录OBS Browser客户端。

    登录OBS Browser客户端相关操作请参考[登录客户端](https://support.huaweicloud.com/clientogw-obs/zh-cn_topic_0045829058.html)。

5.  通过OBS Browser创建OBS桶。

    创建OBS桶相关操作请参考[创建桶](https://support.huaweicloud.com/clientogw-obs/zh-cn_topic_0045829125.html)。

6.  通过OBS Browser将已准备好的备份文件上传至OBS桶。

    上传备份文件至OBS桶相关操作请参考[上传文件或文件夹](https://support.huaweicloud.com/clientogw-obs/zh-cn_topic_0045828972.html)。

7.  <a name="li08181716145312"></a>构造备份迁移任务接口请求体。

    构造备份迁移任务接口请求体相关操作请参考[创建备份迁移任务](创建备份迁移任务.md)。

8.  查询任务详情或任务列表接口，观察任务状态。
    -   查询任务详情相关操作请参考[获取备份迁移任务详情](获取备份迁移任务详情.md)。
    -   查询任务列表相关操作请参考[获取备份迁移任务列表](获取备份迁移任务列表.md)。

9.  调用删除任务接口，删除迁移任务。

    删除迁移任务相关操作请参考[删除备份迁移任务](删除备份迁移任务.md)。

10. 登录OBS Browser, 删除备份文件和OBS桶。
    -   删除备份文件相关操作请参考[删除文件或文件夹](https://support.huaweicloud.com/clientogw-obs/zh-cn_topic_0086375570.html)。
    -   删除OBS桶相关操作请参考[删除桶](https://support.huaweicloud.com/clientogw-obs/zh-cn_topic_0045828968.html)。



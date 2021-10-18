# 分片集群MongoDB迁移前清除孤儿文档<a name="drs_09_0101"></a>

## 什么是孤儿文档<a name="section9909238203913"></a>

MongoDB负载均衡器（Balancer）会根据集合的分片键\(Shard key\)均衡数据。Balancer的工作原理是：需要Balancer的数据块（Chunk）先复制到目标Shard，成功后再删除原Shard上的Chunk，来完成一次Chunk迁移，通过多次Chunk迁移来实现均衡。在Chunk迁移时，如果发生网络闪断等不可预知的场景，完成了复制但没有完成删除，那么对同一条文档会同时存在于两个Shard上。因为Chunk迁移在MongoDB上是感知的，config会更新这条文档应该在哪个Shard上，那么另一个Shard上的文档会存在但不会被感知，后续的update、delete操作都不会作用于这个错误的Shard上的文档，那么这条文档被称为孤儿文档（Orphaned Document）。

## 迁移影响<a name="section1411683158"></a>

DRS在迁移集群时，会从Shard上抽取全量数据。正常文档和孤儿文档在不同的Shard上，DRS不会感知，都会迁移到目标库。DRS针对MongoDB迁移的冲突策略为忽略，因此最终目标库上的文档取决于哪个文档先被迁过去，会造成数据内容或行数不一致。

## 操作步骤<a name="section13123163021517"></a>

1.  下载用于清除孤儿文档的[cleanupOrphaned.js](https://res-static.hc-cdn.cn/cloudbu-site/china/zh-cn/zhuchenlu/cleanupOrphaned.js)脚本文件。
2.  <a name="li9814142002918"></a>修改cleanupOrphaned.js脚本文件，将test替换为待清理孤儿文档的数据库名。
3.  <a name="li2467154265618"></a>执行以下命令，清理Shard节点下指定的数据库中所有集合的孤儿文档。

    ```
    mongo --host ShardIP --port Primaryport --authenticationDatabase database -u username -p passowrd cleanupOrphaned.js
    ```

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   ShardIP：Shard节点的IP地址。
    >-   Primaryport：Shard节点中的Primary节点的服务端口。
    >-   database：鉴权数据库名，即数据库账号所属的数据库。
    >-   username：登录数据库的账号。
    >-   passowrd：登录数据库的密码。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >如果您有多个数据库，您需要重复执行步骤[2](#li9814142002918)和步骤[3](#li2467154265618)，分别为每个数据库的每个Shard节点清理孤立文档。



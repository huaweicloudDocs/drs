# 如何设置MongoDB数据库分片集群的分片键<a name="drs_14_0003"></a>

MongoDB数据库中数据的分片是以集合为基本单位的，集合中的数据通过片键被分成多部分。

对集合进行分片时，您需要选择一个片键 , 片键是每条记录都必须包含的，且建立了索引的单个字段或复合字段，MongoDB数据库按照片键将数据划分到不同的数据块中，并将数据块均衡地分布到所有分片中。为了按照片键划分数据块，MongoDB数据库使用基于范围的分片方式或者基于哈希的分片方式。

**表 1**  分片键分类

<a name="table9673142268"></a>
<table><thead align="left"><tr id="row2067316415261"><th class="cellrowborder" valign="top" width="17.46%" id="mcps1.2.4.1.1"><p id="p1067315410261"><a name="p1067315410261"></a><a name="p1067315410261"></a><strong id="b6532735112619"><a name="b6532735112619"></a><a name="b6532735112619"></a>分片键类型</strong></p>
</th>
<th class="cellrowborder" valign="top" width="49.2%" id="mcps1.2.4.1.2"><p id="p16732462617"><a name="p16732462617"></a><a name="p16732462617"></a><strong id="b356311358262"><a name="b356311358262"></a><a name="b356311358262"></a>描述</strong></p>
</th>
<th class="cellrowborder" valign="top" width="33.339999999999996%" id="mcps1.2.4.1.3"><p id="p1067311462619"><a name="p1067311462619"></a><a name="p1067311462619"></a><strong id="b15637355267"><a name="b15637355267"></a><a name="b15637355267"></a>使用场景</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row166731946261"><td class="cellrowborder" valign="top" width="17.46%" headers="mcps1.2.4.1.1 "><p id="p267334112611"><a name="p267334112611"></a><a name="p267334112611"></a>基于范围的分片键</p>
</td>
<td class="cellrowborder" valign="top" width="49.2%" headers="mcps1.2.4.1.2 "><p id="p16731141262"><a name="p16731141262"></a><a name="p16731141262"></a>基于范围的分片键是根据分片键值把数据分成一个个邻接的范围，如果没有指定特定的分片类型，则基于范围的分片键是默认的分片类型。</p>
<p id="p7700658132614"><a name="p7700658132614"></a><a name="p7700658132614"></a>特点：基于范围的分片键对于范围类型的查询比较高效，给定一个片键的范围，分发路由可以很简单地确定哪个数据块存储了请求需要的数据，并将请求转发到相应的分片中。</p>
</td>
<td class="cellrowborder" valign="top" width="33.339999999999996%" headers="mcps1.2.4.1.3 "><p id="p1867314413265"><a name="p1867314413265"></a><a name="p1867314413265"></a>建议在分片键基数较大，频率较低，并且分片键值不是单调变化的情况下使用基于范围的分片键。</p>
</td>
</tr>
<tr id="row196737482617"><td class="cellrowborder" valign="top" width="17.46%" headers="mcps1.2.4.1.1 "><p id="p13673346260"><a name="p13673346260"></a><a name="p13673346260"></a>基于哈希的分片键</p>
</td>
<td class="cellrowborder" valign="top" width="49.2%" headers="mcps1.2.4.1.2 "><p id="p156734416261"><a name="p156734416261"></a><a name="p156734416261"></a>基于哈希的分片键是指MongoDB数据库计算一个字段的哈希值，并用这个哈希值来创建数据块。</p>
<p id="p11623414183910"><a name="p11623414183910"></a><a name="p11623414183910"></a>特点：保证了集群中数据的均衡。哈希值的随机性使数据随机分布在每个数据块中，因此也随机分布在不同分片中。</p>
</td>
<td class="cellrowborder" valign="top" width="33.339999999999996%" headers="mcps1.2.4.1.3 "><p id="p17673104132612"><a name="p17673104132612"></a><a name="p17673104132612"></a>如果分片键值的基数较大，拥有大量不一样的值，或者分片键值是单调变化的，则建议使用基于哈希的分片键。</p>
</td>
</tr>
</tbody>
</table>

集合设置分片并插入文档之后，其中的每个文档的分片的键和值都是不可更改的。如果需要修改文档的分片键，必须要先删除文档，再修改分片键，然后重新插入文档。

>![](public_sys-resources/icon-note.gif) **说明：**   
>分片键不支持数组索引，文本索引和地理空间索引。  

## 基于范围的分片键设置<a name="section138609266341"></a>

1.  使用如下命令，开启数据库分片开关。

    **sh.enableSharding**_\(database\)_

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >参数database表示要开启分片集合的数据库。  

2.  设置分片键。

    **sh.shardCollection**_\(namespace, key\)_

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   参数namespace表示需要进行分片的目标集合的完整命名空间<database\>.<collections\>。  
    >-   key表示要设置分片键的索引。  

    -   如果需要进行分片的目标集合是空集合，可以不创建索引直接进行下一步的分片设置，该操作会自动创建索引。

        **sh.shardCollection\(\)**

    -   如果需要进行分片的目标集合是非空集合，则需要先创建索引key。然后使用如下命令设置分片键。

        **sh.shardCollection\(\)**



## 基于哈希的分片键设置<a name="section010117324550"></a>

1.  使用如下命令，开启数据库分片开关。

    **sh.enableSharding**_\(database\)_

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >参数database表示要开启分片集合的数据库。  

2.  设置基于哈希的分片键。

    **sh.shardCollection**\(_"<database\>.<collection\>", \{ <shard key\> : "hashed" \} _, false, \{numInitialChunks: 预置的chunk个数\}\)

    其中numInitialChunks值的估算方法是：db.collection.stats\(\).size / 10\*1024\*1024\*1024 。

    如果集合已经包含数据，则需要先使用如下命令对需要创建的基于哈希的分片键先创建哈希索引：

    **db.collection.createIndex\(\)**

    然后再使用如下命令创建基于哈希的分片键：

    **sh.shardCollection\(\)**



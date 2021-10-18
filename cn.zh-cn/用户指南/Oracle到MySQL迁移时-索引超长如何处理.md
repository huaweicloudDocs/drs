# Oracle到MySQL迁移时，索引超长如何处理<a name="drs_04_0022"></a>

## 索引长度说明<a name="section131623398475"></a>

MySQL引擎对索引长度有一些限制，最主要的因素就是存储引擎和字符集。不同的字符集，单个字符包含的最大字节数有所不同。例如UTF8字符集，一个字符最多包含3个字节。而UTF8MB4一个字符最多包含 4 个字节。

-   如果是单字段索引，则字段长度不应超过[表1](#table149825104820)中的“单字段最大字符数“。例如，MySQL 5.7.6版本的InnoDB引擎，单字段索引不应超过767个字节（字符数=767/最大字节数）。
-   如果是联合索引，则每个字段长度均不能超过[表1](#table149825104820)中的“单字段索引最大字符数“，且所有字段长度合计不应超过“联合索引合计最大字符数“。例如，MySQL 5.7.6版本的InnoDB引擎，每个字段索引不应超过767个字节（字符数=767/最大字节数），且所有字段索引长度总和不超过3072个字节（字符数=3072/最大字节数）。

**表 1**  索引长度说明

<a name="table149825104820"></a>
<table><thead align="left"><tr id="row74902564816"><th class="cellrowborder" valign="top" width="13.167366526694662%" id="mcps1.2.7.1.1"><p id="p174992516484"><a name="p174992516484"></a><a name="p174992516484"></a>引擎</p>
</th>
<th class="cellrowborder" valign="top" width="12.847430513897221%" id="mcps1.2.7.1.2"><p id="p250825154820"><a name="p250825154820"></a><a name="p250825154820"></a>MySQL版本</p>
</th>
<th class="cellrowborder" valign="top" width="18.49630073985203%" id="mcps1.2.7.1.3"><p id="p450182513489"><a name="p450182513489"></a><a name="p450182513489"></a>字符集</p>
</th>
<th class="cellrowborder" valign="top" width="18.58628274345131%" id="mcps1.2.7.1.4"><p id="p1250142520482"><a name="p1250142520482"></a><a name="p1250142520482"></a>最大字节数</p>
</th>
<th class="cellrowborder" valign="top" width="18.406318736252754%" id="mcps1.2.7.1.5"><p id="p2501825164818"><a name="p2501825164818"></a><a name="p2501825164818"></a>单字段索引最大字符数</p>
</th>
<th class="cellrowborder" valign="top" width="18.49630073985203%" id="mcps1.2.7.1.6"><p id="p250102504818"><a name="p250102504818"></a><a name="p250102504818"></a>联合索引合计最大字符数</p>
</th>
</tr>
</thead>
<tbody><tr id="row7511252480"><td class="cellrowborder" rowspan="2" valign="top" width="13.167366526694662%" headers="mcps1.2.7.1.1 "><p id="p15062544819"><a name="p15062544819"></a><a name="p15062544819"></a>InnoDB</p>
<p id="p165011254489"><a name="p165011254489"></a><a name="p165011254489"></a></p>
<p id="p17504251488"><a name="p17504251488"></a><a name="p17504251488"></a></p>
<p id="p1050152516486"><a name="p1050152516486"></a><a name="p1050152516486"></a></p>
</td>
<td class="cellrowborder" valign="top" width="12.847430513897221%" headers="mcps1.2.7.1.2 "><p id="p1250142519489"><a name="p1250142519489"></a><a name="p1250142519489"></a>MySQL 5.7.6及以下版本</p>
</td>
<td class="cellrowborder" valign="top" width="18.49630073985203%" headers="mcps1.2.7.1.3 "><p id="p55116253485"><a name="p55116253485"></a><a name="p55116253485"></a>UTF8MB4</p>
</td>
<td class="cellrowborder" valign="top" width="18.58628274345131%" headers="mcps1.2.7.1.4 "><p id="p25152564811"><a name="p25152564811"></a><a name="p25152564811"></a>4</p>
</td>
<td class="cellrowborder" valign="top" width="18.406318736252754%" headers="mcps1.2.7.1.5 "><p id="p15162514485"><a name="p15162514485"></a><a name="p15162514485"></a>191</p>
</td>
<td class="cellrowborder" valign="top" width="18.49630073985203%" headers="mcps1.2.7.1.6 "><p id="p15511525184811"><a name="p15511525184811"></a><a name="p15511525184811"></a>768</p>
</td>
</tr>
<tr id="row19522255486"><td class="cellrowborder" valign="top" headers="mcps1.2.7.1.1 "><p id="p195142511482"><a name="p195142511482"></a><a name="p195142511482"></a>MySQL 5.7.7及以上版本</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.7.1.2 "><p id="p145215255483"><a name="p145215255483"></a><a name="p145215255483"></a>UTF8MB4</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.7.1.3 "><p id="p7521925154810"><a name="p7521925154810"></a><a name="p7521925154810"></a>4</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.7.1.4 "><p id="p7521025124815"><a name="p7521025124815"></a><a name="p7521025124815"></a>768</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.7.1.5 "><p id="p252132534817"><a name="p252132534817"></a><a name="p252132534817"></a>768</p>
</td>
</tr>
</tbody>
</table>

## 索引超长的处理方法<a name="section316165824716"></a>

-   方法一

    不迁移含有超长索引的表。


-   方法二

    修改源库索引长度满足以上索引长度说明中的要求，改操作可能导致迁移后数据不完整，请谨慎使用。以目标库为MySQL 5.7.6及以下版本的UTF8MB4为例，可通过如下方式修改长度。

    ```
    alter table tablename modify columnname varchar2 (768) ;
    ```


其中，tablename请用实际表名代替，columnname请用实际列名代替。

-   方法三

    在源库删除该索引及其约束。以目标库为MySQL 5.7.6及以下版本的UTF8MB4为例，可通过如下方式删除索引及其约束。

    ```
    drop index indexname;
    alter table tablename drop constraint constraintname;
    ```

    其中，indexname请用实际索引名代替，tablename请用实际表名代替，constraintname请用实际约束名代替。



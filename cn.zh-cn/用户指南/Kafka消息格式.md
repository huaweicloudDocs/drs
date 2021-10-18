# Kafka消息格式<a name="drs_03_0052"></a>

同步到Kafka集群中的数据以avro、JSON和JSON-C格式存储。

## avro格式<a name="section33313217425"></a>

avro格式的schema定义详情请参见[record.rar](https://res-static.hc-cdn.cn/cloudbu-site/china/zh-cn/zhuchenlu/record.rar)。在实时同步到Kafka集群后，您需要根据schema定义进行数据解析，数据解析样例请参见[drs-avro-read.rar](https://res-static.hc-cdn.cn/cloudbu-site/china/zh-cn/zhuchenlu/drs-avro-read.rar)。

## JSON格式<a name="section737619567426"></a>

JSON格式定义详情参考[表1](#table71321778434)：

**表 1**  JSON参数说明

<a name="table71321778434"></a>
<table><thead align="left"><tr id="row10132137144320"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.3.1.1"><p id="p4132137134313"><a name="p4132137134313"></a><a name="p4132137134313"></a><strong id="b171321570439"><a name="b171321570439"></a><a name="b171321570439"></a>参数名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="80%" id="mcps1.2.3.1.2"><p id="p513215719436"><a name="p513215719436"></a><a name="p513215719436"></a><strong id="b17132773438"><a name="b17132773438"></a><a name="b17132773438"></a>说明</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row1913277164310"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p41322712430"><a name="p41322712430"></a><a name="p41322712430"></a>mysqlType</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p313287144310"><a name="p313287144310"></a><a name="p313287144310"></a>源端表字段名称和类型。</p>
</td>
</tr>
<tr id="row1513216719436"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p31327764318"><a name="p31327764318"></a><a name="p31327764318"></a>id</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p613277204315"><a name="p613277204315"></a><a name="p613277204315"></a>DRS内部定义的事件操作的序列号，单调递增。</p>
</td>
</tr>
<tr id="row1313247154319"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p91322713433"><a name="p91322713433"></a><a name="p91322713433"></a>es</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p141323714437"><a name="p141323714437"></a><a name="p141323714437"></a>源库产生这一条记录的时间，13位Unix时间戳，单位为毫秒。</p>
</td>
</tr>
<tr id="row1413219714312"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p5132207184315"><a name="p5132207184315"></a><a name="p5132207184315"></a>ts</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p201329704310"><a name="p201329704310"></a><a name="p201329704310"></a>写入到目标kafka的时间，13位Unix时间戳，单位为毫秒。</p>
</td>
</tr>
<tr id="row1513227114316"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p12132574435"><a name="p12132574435"></a><a name="p12132574435"></a>database</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p21321871439"><a name="p21321871439"></a><a name="p21321871439"></a>数据库名称（Oracle数据库填写schema）。</p>
</td>
</tr>
<tr id="row2132117114319"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p181321674431"><a name="p181321674431"></a><a name="p181321674431"></a>table</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p91325774319"><a name="p91325774319"></a><a name="p91325774319"></a>表名。</p>
</td>
</tr>
<tr id="row6132167204312"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p61330794317"><a name="p61330794317"></a><a name="p61330794317"></a>type</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p1133571439"><a name="p1133571439"></a><a name="p1133571439"></a>操作类型，比如DELETE，UPDATE，INSERT，DDL。</p>
</td>
</tr>
<tr id="row1613314711437"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p1813317734320"><a name="p1813317734320"></a><a name="p1813317734320"></a>isDdl</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p1713318784314"><a name="p1713318784314"></a><a name="p1713318784314"></a>是否是DDL操作。</p>
</td>
</tr>
<tr id="row18133107134313"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p613310794319"><a name="p613310794319"></a><a name="p613310794319"></a>sql</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p11336754315"><a name="p11336754315"></a><a name="p11336754315"></a>DDL的SQL语句，在DML操作中，取值为""。</p>
</td>
</tr>
<tr id="row0133276439"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p613313724314"><a name="p613313724314"></a><a name="p613313724314"></a>sqlType</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p7133197124310"><a name="p7133197124310"></a><a name="p7133197124310"></a>源端表字段的jdbc类型。</p>
</td>
</tr>
<tr id="row81330710432"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p161331174434"><a name="p161331174434"></a><a name="p161331174434"></a>data</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p1313311724319"><a name="p1313311724319"></a><a name="p1313311724319"></a>最新的数据，为JSON数组，如果type参数是插入则表示最新插入的数据，如果是更新，则表示更新后的最新数据。</p>
</td>
</tr>
<tr id="row121334714439"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p7133479437"><a name="p7133479437"></a><a name="p7133479437"></a>old</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p2133187184313"><a name="p2133187184313"></a><a name="p2133187184313"></a>旧数据，如果type参数是更新，则表示更新前的数据；如果是删除，则表示被删除的数据；如果是插入，取值为null。</p>
</td>
</tr>
<tr id="row17133872434"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p8133774432"><a name="p8133774432"></a><a name="p8133774432"></a>pkNames</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p17133672438"><a name="p17133672438"></a><a name="p17133672438"></a>主键名称。</p>
</td>
</tr>
</tbody>
</table>

```
{
    "mysqlType":{
        "c11":"binary",
        "c10":"varchar",
        "c13":"text",
        "c12":"varbinary",
        "c14":"blob",
        "c1":"varchar",
        "c2":"varbinary",
        "c3":"int",
        "c4":"datetime",
        "c5":"timestamp",
        "c6":"char",
        "c7":"float",
        "c8":"double",
        "c9":"decimal",
        "id":"int"
    },
    "id":27677,
    "es":1624614713000,
    "ts":1625058726990,
    "database":"test01",
    "table":"test ",
    "type":"UPDATE",
    "isDdl":false,
    "sql":"",
    "sqlType":{
        "c11":-2,
        "c10":12,
        "c13":-1,
        "c12":-3,
        "c14":2004,
        "c1":12,
        "c2":-3,
        "c3":4,
        "c4":94,
        "c5":93,
        "c6":1,
        "c7":6,
        "c8":8,
        "c9":3,
        "id":4
    },
    "data":[
        {
            "c11":"[]",
            "c10":"华为云huaweicloud",
            "c13":"asfiajhfiaf939-0239uoituqorjoqirfoidjfqrniowejoiwqjroqwjrowqjojoiqgoiegnkjgoi23roiugouofdug9u90weurtg103",
            "c12":"[106, 103, 111, 106, 103, 111, 105, 100, 115, 106, 103, 111, 106, 111, 115, 111, 103, 57, 51, 52, 48, 57, 52, 51, 48, 57, 116, 106, 104, 114, 103, 106, 101, 119, 57, 116, 117, 48, 57, 51, 52, 48, 116, 101, 114, 111, 101, 106, 103, 57, 56, 51, 48, 52, 105, 101, 117, 114, 103, 57, 101, 119, 117, 114, 103, 48, 119, 101, 117, 116, 57, 114, 48, 52, 117, 48, 57, 53, 116, 117, 51, 48, 57, 50, 117, 116, 48, 57, 51, 117, 116, 48, 119, 57, 101]",
            "c14":"[106, 103, 111, 106, 103, 111, 105, 100, 115, 106, 103, 111, 106, 111, 115, 111, 103, 57, 51, 52, 48, 57, 52, 51, 48, 57, 116, 106, 104, 114, 103, 106, 101, 119, 57, 116, 117, 48, 57, 51, 52, 48, 116, 101, 114, 111, 101, 106, 103, 57, 56, 51, 48, 52, 105, 55, 57, 56, 52, 54, 53, 52, 54, 54, 54, 49, 52, 54, 53, 33, 64, 35, 36, 37, 94, 42, 40, 41, 95, 41, 43, 95, 43, 124, 125, 34, 63, 62, 58, 58, 101, 117, 114, 103, 57, 101, 119, 117, 114, 103, 48, 119, 101, 117, 116, 57, 114, 48, 52, 117, 48, 57, 53, 116, 117, 51, 48, 57, 50, 117, 116, 48, 57, 51, 117, 116, 48, 119, 57, 101]",
            "c1":"cf3f70a7-7565-44b0-ae3c-83bec549ea8e:104",
            "c2":"[]",
            "c3":"103",
            "c4":"2021-06-25 17:51:53",
            "c5":"1624614713.201",
            "c6":"!@#$%90weurtg103",
            "c7":"10357.0",
            "c8":"1.2510357E7",
            "c9":"9874510357",
            "id":"104"
        }
    ],
    "old":[
        {
            "c11":"[]",
            "c10":"华为云huaweicloud",
            "c13":"asfiajhfiaf939-0239",
            "c12":"[106, 103, 111, 106, 103, 111, 105, 100, 115, 106, 103, 111, 106, 111, 115, 111, 103, 57, 51, 52, 48, 57, 52, 51, 48, 57, 116, 106, 104, 114, 103, 106, 101, 119, 57, 116, 117, 48, 57, 51, 52, 48, 116, 101, 114, 111, 101, 106, 103, 57, 56, 51, 48, 52, 105, 101, 117, 114, 103, 57, 101, 119, 117, 114, 103, 48, 119, 101, 117, 116, 57, 114, 48, 52, 117, 48, 57, 53, 116, 117, 51, 48, 57, 50, 117, 116, 48, 57, 51, 117, 116, 48, 119, 57, 101]",
            "c14":"[106, 103, 111, 106, 103, 111, 105, 100, 115, 106, 103, 111, 106, 111, 115, 111, 103, 57, 51, 52, 48, 57, 52, 51, 48, 57, 116, 106, 104, 114, 103, 106, 101, 119, 57, 116, 117, 48, 57, 51, 52, 48, 116, 101, 114, 111, 101, 106, 103, 57, 56, 51, 48, 52, 105, 55, 57, 56, 52, 54, 53, 52, 54, 54, 54, 49, 52, 54, 53, 33, 64, 35, 36, 37, 94, 42, 40, 41, 95, 41, 43, 95, 43, 124, 125, 34, 63, 62, 58, 58, 101, 117, 114, 103, 57, 101, 119, 117, 114, 103, 48, 119, 101, 117, 116, 57, 114, 48, 52, 117, 48, 57, 53, 116, 117, 51, 48, 57, 50, 117, 116, 48, 57, 51, 117, 116, 48, 119, 57, 101]",
            "c1":"cf3f70a7-7565-44b0-ae3c-83bec549ea8e:104",
            "c2":"[]",
            "c3":"103",
            "c4":"2021-06-25 17:51:53",
            "c5":"1624614713.201",
            "c6":"!@#$%90weurtg103",
            "c7":"10357.0",
            "c8":"1.2510357E7",
            "c9":"9874510357",
            "id":"103"
        }
    ],
    "pkNames":[
        "id"
    ]
}
```

## JSON-C格式<a name="section175558549264"></a>

JSON-C格式与JSON格式类似，区别是对于删除操作，JSON数据放在old上，JSON-C放在data上。对于timestamp类型数据转换成yyyy-mm-dd hh:mm:ss的字符串。

JSON-C定义详情参考[表2](#table111344482275)：

**表 2**  JSON-C参数说明

<a name="table111344482275"></a>
<table><thead align="left"><tr id="row313414485278"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.3.1.1"><p id="p21341048122718"><a name="p21341048122718"></a><a name="p21341048122718"></a><strong id="b1913434812271"><a name="b1913434812271"></a><a name="b1913434812271"></a>参数名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="80%" id="mcps1.2.3.1.2"><p id="p81351348172711"><a name="p81351348172711"></a><a name="p81351348172711"></a><strong id="b131350480276"><a name="b131350480276"></a><a name="b131350480276"></a>说明</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row15135134817271"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p4135174892717"><a name="p4135174892717"></a><a name="p4135174892717"></a>mysqlType</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p2135194832710"><a name="p2135194832710"></a><a name="p2135194832710"></a>源端表字段名称和类型。</p>
</td>
</tr>
<tr id="row41355489273"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p413516482275"><a name="p413516482275"></a><a name="p413516482275"></a>id</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p5135548132713"><a name="p5135548132713"></a><a name="p5135548132713"></a>DRS内部定义的事件操作的序列号，单调递增。</p>
</td>
</tr>
<tr id="row18135124852716"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p1013512487273"><a name="p1013512487273"></a><a name="p1013512487273"></a>es</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p141351848122711"><a name="p141351848122711"></a><a name="p141351848122711"></a>源库产生这一条记录的时间，13位Unix时间戳，单位为毫秒。</p>
</td>
</tr>
<tr id="row15135204812712"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p713594810271"><a name="p713594810271"></a><a name="p713594810271"></a>ts</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p18135204813274"><a name="p18135204813274"></a><a name="p18135204813274"></a>写入到目标kafka的时间，13位Unix时间戳，单位为毫秒。</p>
</td>
</tr>
<tr id="row1713554852719"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p171352483271"><a name="p171352483271"></a><a name="p171352483271"></a>database</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p2135204817276"><a name="p2135204817276"></a><a name="p2135204817276"></a>数据库名称（Oracle数据库填写schema）。</p>
</td>
</tr>
<tr id="row111357485279"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p21359489274"><a name="p21359489274"></a><a name="p21359489274"></a>table</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p10136648192718"><a name="p10136648192718"></a><a name="p10136648192718"></a>表名。</p>
</td>
</tr>
<tr id="row13136948112714"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p6136154822710"><a name="p6136154822710"></a><a name="p6136154822710"></a>type</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p2013694810272"><a name="p2013694810272"></a><a name="p2013694810272"></a>操作类型，比如DELETE，UPDATE，INSERT，DDL。</p>
</td>
</tr>
<tr id="row131362480270"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p111361048132719"><a name="p111361048132719"></a><a name="p111361048132719"></a>isDdl</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p313613489274"><a name="p313613489274"></a><a name="p313613489274"></a>是否是DDL操作。</p>
</td>
</tr>
<tr id="row8136174892719"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p71361448182715"><a name="p71361448182715"></a><a name="p71361448182715"></a>sql</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p1813615481272"><a name="p1813615481272"></a><a name="p1813615481272"></a>DDL的SQL语句，在DML操作中，取值为""。</p>
</td>
</tr>
<tr id="row3136144882712"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p181361048132712"><a name="p181361048132712"></a><a name="p181361048132712"></a>sqlType</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p12137348192712"><a name="p12137348192712"></a><a name="p12137348192712"></a>源端表字段的jdbc类型。</p>
</td>
</tr>
<tr id="row12137204862711"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p17137948102714"><a name="p17137948102714"></a><a name="p17137948102714"></a>data</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p113794882713"><a name="p113794882713"></a><a name="p113794882713"></a>最新的数据，为JSON数组，如果type参数是插入则表示最新插入的数据，如果是更新，则表示更新后的最新数据；如果是删除，则表示被删除的数据。</p>
</td>
</tr>
<tr id="row1213764822716"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p7137144842710"><a name="p7137144842710"></a><a name="p7137144842710"></a>old</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p1813764811271"><a name="p1813764811271"></a><a name="p1813764811271"></a>旧数据，如果type参数是更新，则表示更新前的数据；如果是插入，取值为null。</p>
</td>
</tr>
<tr id="row1513704815270"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p3137048172713"><a name="p3137048172713"></a><a name="p3137048172713"></a>pkNames</p>
</td>
<td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p1413716484277"><a name="p1413716484277"></a><a name="p1413716484277"></a>主键名称。</p>
</td>
</tr>
</tbody>
</table>

## JSON格式数据中常见的转义字符<a name="section1646420326440"></a>

**表 3**  转义字符

<a name="table181661514457"></a>
<table><thead align="left"><tr id="row11671212459"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p151673164513"><a name="p151673164513"></a><a name="p151673164513"></a><strong id="b7268143161113"><a name="b7268143161113"></a><a name="b7268143161113"></a>字符</strong></p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p616711124513"><a name="p616711124513"></a><a name="p616711124513"></a><strong id="b10274194312116"><a name="b10274194312116"></a><a name="b10274194312116"></a>转义字符</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row2167181154517"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p8177153116115"><a name="p8177153116115"></a><a name="p8177153116115"></a>&lt;</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p21771231181110"><a name="p21771231181110"></a><a name="p21771231181110"></a>\u003d</p>
</td>
</tr>
<tr id="row91671118452"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p12177133111116"><a name="p12177133111116"></a><a name="p12177133111116"></a>&gt;</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p0177103161118"><a name="p0177103161118"></a><a name="p0177103161118"></a>\u003e</p>
</td>
</tr>
<tr id="row616718164511"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p2177831151110"><a name="p2177831151110"></a><a name="p2177831151110"></a>&amp;</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p117711311118"><a name="p117711311118"></a><a name="p117711311118"></a>\u0026</p>
</td>
</tr>
<tr id="row61676144513"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p8177103118116"><a name="p8177103118116"></a><a name="p8177103118116"></a>=</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p817793120116"><a name="p817793120116"></a><a name="p817793120116"></a>\u003d</p>
</td>
</tr>
<tr id="row10167416459"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p1177103121115"><a name="p1177103121115"></a><a name="p1177103121115"></a>'</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p317753111112"><a name="p317753111112"></a><a name="p317753111112"></a>\u0027</p>
</td>
</tr>
</tbody>
</table>


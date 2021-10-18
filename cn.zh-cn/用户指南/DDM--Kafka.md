# DDM-\>Kafka<a name="drs_04_0448"></a>

## 操作要求<a name="section1691943218231"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table88114333143"></a>
<table><thead align="left"><tr id="row581153310145"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p6811173316140"><a name="p6811173316140"></a><a name="p6811173316140"></a><strong id="b481283316141"><a name="b481283316141"></a><a name="b481283316141"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p13812533121416"><a name="p13812533121416"></a><a name="p13812533121416"></a><strong id="b13812163313148"><a name="b13812163313148"></a><a name="b13812163313148"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row15813533111413"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p10813183318143"><a name="p10813183318143"></a><a name="p10813183318143"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul98136337142"></a><a name="ul98136337142"></a><ul id="ul98136337142"><li><a href="#table13451741151419">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>源数据库中存在主键重复的数据时, 直接同步将导致目标库数据比源库少, 请务必检查并订正数据后启动同步。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li><li>数据类型不兼容时，可能引起同步失败。</li></ul>
</td>
</tr>
<tr id="row4813933151416"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p9813163318143"><a name="p9813163318143"></a><a name="p9813163318143"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1581343351414"></a><a name="ul1581343351414"></a><ul id="ul1581343351414"><li>增量同步支持DDL操作。</li><li>增量同步过程中，不允许修改、删除连接源和目标数据库的用户的用户名、密码、权限，或修改源和目标数据库的端口号。</li><li>创建任务后，不支持增加逻辑库或修改旧逻辑库关联新的RDS，否则会导致同步任务失败。</li><li>该链路不支持SSL安全连接。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section86695405239"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table13451741151419"></a>
<table><thead align="left"><tr id="row1546144115146"><th class="cellrowborder" valign="top" width="18.35%" id="mcps1.2.3.1.1"><p id="p1146841151414"><a name="p1146841151414"></a><a name="p1146841151414"></a><strong id="b184614131416"><a name="b184614131416"></a><a name="b184614131416"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.65%" id="mcps1.2.3.1.2"><p id="p174612411146"><a name="p174612411146"></a><a name="p174612411146"></a><strong id="b1646134181410"><a name="b1646134181410"></a><a name="b1646134181410"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row8461641171413"><td class="cellrowborder" valign="top" width="18.35%" headers="mcps1.2.3.1.1 "><p id="p20465419144"><a name="p20465419144"></a><a name="p20465419144"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.65%" headers="mcps1.2.3.1.2 "><a name="ul1946741191416"></a><a name="ul1946741191416"></a><ul id="ul1946741191416"><li>源物理分片数据库帐户需要具备如下权限：SELECT。</li></ul>
</td>
</tr>
<tr id="row154614181415"><td class="cellrowborder" valign="top" width="18.35%" headers="mcps1.2.3.1.1 "><p id="p1946341101411"><a name="p1946341101411"></a><a name="p1946341101411"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.65%" headers="mcps1.2.3.1.2 "><a name="ul246941191416"></a><a name="ul246941191416"></a><ul id="ul246941191416"><li>支持表数据的同步。</li></ul>
</td>
</tr>
<tr id="row1347114112141"><td class="cellrowborder" valign="top" width="18.35%" headers="mcps1.2.3.1.1 "><p id="p11471641191416"><a name="p11471641191416"></a><a name="p11471641191416"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.65%" headers="mcps1.2.3.1.2 "><a name="ul747184141414"></a><a name="ul747184141414"></a><ul id="ul747184141414"><li>源物理分片数据库的binlog日志必须打开，且binlog日志格式必须为Row格式，数据库GTID状态建议为开启，binlog_row_image必须为FULL。</li><li>在磁盘空间允许的情况下，binlog保存时间越长越好，建议为3天。</li><li>必须设置源数据库的server_id。server_id的取值范围在1－4294967296之间。</li><li>源分库分表中间件中的库名、表名不能包含：'&lt;&gt;/\以及非ASCII字符。</li><li>源物理分片数据库建议开启skip-name-resolve，减少连接超时的可能性。</li><li>源物理分片数据库不支持枚举类型和set集合类型的<span id="text14481541181412"><a name="text14481541181412"></a><a name="text14481541181412"></a>实时同步</span>。</li><li>源数据库表名、字段名不能超过30个字符。</li></ul>
</td>
</tr>
<tr id="row7481741131418"><td class="cellrowborder" valign="top" width="18.35%" headers="mcps1.2.3.1.1 "><p id="p7486415147"><a name="p7486415147"></a><a name="p7486415147"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.65%" headers="mcps1.2.3.1.2 "><a name="ul29831994476"></a><a name="ul29831994476"></a><ul id="ul29831994476"><li>消费时 isolation.level 参数为read_committed。</li></ul>
</td>
</tr>
</tbody>
</table>


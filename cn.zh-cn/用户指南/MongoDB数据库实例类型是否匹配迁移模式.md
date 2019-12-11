# MongoDB数据库实例类型是否匹配迁移模式<a name="drs_11_0066"></a>

## MongoDB数据库迁移场景<a name="section1215815382368"></a>

**表 1**  MongoDB数据库实例类型是否匹配迁移模式

<a name="table1828717534330"></a>
<table><tbody><tr id="row928715319335"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p1028711530339"><a name="p1028711530339"></a><a name="p1028711530339"></a><strong id="b19287753193317"><a name="b19287753193317"></a><a name="b19287753193317"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p1728711536333"><a name="p1728711536333"></a><a name="p1728711536333"></a>MongoDB数据库实例类型是否匹配迁移模式。</p>
</td>
</tr>
<tr id="row1428712532337"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p172871353193310"><a name="p172871353193310"></a><a name="p172871353193310"></a><strong id="b1228755315331"><a name="b1228755315331"></a><a name="b1228755315331"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p3287165313334"><a name="p3287165313334"></a><a name="p3287165313334"></a>检查MongoDB数据库实例类型是否匹配迁移模式，若不匹配，则会导致迁移失败。</p>
</td>
</tr>
<tr id="row132879539336"><th class="firstcol" rowspan="2" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p828715530336"><a name="p828715530336"></a><a name="p828715530336"></a><strong id="b1728745333319"><a name="b1728745333319"></a><a name="b1728745333319"></a>失败提示及处理建议</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p1614134064919"><a name="p1614134064919"></a><a name="p1614134064919"></a><strong id="b281345617493"><a name="b281345617493"></a><a name="b281345617493"></a>失败原因</strong>：增量迁移只支持副本集作为源数据库。</p>
<p id="p1021923974918"><a name="p1021923974918"></a><a name="p1021923974918"></a><strong id="b20239175318246"><a name="b20239175318246"></a><a name="b20239175318246"></a>处理建议</strong>：请使用副本集作为源数据库进行增量迁移。</p>
</td>
</tr>
<tr id="row5769193964016"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p14770939154019"><a name="p14770939154019"></a><a name="p14770939154019"></a><strong id="b979844514404"><a name="b979844514404"></a><a name="b979844514404"></a>告警原因</strong>：迁移模式是增量迁移，但是目标库实例类型未知。</p>
<p id="p125581951164017"><a name="p125581951164017"></a><a name="p125581951164017"></a><strong id="b1231455812403"><a name="b1231455812403"></a><a name="b1231455812403"></a>处理建议</strong>：请确认目标库实例类型是副本集或者是分片集群。</p>
</td>
</tr>
</tbody>
</table>


# 源数据库索引（\_id）检查<a name="drs_11_0114"></a>

## MongoDB迁移场景<a name="section834844911539"></a>

**表 1**  源数据库索引（\_id）检查

<a name="table1286312219628"></a>
<table><tbody><tr id="row1333815319628"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p16418526191940"><a name="p16418526191940"></a><a name="p16418526191940"></a><strong id="b13549013191940"><a name="b13549013191940"></a><a name="b13549013191940"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p59157410191053"><a name="p59157410191053"></a><a name="p59157410191053"></a>源数据库索引（_id）检查。</p>
</td>
</tr>
<tr id="row59198819628"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p12227812191940"><a name="p12227812191940"></a><a name="p12227812191940"></a><strong id="b42941445191940"><a name="b42941445191940"></a><a name="b42941445191940"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p2174934014558"><a name="p2174934014558"></a><a name="p2174934014558"></a>检查源库是否存在没有索引（_id）的集合，若存在，则导致迁移失败。</p>
</td>
</tr>
<tr id="row5971331319628"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p31582987191940"><a name="p31582987191940"></a><a name="p31582987191940"></a><strong id="b15811431191940"><a name="b15811431191940"></a><a name="b15811431191940"></a>告警提示及<strong id="b117671048113514"><a name="b117671048113514"></a><a name="b117671048113514"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p1922623283013"><a name="p1922623283013"></a><a name="p1922623283013"></a><strong id="b839165483018"><a name="b839165483018"></a><a name="b839165483018"></a>失败原因：</strong>源数据库存在没有索引（_id）的集合。</p>
<p id="p7398373485"><a name="p7398373485"></a><a name="p7398373485"></a><strong id="b17206281884"><a name="b17206281884"></a><a name="b17206281884"></a>处理建议</strong>：针对源数据库没有索引（_id）的集合手动添加索引，参考命令：db.集合名.ensureIndex({_id: 1})，如果创建索引失败提示有重复的索引（_id）值，则不支持该集合的迁移。</p>
</td>
</tr>
</tbody>
</table>


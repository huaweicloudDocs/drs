# 源库是否包含无日志表\(UNLOGGED TABLE\)<a name="drs_11_0112"></a>

## PostgreSQL-\>PostgreSQL同步场景<a name="section14404223174716"></a>

**表 1**  源库是否包含无日志表\(UNLOGGED TABLE\)

<a name="table1286312219628"></a>
<table><tbody><tr id="row1333815319628"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p16418526191940"><a name="p16418526191940"></a><a name="p16418526191940"></a><strong id="b13549013191940"><a name="b13549013191940"></a><a name="b13549013191940"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p59157410191053"><a name="p59157410191053"></a><a name="p59157410191053"></a>源库是否包含无日志表(UNLOGGED TABLE)。</p>
</td>
</tr>
<tr id="row59198819628"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p12227812191940"><a name="p12227812191940"></a><a name="p12227812191940"></a><strong id="b42941445191940"><a name="b42941445191940"></a><a name="b42941445191940"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p2174934014558"><a name="p2174934014558"></a><a name="p2174934014558"></a>检查源库是否包含无日志表(UNLOGGED TABLE)，若存在无日志表，则导致同步失败。</p>
</td>
</tr>
<tr id="row5971331319628"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p31582987191940"><a name="p31582987191940"></a><a name="p31582987191940"></a><strong id="b15811431191940"><a name="b15811431191940"></a><a name="b15811431191940"></a>告警提示及<strong id="b117671048113514"><a name="b117671048113514"></a><a name="b117671048113514"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p7398373485"><a name="p7398373485"></a><a name="p7398373485"></a><strong id="b2039037134818"><a name="b2039037134818"></a><a name="b2039037134818"></a>告警原因</strong>：源数据库包含无日志表(UNLOGGED TABLE)，对无日志表的修改不会记录日志, 因此进入增量同步后，UNLOGGED类型的表将无法同步增量数据。</p>
<p id="p97203281380"><a name="p97203281380"></a><a name="p97203281380"></a><strong id="b17206281884"><a name="b17206281884"></a><a name="b17206281884"></a>处理建议</strong>：请确认这些无日志表是否需要同步增量数据，如果需要，请将这些表的UNLOGGED属性去掉，参考命令：ALTER TABLE TABLE_NAME SET LOGGED。</p>
</td>
</tr>
</tbody>
</table>


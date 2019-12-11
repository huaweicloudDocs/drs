# SERVER\_UUID的一致性检查<a name="drs_11_0025"></a>

## MySQL迁移场景<a name="section951717570246"></a>

**表 1**  SERVER\_UUID的一致性检查

<a name="table9224429145915"></a>
<table><tbody><tr id="row1725662975918"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p2025612295590"><a name="p2025612295590"></a><a name="p2025612295590"></a><strong id="b1256182915912"><a name="b1256182915912"></a><a name="b1256182915912"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p627012919591"><a name="p627012919591"></a><a name="p627012919591"></a>SERVER_UUID的一致性检查。</p>
</td>
</tr>
<tr id="row9270132995914"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p8287182917591"><a name="p8287182917591"></a><a name="p8287182917591"></a><strong id="b0287172915910"><a name="b0287172915910"></a><a name="b0287172915910"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p2287102965911"><a name="p2287102965911"></a><a name="p2287102965911"></a>源数据库和目标数据库的系统参数SERVER_UUID相同，将导致增量迁移失败。</p>
</td>
</tr>
<tr id="row8287142915915"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p6303132925913"><a name="p6303132925913"></a><a name="p6303132925913"></a><strong id="b103035294594"><a name="b103035294594"></a><a name="b103035294594"></a>失败提示及<strong id="b14490151682817"><a name="b14490151682817"></a><a name="b14490151682817"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p1830392914594"><a name="p1830392914594"></a><a name="p1830392914594"></a><strong id="b3733349123219"><a name="b3733349123219"></a><a name="b3733349123219"></a>失败原因</strong>：源数据库和目标数据库的参数SERVER_UUID相同, 将导致增量迁移失败。。</p>
<p id="p11226153214386"><a name="p11226153214386"></a><a name="p11226153214386"></a><strong id="b14548638193514"><a name="b14548638193514"></a><a name="b14548638193514"></a>处理建议</strong>：检查源数据库与目标数据库是否设置为同一个MySQL数据库。</p>
</td>
</tr>
</tbody>
</table>


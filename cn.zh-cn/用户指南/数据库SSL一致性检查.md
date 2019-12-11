# 数据库SSL一致性检查<a name="drs_11_0108"></a>

## MongoDB数据库迁移场景<a name="section2142104644718"></a>

**表 1**  数据库SSL一致性检查

<a name="table853017177447"></a>
<table><tbody><tr id="row1854591710447"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p1356101713440"><a name="p1356101713440"></a><a name="p1356101713440"></a><strong id="b16561131710445"><a name="b16561131710445"></a><a name="b16561131710445"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p13561917164412"><a name="p13561917164412"></a><a name="p13561917164412"></a>数据库SSL一致性检查。</p>
</td>
</tr>
<tr id="row2057614176447"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p18576517134410"><a name="p18576517134410"></a><a name="p18576517134410"></a><strong id="b2057611172444"><a name="b2057611172444"></a><a name="b2057611172444"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p196081717204410"><a name="p196081717204410"></a><a name="p196081717204410"></a>检查源数据库和目标数据库的SSL是否一致，源数据库和目标数据库不能同时开启SSL安全连接，否则，会导致迁移失败。</p>
</td>
</tr>
<tr id="row56083173444"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p06081617174412"><a name="p06081617174412"></a><a name="p06081617174412"></a><strong id="b1660821713443"><a name="b1660821713443"></a><a name="b1660821713443"></a>失败提示及<strong id="b117671048113514"><a name="b117671048113514"></a><a name="b117671048113514"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p14903715131210"><a name="p14903715131210"></a><a name="p14903715131210"></a><strong id="b16903171519126"><a name="b16903171519126"></a><a name="b16903171519126"></a>失败原因</strong>：源数据库和目标数据库同时使用了SSL连接。</p>
<p id="p2084215421831"><a name="p2084215421831"></a><a name="p2084215421831"></a><strong id="b1642212111403"><a name="b1642212111403"></a><a name="b1642212111403"></a>处理建议</strong>：若为入云场景，源数据库使用了SSL连接，则目标数据库须关闭SSL连接；若为出云场景，目标数据库使用了SSL连接，则源数据库须关闭SSL连接。</p>
</td>
</tr>
</tbody>
</table>


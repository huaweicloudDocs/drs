# 目标数据库SSL证书类型检查<a name="drs_11_0107"></a>

## MySQL迁移场景<a name="section191963424478"></a>

**表 1**  目标数据库SSL证书类型检查

<a name="table853017177447"></a>
<table><tbody><tr id="row1854591710447"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p1356101713440"><a name="p1356101713440"></a><a name="p1356101713440"></a><strong id="b16561131710445"><a name="b16561131710445"></a><a name="b16561131710445"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p13561917164412"><a name="p13561917164412"></a><a name="p13561917164412"></a>目标数据库SSL证书类型检查。</p>
</td>
</tr>
<tr id="row2057614176447"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p18576517134410"><a name="p18576517134410"></a><a name="p18576517134410"></a><strong id="b2057611172444"><a name="b2057611172444"></a><a name="b2057611172444"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p196081717204410"><a name="p196081717204410"></a><a name="p196081717204410"></a>检查云内数据库迁移出云时，目标数据库的SSL证书类型是否正确，如不符合要求，会导致迁移失败。</p>
</td>
</tr>
<tr id="row56083173444"><th class="firstcol" rowspan="2" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p06081617174412"><a name="p06081617174412"></a><a name="p06081617174412"></a><strong id="b1660821713443"><a name="b1660821713443"></a><a name="b1660821713443"></a>失败提示及<strong id="b117671048113514"><a name="b117671048113514"></a><a name="b117671048113514"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p14903715131210"><a name="p14903715131210"></a><a name="p14903715131210"></a><strong id="b16903171519126"><a name="b16903171519126"></a><a name="b16903171519126"></a>失败原因</strong>：目标数据库SSL证书不存在。</p>
<p id="p2084215421831"><a name="p2084215421831"></a><a name="p2084215421831"></a><strong id="b1642212111403"><a name="b1642212111403"></a><a name="b1642212111403"></a>处理建议</strong>：请在“源库及目标库”页面，目标库信息处开启SSL安全连接并上传内容只包含一段以“BEGIN CERTIFICATE”开始和“END CERTIFICATE”结束的SSL加密证书。</p>
</td>
</tr>
<tr id="row1928241133619"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p127189289361"><a name="p127189289361"></a><a name="p127189289361"></a><strong id="b1471862815366"><a name="b1471862815366"></a><a name="b1471862815366"></a>失败原因</strong>：不支持目标数据库SSL证书类型。</p>
<p id="p16360617113611"><a name="p16360617113611"></a><a name="p16360617113611"></a><strong id="b15360131763610"><a name="b15360131763610"></a><a name="b15360131763610"></a>处理建议</strong>：请在“源库及目标库”页面，目标库信息处开启SSL安全连接并上传内容只包含一段以“BEGIN CERTIFICATE”开始和“END CERTIFICATE”结束的SSL加密证书。</p>
</td>
</tr>
</tbody>
</table>


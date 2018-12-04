# 源数据库的SSL状态检查<a name="drs_11_0042"></a>

## 源数据库为PostgreSQL数据库<a name="section191963424478"></a>

**表 1**  源数据库的SSL状态检查

<a name="table853017177447"></a>
<table><tbody><tr id="row1854591710447"><th class="firstcol" valign="top" width="8.540000000000001%" id="mcps1.2.3.1.1"><p id="p1356101713440"><a name="p1356101713440"></a><a name="p1356101713440"></a><strong id="b16561131710445"><a name="b16561131710445"></a><a name="b16561131710445"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.46%" headers="mcps1.2.3.1.1 "><p id="p13561917164412"><a name="p13561917164412"></a><a name="p13561917164412"></a><span class="keyword" id="keyword6190152234519"><a name="keyword6190152234519"></a><a name="keyword6190152234519"></a>源数据库的SSL状态</span>检查。</p>
</td>
</tr>
<tr id="row2057614176447"><th class="firstcol" valign="top" width="8.540000000000001%" id="mcps1.2.3.2.1"><p id="p18576517134410"><a name="p18576517134410"></a><a name="p18576517134410"></a><strong id="b2057611172444"><a name="b2057611172444"></a><a name="b2057611172444"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.46%" headers="mcps1.2.3.2.1 "><p id="p196081717204410"><a name="p196081717204410"></a><a name="p196081717204410"></a>检查源数据库的SSL是否开启。</p>
</td>
</tr>
<tr id="row56083173444"><th class="firstcol" valign="top" width="8.540000000000001%" id="mcps1.2.3.3.1"><p id="p06081617174412"><a name="p06081617174412"></a><a name="p06081617174412"></a><strong id="b1660821713443"><a name="b1660821713443"></a><a name="b1660821713443"></a>失败提示及处理建议</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.46%" headers="mcps1.2.3.3.1 "><p id="p062301714444"><a name="p062301714444"></a><a name="p062301714444"></a><strong id="b1990511401232"><a name="b1990511401232"></a><a name="b1990511401232"></a>失败原因</strong>：源数据库的SSL连接关闭了。</p>
<p id="p2084215421831"><a name="p2084215421831"></a><a name="p2084215421831"></a><strong id="b1642212111403"><a name="b1642212111403"></a><a name="b1642212111403"></a>处理建议</strong>：建议打开源数据库的SSL连接，指定配置文件中受信任的根证书地址ssl_ca_file，修改postgresql.conf中的ssl参数为on，重启数据库生效。</p>
</td>
</tr>
</tbody>
</table>


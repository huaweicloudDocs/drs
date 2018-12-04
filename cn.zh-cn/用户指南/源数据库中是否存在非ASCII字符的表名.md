# 源数据库中是否存在非ASCII字符的表名<a name="drs_11_0021"></a>

## 源数据库为MySQL数据库<a name="section7657449172117"></a>

**表 1**  源数据库中是否存在非ASCII字符的表名

<a name="table17789454195019"></a>
<table><tbody><tr id="row14789554115018"><th class="firstcol" valign="top" width="8.459999999999999%" id="mcps1.2.3.1.1"><p id="p580565495010"><a name="p580565495010"></a><a name="p580565495010"></a><strong id="b1380575416506"><a name="b1380575416506"></a><a name="b1380575416506"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.53999999999999%" headers="mcps1.2.3.1.1 "><p id="p83811335135120"><a name="p83811335135120"></a><a name="p83811335135120"></a>源数据库中是否存在非ASCII字符的表名。</p>
</td>
</tr>
<tr id="row3805155418509"><th class="firstcol" valign="top" width="8.459999999999999%" id="mcps1.2.3.2.1"><p id="p10820654125010"><a name="p10820654125010"></a><a name="p10820654125010"></a><strong id="b782045415011"><a name="b782045415011"></a><a name="b782045415011"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.53999999999999%" headers="mcps1.2.3.2.1 "><p id="p38201054185012"><a name="p38201054185012"></a><a name="p38201054185012"></a>源数据库中存在非ASCII字符的表名，导致迁移失败。</p>
</td>
</tr>
<tr id="row108201754185014"><th class="firstcol" valign="top" width="8.459999999999999%" id="mcps1.2.3.3.1"><p id="p1883655420502"><a name="p1883655420502"></a><a name="p1883655420502"></a><strong id="b783655435016"><a name="b783655435016"></a><a name="b783655435016"></a>失败提示及处理建议</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.53999999999999%" headers="mcps1.2.3.3.1 "><p id="p1283615415501"><a name="p1283615415501"></a><a name="p1283615415501"></a><strong id="b3733349123219"><a name="b3733349123219"></a><a name="b3733349123219"></a>失败原因</strong>：源数据库中存在非ASCII字符的表名。</p>
<p id="p361285017345"><a name="p361285017345"></a><a name="p361285017345"></a><strong id="b131151059193412"><a name="b131151059193412"></a><a name="b131151059193412"></a>处理建议</strong>：修改源数据库中存在的非ASCII字符的表名。</p>
</td>
</tr>
</tbody>
</table>


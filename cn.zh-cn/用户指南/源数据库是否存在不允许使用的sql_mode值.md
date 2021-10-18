# 源数据库是否存在不允许使用的sql\_mode值<a name="drs_11_0049"></a>

## MySQL迁移场景<a name="section139872157212"></a>

**表 1**  源数据库是否存在不允许使用的sql\_mode值

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>源数据库是否存在不允许使用的sql_mode值。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>检查源数据库是否存在不允许使用的sql_mode值，若存在，可能会导致迁移失败。</p>
</td>
</tr>
<tr id="row1412765616510"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>不通过提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p29251110763"><a name="p29251110763"></a><a name="p29251110763"></a><strong id="b692511101368"><a name="b692511101368"></a><a name="b692511101368"></a>不通过原因</strong>：源数据库参数SQL_MODE包含不允许的sql_mode值：no_engine_substitution。</p>
<p id="p69257101863"><a name="p69257101863"></a><a name="p69257101863"></a><strong id="b5278546253"><a name="b5278546253"></a><a name="b5278546253"></a>处理建议</strong>：修改源数据库的参数值。</p>
</td>
</tr>
</tbody>
</table>


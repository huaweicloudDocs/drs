# 源库和目标库参数log\_bin\_trust\_function\_creators一致性校验<a name="drs_11_0227"></a>

## MySQL迁移场景<a name="section1238917511343"></a>

**表 1**  源库和目标库参数log\_bin\_trust\_function\_creators一致性校验

<a name="table1027815019274"></a>
<table><tbody><tr id="row162799012715"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p92793032716"><a name="p92793032716"></a><a name="p92793032716"></a><strong id="b427910052715"><a name="b427910052715"></a><a name="b427910052715"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p7279003272"><a name="p7279003272"></a><a name="p7279003272"></a>源库和目标库参数log_bin_trust_function_creators一致性校验。</p>
</td>
</tr>
<tr id="row1627919072710"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p9279100192710"><a name="p9279100192710"></a><a name="p9279100192710"></a><strong id="b1927950162716"><a name="b1927950162716"></a><a name="b1927950162716"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p19279203274"><a name="p19279203274"></a><a name="p19279203274"></a>在进行MySQL到MySQL的出云迁移时，源库和目标库参数log_bin_trust_function_creators需保持一致。当源数据库支持自定义函数时，而目标数据库不支持自定义函数，此时源数据库自定义函数的参数log_bin_trust_function_creators=on，目标数据库自定义函数的参数log_bin_trust_function_creators=off，需修改目标库的log_bin_trust_function_creators=on。若二者不一致，可能会导致迁移失败。</p>
</td>
</tr>
<tr id="row162791072715"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1927940142715"><a name="p1927940142715"></a><a name="p1927940142715"></a><strong id="b1628050192711"><a name="b1628050192711"></a><a name="b1628050192711"></a>待确认提示及<strong id="b72805016275"><a name="b72805016275"></a><a name="b72805016275"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p128060162710"><a name="p128060162710"></a><a name="p128060162710"></a><strong id="b1328017017279"><a name="b1328017017279"></a><a name="b1328017017279"></a>待确认原因</strong>：目标数据库不支持自定义函数。</p>
<p id="p228018015279"><a name="p228018015279"></a><a name="p228018015279"></a><strong id="b1128060152712"><a name="b1128060152712"></a><a name="b1128060152712"></a>处理建议</strong>：请检查目标库my.cnf文件中是否存在参数log_bin_trust_function_creators=on，若不存在则在my.cnf中加上该参数， 并重启目标数据库使之生效。</p>
</td>
</tr>
</tbody>
</table>


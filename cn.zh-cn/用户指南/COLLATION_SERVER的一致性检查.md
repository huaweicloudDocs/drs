# COLLATION\_SERVER的一致性检查<a name="drs_11_0024"></a>

## MySQL数据库<a name="section9856141292417"></a>

**表 1**  COLLATION\_SERVER的一致性检查

<a name="table8590456125712"></a>
<table><tbody><tr id="row196050566578"><th class="firstcol" valign="top" width="8.540000000000001%" id="mcps1.2.3.1.1"><p id="p1660575625716"><a name="p1660575625716"></a><a name="p1660575625716"></a><strong id="b36214561575"><a name="b36214561575"></a><a name="b36214561575"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.46%" headers="mcps1.2.3.1.1 "><p id="p1962105685720"><a name="p1962105685720"></a><a name="p1962105685720"></a>COLLATION_SERVER的一致性检查。</p>
</td>
</tr>
<tr id="row1962113565572"><th class="firstcol" valign="top" width="8.540000000000001%" id="mcps1.2.3.2.1"><p id="p263795618571"><a name="p263795618571"></a><a name="p263795618571"></a><strong id="b15637165617576"><a name="b15637165617576"></a><a name="b15637165617576"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.46%" headers="mcps1.2.3.2.1 "><p id="p1163725618573"><a name="p1163725618573"></a><a name="p1163725618573"></a>源数据库和目标数据库的参数COLLATION_SERVER不一致，导致迁移失败。</p>
</td>
</tr>
<tr id="row1863712566570"><th class="firstcol" valign="top" width="8.540000000000001%" id="mcps1.2.3.3.1"><p id="p3653156175718"><a name="p3653156175718"></a><a name="p3653156175718"></a><strong id="b146531756185711"><a name="b146531756185711"></a><a name="b146531756185711"></a>失败提示及处理建议</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.46%" headers="mcps1.2.3.3.1 "><p id="p126682056125710"><a name="p126682056125710"></a><a name="p126682056125710"></a><strong id="b3733349123219"><a name="b3733349123219"></a><a name="b3733349123219"></a>失败原因</strong>：源数据库和目标数据库的参数COLLATION_SERVER不一致。</p>
<p id="p11737124603715"><a name="p11737124603715"></a><a name="p11737124603715"></a><strong id="b920462613356"><a name="b920462613356"></a><a name="b920462613356"></a>处理建议</strong>：修改源数据库或目标数据库的参数COLLATION_SERVER。</p>
</td>
</tr>
</tbody>
</table>


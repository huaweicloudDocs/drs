# 源库和目标库的参数Time\_Zone或System\_Time\_Zone不一致<a name="drs_11_0023"></a>

## MySQL迁移场景<a name="section129755213237"></a>

**表 1**  TIME\_ZONE的一致性检查

<a name="table42025216558"></a>
<table><tbody><tr id="row35255255516"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p8521452165515"><a name="p8521452165515"></a><a name="p8521452165515"></a><strong id="b1367155285519"><a name="b1367155285519"></a><a name="b1367155285519"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p1341171725620"><a name="p1341171725620"></a><a name="p1341171725620"></a>TIME_ZONE的一致性检查。</p>
</td>
</tr>
<tr id="row567105212553"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p184352155517"><a name="p184352155517"></a><a name="p184352155517"></a><strong id="b484145215557"><a name="b484145215557"></a><a name="b484145215557"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p11524183955615"><a name="p11524183955615"></a><a name="p11524183955615"></a>源数据库和目标数据库的参数TIME_ZONE不一致，导致迁移失败。</p>
</td>
</tr>
<tr id="row398195218554"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p798452185510"><a name="p798452185510"></a><a name="p798452185510"></a><strong id="b1998155216556"><a name="b1998155216556"></a><a name="b1998155216556"></a>失败提示及<strong id="b14490151682817"><a name="b14490151682817"></a><a name="b14490151682817"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p798115218552"><a name="p798115218552"></a><a name="p798115218552"></a><strong id="b3733349123219"><a name="b3733349123219"></a><a name="b3733349123219"></a>失败原因</strong>：源数据库和目标数据库的参数TIME_ZONE或SYSTEM_TIME_ZONE不一致。</p>
<p id="p11403747153617"><a name="p11403747153617"></a><a name="p11403747153617"></a><strong id="b15395121810356"><a name="b15395121810356"></a><a name="b15395121810356"></a>处理建议</strong>：将目标数据库的TIME_ZONE修改为和源数据库的TIME_ZONE一致，或者将源数据库的TIME_ZONE修改为和目标数据库的TIME_ZONE一致。</p>
</td>
</tr>
</tbody>
</table>


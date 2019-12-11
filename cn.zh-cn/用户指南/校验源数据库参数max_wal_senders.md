# 校验源数据库参数max\_wal\_senders<a name="drs_11_0053"></a>

## PostgreSQL迁移场景<a name="section19232412143112"></a>

**表 1**  校验源数据库参数max\_wal\_senders

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>校验源数据库参数max_wal_senders。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>源数据库max_wal_senders参数值必须大于0，否则，可能会导致迁移失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" rowspan="3" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>失败提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p4375933165516"><a name="p4375933165516"></a><a name="p4375933165516"></a><strong id="b81659016572"><a name="b81659016572"></a><a name="b81659016572"></a>失败原因</strong>：源数据库参数<span class="parmname" id="parmname12721175915335"><a name="parmname12721175915335"></a><a name="parmname12721175915335"></a>“max_wal_senders”</span>必须大于0。</p>
<p id="p11593173210554"><a name="p11593173210554"></a><a name="p11593173210554"></a><strong id="b25021232367"><a name="b25021232367"></a><a name="b25021232367"></a>处理建议</strong>：建议修改配置文件postgresql.conf中的<span class="parmname" id="parmname75491120123313"><a name="parmname75491120123313"></a><a name="parmname75491120123313"></a>“max_wal_senders”</span>参数，重启数据库生效。</p>
</td>
</tr>
<tr id="row12931536144811"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p79614275530"><a name="p79614275530"></a><a name="p79614275530"></a><strong id="b3838321145715"><a name="b3838321145715"></a><a name="b3838321145715"></a>失败原因</strong>：用户基本权限不足。</p>
<p id="p17341101345410"><a name="p17341101345410"></a><a name="p17341101345410"></a><strong id="b0502934367"><a name="b0502934367"></a><a name="b0502934367"></a>处理建议</strong>：查看对应的数据库帐号权限是否符合迁移要求。</p>
</td>
</tr>
<tr id="row1524317419487"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p117543371522"><a name="p117543371522"></a><a name="p117543371522"></a><strong id="b1227672515714"><a name="b1227672515714"></a><a name="b1227672515714"></a>失败原因</strong>：内部错误。</p>
<p id="p1490342055417"><a name="p1490342055417"></a><a name="p1490342055417"></a><strong id="b55807361765"><a name="b55807361765"></a><a name="b55807361765"></a>处理建议</strong>：请联系客服人员处理。</p>
</td>
</tr>
</tbody>
</table>


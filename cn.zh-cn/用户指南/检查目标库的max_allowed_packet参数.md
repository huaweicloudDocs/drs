# 检查目标库的max\_allowed\_packet参数<a name="drs_15_0017"></a>

## MySQL数据库<a name="section1238917511343"></a>

**表 1**  检查目标库的max\_allowed\_packet参数

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p4802184614916"><a name="p4802184614916"></a><a name="p4802184614916"></a>检查目标库的max_allowed_packet参数。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p43145422920"><a name="p43145422920"></a><a name="p43145422920"></a>目标库的max_allowed_packet参数值小于100MB，导致目标库无法写入造成全量迁移失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>不通过提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p12833144912248"><a name="p12833144912248"></a><a name="p12833144912248"></a><strong id="b383384952415"><a name="b383384952415"></a><a name="b383384952415"></a>告警信息</strong>：目标库的max_allowed_packet参数值过小导致目标库数据无法写入造成全量迁移失败。</p>
<p id="p1392595254319"><a name="p1392595254319"></a><a name="p1392595254319"></a><strong id="b109251352134317"><a name="b109251352134317"></a><a name="b109251352134317"></a>处理建议</strong>：修改目标库max_allowed_packet参数值，使其大于100MB。</p>
</td>
</tr>
</tbody>
</table>


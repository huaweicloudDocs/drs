# 目标库最大支持chunk数目检查<a name="drs_11_0202"></a>

## MongoDB数据库迁移场景<a name="section14885958191920"></a>

**表 1**  目标库最大支持chunk数目检查

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>目标库最大支持chunk数目检查。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>检查目标数据库的最大chunk数目是否足以支撑源库数据的分片分裂，当chunk个数达到目标库的最大支撑数目时，chunk不再分裂，会影响写入性能。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>不通过提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p195635219105"><a name="p195635219105"></a><a name="p195635219105"></a><strong id="b15638219102"><a name="b15638219102"></a><a name="b15638219102"></a>待确认原因</strong>：目标库的最大chunk数目不足以支撑源库数据的分片分裂，当chunk个数达到目标库的最大支撑数目时，chunk不再分裂，会影响写入性能。</p>
<p id="p143538103549"><a name="p143538103549"></a><a name="p143538103549"></a><strong id="b03535104549"><a name="b03535104549"></a><a name="b03535104549"></a>处理建议</strong>：选择更高规格的目标库实例。</p>
</td>
</tr>
</tbody>
</table>


# 目标数据库参数max\_worker\_processes是否足够<a name="drs_11_0047"></a>

## PostgreSQL迁移场景<a name="section187801525315"></a>

**表 1**  目标数据库参数max\_worker\_processes是否足够

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>目标数据库参数max_worker_processes是否足够。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>目标数据库的max_worker_processes参数值不能比源数据库的参数值小，否则，可能会导致迁移失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>不通过提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p2015019633418"><a name="p2015019633418"></a><a name="p2015019633418"></a><strong id="b7150136123410"><a name="b7150136123410"></a><a name="b7150136123410"></a>不通过原因</strong>：目标数据库参数max_worker_processes比源数据库的小。</p>
<p id="p16150966343"><a name="p16150966343"></a><a name="p16150966343"></a><strong id="b18861151514619"><a name="b18861151514619"></a><a name="b18861151514619"></a>处理建议</strong>：修改源数据库或目标数据库的参数，结束迁移后建议恢复修改的参数。</p>
</td>
</tr>
</tbody>
</table>


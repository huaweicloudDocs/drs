# 目标数据库参数max\_prepared\_transactions是否足够<a name="drs_11_0051"></a>

## PostgreSQL迁移场景<a name="section10111242048"></a>

**表 1**  目标数据库参数max\_prepared\_transactions是否足够

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>目标数据库参数max_prepared_transactions是否足够。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>目标数据库的max_prepared_transactions参数值不能比源数据库的参数值小，否则，可能会导致迁移失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>失败提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p20871250163319"><a name="p20871250163319"></a><a name="p20871250163319"></a><strong id="b75018522404"><a name="b75018522404"></a><a name="b75018522404"></a><strong id="b10501165213401"><a name="b10501165213401"></a><a name="b10501165213401"></a>失败原因</strong>：</strong>目标数据库参数max_prepared_transactions比源数据库的小。</p>
<p id="p1784825343514"><a name="p1784825343514"></a><a name="p1784825343514"></a><strong id="b876719201363"><a name="b876719201363"></a><a name="b876719201363"></a>处理建议</strong>：修改源数据库或目标数据库的参数，结束迁移后建议恢复修改的参数。</p>
</td>
</tr>
</tbody>
</table>


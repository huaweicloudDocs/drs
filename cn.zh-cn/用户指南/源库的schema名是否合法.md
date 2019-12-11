# 源库的schema名是否合法<a name="drs_11_0104"></a>

## PostgreSQL迁移场景<a name="section14885958191920"></a>

**表 1**  源库的schema名是否合法

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>源库的schema名是否合法。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>源数据库的schema名不支持 '" .字符，检查源数据库schema名是否合法，若存在不合法的字符，会导致数据同步失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>失败提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p195635219105"><a name="p195635219105"></a><a name="p195635219105"></a><strong id="b15638219102"><a name="b15638219102"></a><a name="b15638219102"></a>失败原因</strong>：源数据库schema名包含不支持的字符。</p>
<p id="p5596164719372"><a name="p5596164719372"></a><a name="p5596164719372"></a><strong id="b155961647123711"><a name="b155961647123711"></a><a name="b155961647123711"></a>处理建议</strong>：通过执行如下语句，在源数据库修改包含不支持字符的schema名。</p>
<pre class="codeblock" id="codeblock167871438382"><a name="codeblock167871438382"></a><a name="codeblock167871438382"></a>alter schema old_name rename to new_name;</pre>
</td>
</tr>
</tbody>
</table>


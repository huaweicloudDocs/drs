# 源数据库集合TTL索引检查<a name="drs_11_0201"></a>

## MongoDB迁移场景<a name="section1238917511343"></a>

**表 1**  源数据库集合TTL索引检查

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11.06%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="88.94%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>源数据库集合TTL索引检查。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11.06%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="88.94%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>TTL索引会因为源数据库和目标库数据的时区，时钟不一致导致迁移后数据不一致。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11.06%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>失败提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="88.94%" headers="mcps1.2.3.3.1 "><p id="p120814434258"><a name="p120814434258"></a><a name="p120814434258"></a><strong id="b57571055142517"><a name="b57571055142517"></a><a name="b57571055142517"></a>告警原因：</strong>TTL索引会因为源数据库和目标库数据的时区，时钟不一致导致迁移后数据不一致。</p>
<p id="p7816154219281"><a name="p7816154219281"></a><a name="p7816154219281"></a><strong id="b1681613421284"><a name="b1681613421284"></a><a name="b1681613421284"></a>处理建议：</strong>如果关注存在TTL索引的集合的数据的一致性，需要删除TTL索引或者不迁移存在TTL索引的集合。</p>
<p id="p13747724102918"><a name="p13747724102918"></a><a name="p13747724102918"></a>删除索引的命令请参考如下命令：</p>
<pre class="codeblock" id="codeblock14812143652910"><a name="codeblock14812143652910"></a><a name="codeblock14812143652910"></a>db.集合名.dropIndex(索引名)</pre>
</td>
</tr>
</tbody>
</table>


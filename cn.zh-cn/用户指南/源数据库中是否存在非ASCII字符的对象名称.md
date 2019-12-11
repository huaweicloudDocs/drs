# 源数据库中是否存在非ASCII字符的对象名称<a name="drs_11_0022"></a>

## MySQL迁移场景<a name="section528014415227"></a>

**表 1**  源数据库中是否存在非ASCII字符的对象名称

<a name="table574763395315"></a>
<table><tbody><tr id="row19763133115317"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p20763193325317"><a name="p20763193325317"></a><a name="p20763193325317"></a><strong id="b6763143319536"><a name="b6763143319536"></a><a name="b6763143319536"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p1846685615535"><a name="p1846685615535"></a><a name="p1846685615535"></a>源数据库中是否存在非ASCII字符的对象名称。</p>
</td>
</tr>
<tr id="row4778163311536"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p6778153375320"><a name="p6778153375320"></a><a name="p6778153375320"></a><strong id="b37941733205312"><a name="b37941733205312"></a><a name="b37941733205312"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p8903155155415"><a name="p8903155155415"></a><a name="p8903155155415"></a>源数据库对象名称存在非ASCII码字符，导致迁移失败。</p>
</td>
</tr>
<tr id="row177941133145315"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1979403375310"><a name="p1979403375310"></a><a name="p1979403375310"></a><strong id="b48101433165313"><a name="b48101433165313"></a><a name="b48101433165313"></a>失败提示及<strong id="b14490151682817"><a name="b14490151682817"></a><a name="b14490151682817"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p27421116719"><a name="p27421116719"></a><a name="p27421116719"></a><strong id="b3733349123219"><a name="b3733349123219"></a><a name="b3733349123219"></a>失败原因</strong>：源数据库对象名称中存在非ASCII码字符。</p>
<p id="p17122249153518"><a name="p17122249153518"></a><a name="p17122249153518"></a><strong id="b1142717819357"><a name="b1142717819357"></a><a name="b1142717819357"></a>处理建议</strong>：修改源数据库中存在的非ASCII字符对象名称。</p>
</td>
</tr>
</tbody>
</table>


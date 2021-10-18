# 源数据库binlog保留时间检查<a name="drs_11_0016"></a>

## MySQL迁移场景<a name="section19914332145"></a>

**表 1**  源数据库binlog保留时间检查

<a name="table0430722319"></a>
<table><tbody><tr id="row16591716236"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p159187192315"><a name="p159187192315"></a><a name="p159187192315"></a><strong id="b374373233"><a name="b374373233"></a><a name="b374373233"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p177417182316"><a name="p177417182316"></a><a name="p177417182316"></a>源数据库<span class="keyword" id="keyword930142123613"><a name="keyword930142123613"></a><a name="keyword930142123613"></a>binlog保留时间</span>检查。</p>
</td>
</tr>
<tr id="row1974127152311"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p11909722311"><a name="p11909722311"></a><a name="p11909722311"></a><strong id="b1290117172315"><a name="b1290117172315"></a><a name="b1290117172315"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p13901173235"><a name="p13901173235"></a><a name="p13901173235"></a>检查源数据库binlog保留的时间，在磁盘允许的情况下，保留时间设置的越长越好。</p>
</td>
</tr>
<tr id="row91371272231"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p418616911259"><a name="p418616911259"></a><a name="p418616911259"></a><strong id="b759763871616"><a name="b759763871616"></a><a name="b759763871616"></a>不通过提示及<strong id="b14490151682817"><a name="b14490151682817"></a><a name="b14490151682817"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p6139134312414"><a name="p6139134312414"></a><a name="p6139134312414"></a><strong id="b146994160230"><a name="b146994160230"></a><a name="b146994160230"></a>不通过原因</strong>：源数据库binlog保留时间没有设置。</p>
<p id="p5608853254"><a name="p5608853254"></a><a name="p5608853254"></a><strong id="b18895453327"><a name="b18895453327"></a><a name="b18895453327"></a>处理建议</strong>：</p>
<p id="p1731594142520"><a name="p1731594142520"></a><a name="p1731594142520"></a>登录源数据库，执行如下SQL语句，设置binlog的保留时间：</p>
<pre class="codeblock" id="codeblock1959103142910"><a name="codeblock1959103142910"></a><a name="codeblock1959103142910"></a>call mysql.rds_set_configuration('binlog retention hours', n); </pre>
<p id="p516724532419"><a name="p516724532419"></a><a name="p516724532419"></a>其中n是大于0并且小于等于168的整数。</p>
</td>
</tr>
</tbody>
</table>


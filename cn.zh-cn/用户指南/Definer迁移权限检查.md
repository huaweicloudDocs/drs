# Definer迁移权限检查<a name="drs_15_0016"></a>

## MySQL迁移场景<a name="section7731193174617"></a>

**表 1**  Definer迁移权限检查

<a name="table2803172865716"></a>
<table><tbody><tr id="row1781817289571"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p6834182810574"><a name="p6834182810574"></a><a name="p6834182810574"></a><strong id="b1683462820577"><a name="b1683462820577"></a><a name="b1683462820577"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p10834162825719"><a name="p10834162825719"></a><a name="p10834162825719"></a>Definer迁移权限检查。</p>
</td>
</tr>
<tr id="row1783414283575"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p14834102819579"><a name="p14834102819579"></a><a name="p14834102819579"></a><strong id="b583422810578"><a name="b583422810578"></a><a name="b583422810578"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p11921724131114"><a name="p11921724131114"></a><a name="p11921724131114"></a>出云场景的Definer迁移需要目标库账号具有all privileges权限。</p>
</td>
</tr>
<tr id="row188511828155716"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p11851102818570"><a name="p11851102818570"></a><a name="p11851102818570"></a><strong id="b885192812571"><a name="b885192812571"></a><a name="b885192812571"></a>失败提示及<strong id="b117671048113514"><a name="b117671048113514"></a><a name="b117671048113514"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p82721034195911"><a name="p82721034195911"></a><a name="p82721034195911"></a><strong id="b11803542135910"><a name="b11803542135910"></a><a name="b11803542135910"></a>失败原因</strong>：目标库的指定账号当前权限不足。</p>
<p id="p161906137128"><a name="p161906137128"></a><a name="p161906137128"></a><strong id="b1619081381218"><a name="b1619081381218"></a><a name="b1619081381218"></a>处理建议</strong>：选择Definer指定为目标数据库连接用户账号，或者赋予目标数据库USER all privileges权限。</p>
<p id="p569412165121"><a name="p569412165121"></a><a name="p569412165121"></a>可参考如下语句：</p>
<pre class="codeblock" id="codeblock1587173531212"><a name="codeblock1587173531212"></a><a name="codeblock1587173531212"></a>grant all privileges on *.* to ‘user’@’host’</pre>
</td>
</tr>
</tbody>
</table>


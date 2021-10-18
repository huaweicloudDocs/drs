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
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p11921724131114"><a name="p11921724131114"></a><a name="p11921724131114"></a>入云场景Definer迁移需要源库帐号具有all privileges权限，出云场景的Definer迁移需要目标库帐号具有all privileges权限。</p>
</td>
</tr>
<tr id="row188511828155716"><th class="firstcol" rowspan="2" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p11851102818570"><a name="p11851102818570"></a><a name="p11851102818570"></a><strong id="b885192812571"><a name="b885192812571"></a><a name="b885192812571"></a>不通过提示及<strong id="b117671048113514"><a name="b117671048113514"></a><a name="b117671048113514"></a>处理建议</strong></strong></p>
<p id="p11121344111815"><a name="p11121344111815"></a><a name="p11121344111815"></a></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p82721034195911"><a name="p82721034195911"></a><a name="p82721034195911"></a><strong id="b11803542135910"><a name="b11803542135910"></a><a name="b11803542135910"></a>不通过原因</strong>：目标库的指定帐号当前权限不足。</p>
<p id="p161906137128"><a name="p161906137128"></a><a name="p161906137128"></a><strong id="b1619081381218"><a name="b1619081381218"></a><a name="b1619081381218"></a>处理建议</strong>：选择Definer指定为目标数据库连接用户账号，或者赋予目标数据库用户all privileges权限。</p>
<p id="p569412165121"><a name="p569412165121"></a><a name="p569412165121"></a>可参考如下语句：</p>
<pre class="codeblock" id="codeblock1587173531212"><a name="codeblock1587173531212"></a><a name="codeblock1587173531212"></a>grant all privileges on *.* to ‘user’@’host’</pre>
</td>
</tr>
<tr id="row61201644181819"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p3961114991814"><a name="p3961114991814"></a><a name="p3961114991814"></a><strong id="b179611949161813"><a name="b179611949161813"></a><a name="b179611949161813"></a>不通过原因</strong>：源库的指定帐号当前权限不足。</p>
<p id="p18925174417197"><a name="p18925174417197"></a><a name="p18925174417197"></a><strong id="b1692524414199"><a name="b1692524414199"></a><a name="b1692524414199"></a>处理建议</strong>：</p>
<a name="ol105571046121911"></a><a name="ol105571046121911"></a><ol id="ol105571046121911"><li>将所有Definer迁移到指定目标库用户下：在配置目标库时选择<span class="uicontrol" id="uicontrol0497103014254"><a name="uicontrol0497103014254"></a><a name="uicontrol0497103014254"></a>“所有Definer迁移到该用户下”</span>，使得所有对象Definer均在该指定用户下。</li><li>保留原Definer设置，但需要赋予源数据库用户all privileges权限。<p id="p1498472817"><a name="p1498472817"></a><a name="p1498472817"></a>可参考如下语句：</p>
<pre class="codeblock" id="codeblock010018496813"><a name="codeblock010018496813"></a><a name="codeblock010018496813"></a>grant all privileges on *.* to ‘user’@’host’</pre>
</li></ol>
</td>
</tr>
</tbody>
</table>


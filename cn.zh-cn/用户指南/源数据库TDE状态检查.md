# 源数据库TDE状态检查<a name="drs_11_0035"></a>

## Microsoft SQL Server迁移场景<a name="section1146051884113"></a>

**表 1**  源数据库TDE状态检查

<a name="table7267171318319"></a>
<table><tbody><tr id="row1228220136310"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p428212134312"><a name="p428212134312"></a><a name="p428212134312"></a><strong id="b13282713439"><a name="b13282713439"></a><a name="b13282713439"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p82987132317"><a name="p82987132317"></a><a name="p82987132317"></a><span class="keyword" id="keyword1097119383419"><a name="keyword1097119383419"></a><a name="keyword1097119383419"></a>源数据库TDE状态</span>检查。</p>
</td>
</tr>
<tr id="row929810131437"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p14313513134"><a name="p14313513134"></a><a name="p14313513134"></a><strong id="b1231312135310"><a name="b1231312135310"></a><a name="b1231312135310"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p23135130311"><a name="p23135130311"></a><a name="p23135130311"></a>源数据库不允许存在开启TDE的库。</p>
</td>
</tr>
<tr id="row103600131319"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p20492722124511"><a name="p20492722124511"></a><a name="p20492722124511"></a><strong id="b432981319317"><a name="b432981319317"></a><a name="b432981319317"></a>失败提示及<strong id="b117671048113514"><a name="b117671048113514"></a><a name="b117671048113514"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p122894551449"><a name="p122894551449"></a><a name="p122894551449"></a><strong id="b751573504417"><a name="b751573504417"></a><a name="b751573504417"></a>失败原因</strong>：源数据库存在开启TDE的库。</p>
<p id="p66545351045"><a name="p66545351045"></a><a name="p66545351045"></a><strong id="b15967135110384"><a name="b15967135110384"></a><a name="b15967135110384"></a>处理建议</strong>：对开启了TDE的每个数据库执行如下SQL语句：</p>
<pre class="codeblock" id="codeblock2096092514121"><a name="codeblock2096092514121"></a><a name="codeblock2096092514121"></a>ALTER DATABASE [数据库名] SET ENCRYPTION OFF;
GO</pre>
</td>
</tr>
</tbody>
</table>


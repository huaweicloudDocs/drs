# 源数据库与目标数据库的BLOCK\_SIZE参数值是否相同<a name="drs_11_0063"></a>

## PostgreSQL迁移场景<a name="section2055414110311"></a>

**表 1**  源数据库与目标数据库的BLOCK\_SIZE参数值是否相同

<a name="table195653327432"></a>
<table><tbody><tr id="row7565632164318"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p11565132194313"><a name="p11565132194313"></a><a name="p11565132194313"></a><strong id="b6565203254311"><a name="b6565203254311"></a><a name="b6565203254311"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p3565133234318"><a name="p3565133234318"></a><a name="p3565133234318"></a>源数据库与目标数据库的BLOCK_SIZE参数值是否相同。</p>
</td>
</tr>
<tr id="row145651232104317"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p5565173224315"><a name="p5565173224315"></a><a name="p5565173224315"></a><strong id="b556573254316"><a name="b556573254316"></a><a name="b556573254316"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p656563214319"><a name="p656563214319"></a><a name="p656563214319"></a>如果源数据库与目标数据库的BLOCK_SIZE参数值不同，则会导致迁移失败。</p>
</td>
</tr>
<tr id="row45652032164319"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1556583254317"><a name="p1556583254317"></a><a name="p1556583254317"></a><strong id="b6565832204317"><a name="b6565832204317"></a><a name="b6565832204317"></a>不通过提示及<strong id="b55807361765"><a name="b55807361765"></a><a name="b55807361765"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p58679261532"><a name="p58679261532"></a><a name="p58679261532"></a><strong id="b1466642645714"><a name="b1466642645714"></a><a name="b1466642645714"></a>不通过原因</strong>：源数据库与目标数据库的BLOCK_SIZE参数值不同。</p>
<p id="p1512182855417"><a name="p1512182855417"></a><a name="p1512182855417"></a><strong id="b204711145585"><a name="b204711145585"></a><a name="b204711145585"></a>处理建议</strong>：请更换与目标数据库的BLOCK_SIZE参数值相同的PostgreSQL数据库, 或使用官方已编译好的二进制包。</p>
</td>
</tr>
</tbody>
</table>


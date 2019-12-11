# 源数据库中是否存在非ASCII字符的触发器名（屏蔽）<a name="drs_11_0073"></a>

## MySQL迁移场景<a name="section12971103502818"></a>

**表 1**  源数据库中是否存在非ASCII字符的触发器名

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>源数据库中是否存在非ASCII字符的触发器名。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>源数据库中不能存在非ASCII字符的触发器名，若存在，可能会导致迁移失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>告警提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p18705213564"><a name="p18705213564"></a><a name="p18705213564"></a><strong id="b16814162110612"><a name="b16814162110612"></a><a name="b16814162110612"></a>告警原因</strong>：源数据库中存在非ASCII字符的发器名。</p>
<p id="p10194121217610"><a name="p10194121217610"></a><a name="p10194121217610"></a><strong id="b12194131219616"><a name="b12194131219616"></a><a name="b12194131219616"></a>处理建议</strong>：针对该问题提供如下解决方法。</p>
<p id="p142318178619"><a name="p142318178619"></a><a name="p142318178619"></a>方法一：</p>
<p id="p1188811411261"><a name="p1188811411261"></a><a name="p1188811411261"></a>单击“上一步”，返回至“迁移模式”页面，迁移对象选择自定义对象，请不要选择包含非ASCII字符名的触发器。</p>
<p id="p1120134619618"><a name="p1120134619618"></a><a name="p1120134619618"></a>方法二：修改触发器名。</p>
</td>
</tr>
</tbody>
</table>


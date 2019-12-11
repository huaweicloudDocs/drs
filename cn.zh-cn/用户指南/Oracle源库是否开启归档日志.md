# Oracle源库是否开启归档日志<a name="drs_15_0025"></a>

## Oracle-\>MySQL数据库迁移场景<a name="section14885958191920"></a>

**表 1**  Oracle源库是否开启归档日志

<a name="table108613815105"></a>
<table><tbody><tr id="row78617819106"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p168610811107"><a name="p168610811107"></a><a name="p168610811107"></a><strong id="b1486781108"><a name="b1486781108"></a><a name="b1486781108"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p1586488107"><a name="p1586488107"></a><a name="p1586488107"></a>Oracle源库是否开启归档日志。</p>
</td>
</tr>
<tr id="row18862089105"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p9862831015"><a name="p9862831015"></a><a name="p9862831015"></a><strong id="b5865817103"><a name="b5865817103"></a><a name="b5865817103"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p886178201010"><a name="p886178201010"></a><a name="p886178201010"></a>Oracle到MySQL的增量迁移，要求源数据库打开归档日志。</p>
</td>
</tr>
<tr id="row28610851019"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1786384108"><a name="p1786384108"></a><a name="p1786384108"></a><strong id="b886188161016"><a name="b886188161016"></a><a name="b886188161016"></a>失败提示及<strong id="b2863810106"><a name="b2863810106"></a><a name="b2863810106"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p17861084104"><a name="p17861084104"></a><a name="p17861084104"></a><strong id="b28612811018"><a name="b28612811018"></a><a name="b28612811018"></a>失败原因</strong>：Oracle源库未打开归档日志。</p>
<p id="p2086784106"><a name="p2086784106"></a><a name="p2086784106"></a><strong id="b14861683102"><a name="b14861683102"></a><a name="b14861683102"></a>处理建议</strong>：在Oracle源库中执行[alter database archivelog]，打开归档日志。</p>
</td>
</tr>
</tbody>
</table>


# binlog\_row\_image参数是否为FULL<a name="drs_11_0064"></a>

## MySQL迁移场景<a name="section1747511100511"></a>

**表 1**  binlog\_row\_image参数是否为FULL

<a name="table195653327432"></a>
<table><tbody><tr id="row7565632164318"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p11565132194313"><a name="p11565132194313"></a><a name="p11565132194313"></a><strong id="b6565203254311"><a name="b6565203254311"></a><a name="b6565203254311"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p3565133234318"><a name="p3565133234318"></a><a name="p3565133234318"></a>binlog_row_image参数是否为FULL。</p>
</td>
</tr>
<tr id="row145651232104317"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p5565173224315"><a name="p5565173224315"></a><a name="p5565173224315"></a><strong id="b556573254316"><a name="b556573254316"></a><a name="b556573254316"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p656563214319"><a name="p656563214319"></a><a name="p656563214319"></a>如果源数据库的binlog_row_image参数不为FULL，则会导致迁移失败。</p>
</td>
</tr>
<tr id="row45652032164319"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1556583254317"><a name="p1556583254317"></a><a name="p1556583254317"></a><strong id="b6565832204317"><a name="b6565832204317"></a><a name="b6565832204317"></a>不通过提示及<strong id="b55807361765"><a name="b55807361765"></a><a name="b55807361765"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p13539173216514"><a name="p13539173216514"></a><a name="p13539173216514"></a><strong id="b125393322510"><a name="b125393322510"></a><a name="b125393322510"></a>不通过原因</strong>：源数据库的binlog_row_image参数不为FULL。</p>
<p id="p1512182855417"><a name="p1512182855417"></a><a name="p1512182855417"></a><strong id="b204711145585"><a name="b204711145585"></a><a name="b204711145585"></a>处理建议</strong>：</p>
<a name="ul17471165020216"></a><a name="ul17471165020216"></a><ul id="ul17471165020216"><li>如果源数据库为云上RDS实例，可通过RDS管理界面的参数配置，将binlog_row_image修改为FULL，完成修改后重启源数据库即可。</li><li>如果源数据库为本地自建库，请参考如下步骤修复。<a name="ol12742027192719"></a><a name="ol12742027192719"></a><ol id="ol12742027192719"><li>登录MySQL源数据库所在服务器。</li><li>手动修改my.cnf配置文件，将binlog_row_image参数值修改为FULL后保存。<pre class="codeblock" id="codeblock146081655172710"><a name="codeblock146081655172710"></a><a name="codeblock146081655172710"></a>binlog_row_image=full</pre>
</li><li>为防止继续生成非全镜像日志导致任务失败，需选择一个非业务时间段，重启源数据库即可。</li></ol>
</li></ul>
</td>
</tr>
</tbody>
</table>


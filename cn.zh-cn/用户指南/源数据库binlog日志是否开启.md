# 源数据库binlog日志是否开启<a name="drs_11_0014"></a>

## MySQL迁移场景<a name="section1620113163122"></a>

**表 1**  源数据库binlog日志是否开启

<a name="table3962804119632"></a>
<table><tbody><tr id="row6364655919632"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p24922316191949"><a name="p24922316191949"></a><a name="p24922316191949"></a><strong id="b22974252191949"><a name="b22974252191949"></a><a name="b22974252191949"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p18266321194714"><a name="p18266321194714"></a><a name="p18266321194714"></a><span class="keyword" id="keyword201940522348"><a name="keyword201940522348"></a><a name="keyword201940522348"></a>源数据库binlog日志</span>是否开启。</p>
</td>
</tr>
<tr id="row4711154819632"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p38122892191949"><a name="p38122892191949"></a><a name="p38122892191949"></a><strong id="b7561711191949"><a name="b7561711191949"></a><a name="b7561711191949"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p16470375194725"><a name="p16470375194725"></a><a name="p16470375194725"></a>检查源库是否开启了binlog日志功能。</p>
</td>
</tr>
<tr id="row2611577919632"><th class="firstcol" rowspan="4" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p9560654191949"><a name="p9560654191949"></a><a name="p9560654191949"></a><strong id="b18937028191949"><a name="b18937028191949"></a><a name="b18937028191949"></a>不通过提示及<strong id="b14490151682817"><a name="b14490151682817"></a><a name="b14490151682817"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p19545633181819"><a name="p19545633181819"></a><a name="p19545633181819"></a><strong id="b6416132361612"><a name="b6416132361612"></a><a name="b6416132361612"></a>不通过原因</strong>：源数据库连接失败，导致该项检查无法进行。</p>
<p id="p136381932191813"><a name="p136381932191813"></a><a name="p136381932191813"></a><strong id="b14408155473114"><a name="b14408155473114"></a><a name="b14408155473114"></a>处理建议</strong>：查看源数据库连接是否成功。</p>
</td>
</tr>
<tr id="row18846133810176"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p3846153841717"><a name="p3846153841717"></a><a name="p3846153841717"></a><strong id="b892114819180"><a name="b892114819180"></a><a name="b892114819180"></a>不通过原因</strong>：用户基本权限不足。</p>
<p id="p113919187183"><a name="p113919187183"></a><a name="p113919187183"></a><strong id="b540945712315"><a name="b540945712315"></a><a name="b540945712315"></a>处理建议</strong>：查看对应数据库帐号权限是否符合迁移要求。</p>
<div class="note" id="note1594215405815"><a name="note1594215405815"></a><a name="note1594215405815"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p89426475810"><a name="p89426475810"></a><a name="p89426475810"></a>DRS要求的MySQL权限以及授权操作，请参见<a href="https://support.huaweicloud.com/drs_faq/drs_04_0034.html" target="_blank" rel="noopener noreferrer">DRS要求的MySQL权限有哪些</a>。</p>
</div></div>
</td>
</tr>
<tr id="row82211415171"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p17221741181716"><a name="p17221741181716"></a><a name="p17221741181716"></a><strong id="b144821849121810"><a name="b144821849121810"></a><a name="b144821849121810"></a>不通过原因</strong>：内部错误。</p>
<p id="p16935228161818"><a name="p16935228161818"></a><a name="p16935228161818"></a><strong id="b65021459123119"><a name="b65021459123119"></a><a name="b65021459123119"></a>处理建议</strong>：请联系华为技术支持人员处理。</p>
</td>
</tr>
<tr id="row1605119819632"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p84501827171211"><a name="p84501827171211"></a><a name="p84501827171211"></a><strong id="b6450172781213"><a name="b6450172781213"></a><a name="b6450172781213"></a>不通过原因</strong>：源数据库未开启binlog日志功能。</p>
<p id="p188251676138"><a name="p188251676138"></a><a name="p188251676138"></a><strong id="b118257771318"><a name="b118257771318"></a><a name="b118257771318"></a>处理建议</strong>：</p>
<a name="ul1578371832611"></a><a name="ul1578371832611"></a><ul id="ul1578371832611"><li>如果源数据库为本地自建库，建议参考如下操作开启binlog日志。<a name="ol1378310183261"></a><a name="ol1378310183261"></a><ol id="ol1378310183261"><li>查看binlog日志是否开启。<pre class="codeblock" id="codeblock1278313187263"><a name="codeblock1278313187263"></a><a name="codeblock1278313187263"></a>show variables like "log_bin"\G;</pre>
<p id="p25474920524"><a name="p25474920524"></a><a name="p25474920524"></a><a name="image15549492526"></a><a name="image15549492526"></a><span><img id="image15549492526" src="figures/drs_logbin_off.png" height="79.80000000000001" width="399"></span></p>
</li><li>如果是关闭状态，在mysql配置文件my.cnf或my.ini中的[mysqld]标签下增加一行log-bin = mysql-bin。<p id="p729190175318"><a name="p729190175318"></a><a name="p729190175318"></a><a name="image829110035313"></a><a name="image829110035313"></a><span><img id="image829110035313" src="figures/drs_logbin.png"></span></p>
</li><li>重启数据库。<p id="p643414108533"><a name="p643414108533"></a><a name="p643414108533"></a><a name="image144341105531"></a><a name="image144341105531"></a><span><img id="image144341105531" src="figures/drs_logbin_on.jpg" height="73.720038" width="399"></span></p>
</li></ol>
</li><li>如果源数据库为云上RDS实例，可建议联系技术人员进行处理。</li></ul>
</td>
</tr>
</tbody>
</table>


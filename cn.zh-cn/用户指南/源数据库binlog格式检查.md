# 源数据库binlog格式检查<a name="drs_11_0015"></a>

## MySQL迁移场景<a name="section79804282211"></a>

**表 1**  源数据库binlog格式检查

<a name="table105501938121611"></a>
<table><tbody><tr id="row856613387166"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p85668382163"><a name="p85668382163"></a><a name="p85668382163"></a><strong id="b205661938131612"><a name="b205661938131612"></a><a name="b205661938131612"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p558163851620"><a name="p558163851620"></a><a name="p558163851620"></a><span class="keyword" id="keyword134960248360"><a name="keyword134960248360"></a><a name="keyword134960248360"></a>源数据库binlog格式</span>检查。</p>
</td>
</tr>
<tr id="row658143815161"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1658113812162"><a name="p1658113812162"></a><a name="p1658113812162"></a><strong id="b758113386165"><a name="b758113386165"></a><a name="b758113386165"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p358118389167"><a name="p358118389167"></a><a name="p358118389167"></a>检查源数据库的binlog格式是不是行格式。</p>
</td>
</tr>
<tr id="row175811138201620"><th class="firstcol" rowspan="4" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p759733817168"><a name="p759733817168"></a><a name="p759733817168"></a><strong id="b759763871616"><a name="b759763871616"></a><a name="b759763871616"></a>不通过提示及<strong id="b14490151682817"><a name="b14490151682817"></a><a name="b14490151682817"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p13653759172212"><a name="p13653759172212"></a><a name="p13653759172212"></a><strong id="b290485001816"><a name="b290485001816"></a><a name="b290485001816"></a>不通过原因</strong>：源数据库连接失败，导致该项检查无法进行。</p>
<p id="p162275813224"><a name="p162275813224"></a><a name="p162275813224"></a><strong id="b2455201933220"><a name="b2455201933220"></a><a name="b2455201933220"></a>处理建议</strong>：查看源数据库连接是否成功。</p>
</td>
</tr>
<tr id="row1852791118226"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p552710117226"><a name="p552710117226"></a><a name="p552710117226"></a><strong id="b1015351118233"><a name="b1015351118233"></a><a name="b1015351118233"></a>不通过原因</strong>：用户基本权限不足。</p>
<p id="p6200129142210"><a name="p6200129142210"></a><a name="p6200129142210"></a><strong id="b7939132123214"><a name="b7939132123214"></a><a name="b7939132123214"></a>处理建议</strong>：查看对应数据库帐号权限是否符合迁移要求。</p>
</td>
</tr>
<tr id="row1573613102214"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p957315132221"><a name="p957315132221"></a><a name="p957315132221"></a><strong id="b19195139234"><a name="b19195139234"></a><a name="b19195139234"></a>不通过原因</strong>：源数据库的binlog格式不是row格式。</p>
<p id="p428019342238"><a name="p428019342238"></a><a name="p428019342238"></a><strong id="b27655239328"><a name="b27655239328"></a><a name="b27655239328"></a>处理建议</strong>：</p>
<a name="ul167621317280"></a><a name="ul167621317280"></a><ul id="ul167621317280"><li>如果源数据库为本地自建库，请通过如下方法，修改源数据库binlog格式：<p id="p126991432175411"><a name="p126991432175411"></a><a name="p126991432175411"></a>方法一：手动修改my.cnf或my.ini配置文件，然后重启数据库。</p>
<pre class="codeblock" id="codeblock1646834125515"><a name="codeblock1646834125515"></a><a name="codeblock1646834125515"></a>binlog_format=row</pre>
<p id="p3961101785610"><a name="p3961101785610"></a><a name="p3961101785610"></a>方法二：执行如下命令，中断所有业务连接。</p>
<pre class="codeblock" id="codeblock238753765620"><a name="codeblock238753765620"></a><a name="codeblock238753765620"></a>set global binlog_format='ROW'</pre>
<p id="p1636648185617"><a name="p1636648185617"></a><a name="p1636648185617"></a>然后手动修改my.cnf或my.ini配置文件。</p>
<pre class="codeblock" id="codeblock599085715719"><a name="codeblock599085715719"></a><a name="codeblock599085715719"></a>binlog_format=row</pre>
<p id="p22572051105714"><a name="p22572051105714"></a><a name="p22572051105714"></a>在row模式下，日志增长速率会变大，注意磁盘使用情况。</p>
<div class="note" id="note1594215405815"><a name="note1594215405815"></a><a name="note1594215405815"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p89426475810"><a name="p89426475810"></a><a name="p89426475810"></a>MySQL Global binlog_format参数无法对已连接的会话生效，最安全的切换方式请参见<a href="https://support.huaweicloud.com/drs_faq/drs_16_0002.html" target="_blank" rel="noopener noreferrer">MySQL源库设置了global binlog_format = ROW没有立即生效？</a>。</p>
</div></div>
</li><li>如果源数据库为云上RDS实例，请使用参数组功能，将源数据库参数binlog_format修改为ROW，重启数据库后生效。<div class="note" id="note187501538201"><a name="note187501538201"></a><a name="note187501538201"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p173313201211"><a name="p173313201211"></a><a name="p173313201211"></a>MySQL Global binlog_format参数无法对已连接的会话生效，最安全的切换方式请参见<a href="https://support.huaweicloud.com/drs_faq/drs_16_0002.html" target="_blank" rel="noopener noreferrer">MySQL源库设置了global binlog_format = ROW没有立即生效？</a>。</p>
</div></div>
</li></ul>
</td>
</tr>
<tr id="row359716386162"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p103251455142220"><a name="p103251455142220"></a><a name="p103251455142220"></a><strong id="b146994160230"><a name="b146994160230"></a><a name="b146994160230"></a>不通过原因</strong>：内部错误。</p>
<p id="p181227567221"><a name="p181227567221"></a><a name="p181227567221"></a><strong id="b195621326123217"><a name="b195621326123217"></a><a name="b195621326123217"></a>处理建议</strong>：请联系华为技术支持人员处理。</p>
</td>
</tr>
</tbody>
</table>


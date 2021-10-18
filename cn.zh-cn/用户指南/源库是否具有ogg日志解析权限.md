# 源库是否具有ogg日志解析权限<a name="drs_16_1136"></a>

## Oracle-\>GaussDB\(for openGauss\)同步场景<a name="section77221541188"></a>

**表 1**  源库是否具有ogg日志解析权限

<a name="table3287441519624"></a>
<table><tbody><tr id="row2599816919624"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p28669136191931"><a name="p28669136191931"></a><a name="p28669136191931"></a><strong id="b56695634191931"><a name="b56695634191931"></a><a name="b56695634191931"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p3699183018394"><a name="p3699183018394"></a><a name="p3699183018394"></a>源库是否具有ogg日志解析权限。</p>
</td>
</tr>
<tr id="row5314419219624"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p59166431191931"><a name="p59166431191931"></a><a name="p59166431191931"></a><strong id="b62735832191931"><a name="b62735832191931"></a><a name="b62735832191931"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p11699123053918"><a name="p11699123053918"></a><a name="p11699123053918"></a>源库使用XStream日志读取模式，需要打开源库的ENABLE_GOLDENGATE_REPLICATION开关。</p>
</td>
</tr>
<tr id="row3381416819624"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p33285247191931"><a name="p33285247191931"></a><a name="p33285247191931"></a><strong id="b31131775191931"><a name="b31131775191931"></a><a name="b31131775191931"></a>不通过提示及<strong id="b14490151682817"><a name="b14490151682817"></a><a name="b14490151682817"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p570023015391"><a name="p570023015391"></a><a name="p570023015391"></a><strong id="b13700143015391"><a name="b13700143015391"></a><a name="b13700143015391"></a>不通过原因：</strong>源数据库xstream日志读取模式未打开。</p>
<p id="p15700203013391"><a name="p15700203013391"></a><a name="p15700203013391"></a><strong id="b1700630173911"><a name="b1700630173911"></a><a name="b1700630173911"></a>处理建议：</strong>请检查数据库版本支持XStream日志读取模式且具有ogg license后，在源库执行“ALTER SYSTEM SET ENABLE_GOLDENGATE_REPLICATION = TRUE SCOPE=BOTH;”以打开XStream日志读取模式。</p>
</td>
</tr>
</tbody>
</table>


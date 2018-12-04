# SSL安全连接检查<a name="drs_11_0017"></a>

## 源数据库为MySQL数据库<a name="section17701049191516"></a>

**表 1**  SSL安全连接检查

<a name="table5112628104844"></a>
<table><tbody><tr id="row23611040104844"><th class="firstcol" valign="top" width="8.540000000000001%" id="mcps1.2.3.1.1"><p id="p33446093104844"><a name="p33446093104844"></a><a name="p33446093104844"></a><strong id="b32579387104844"><a name="b32579387104844"></a><a name="b32579387104844"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.46%" headers="mcps1.2.3.1.1 "><p id="p21684690104844"><a name="p21684690104844"></a><a name="p21684690104844"></a>SSL安全连接检查。</p>
</td>
</tr>
<tr id="row60944485104844"><th class="firstcol" valign="top" width="8.540000000000001%" id="mcps1.2.3.2.1"><p id="p37556256104844"><a name="p37556256104844"></a><a name="p37556256104844"></a><strong id="b2461985104844"><a name="b2461985104844"></a><a name="b2461985104844"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.46%" headers="mcps1.2.3.2.1 "><p id="p65203114104844"><a name="p65203114104844"></a><a name="p65203114104844"></a>检查源数据库的SSL安全连接设置状态。</p>
</td>
</tr>
<tr id="row49957115104844"><th class="firstcol" rowspan="10" valign="top" width="8.540000000000001%" id="mcps1.2.3.3.1"><p id="p19994475104844"><a name="p19994475104844"></a><a name="p19994475104844"></a><strong id="b45732548104844"><a name="b45732548104844"></a><a name="b45732548104844"></a>失败提示及处理建议</strong></p>
<p id="p547312923918"><a name="p547312923918"></a><a name="p547312923918"></a></p>
</th>
<td class="cellrowborder" valign="top" width="91.46%" headers="mcps1.2.3.3.1 "><p id="p81193432816"><a name="p81193432816"></a><a name="p81193432816"></a><strong id="b146994160230"><a name="b146994160230"></a><a name="b146994160230"></a>失败原因</strong>：源数据库连接失败，导致该项检查无法进行。</p>
<p id="p5608853254"><a name="p5608853254"></a><a name="p5608853254"></a><strong id="b39059592324"><a name="b39059592324"></a><a name="b39059592324"></a>处理建议</strong>：查看源数据库连接是否成功。</p>
</td>
</tr>
<tr id="row48031612122617"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p158032012182619"><a name="p158032012182619"></a><a name="p158032012182619"></a><strong id="b410261442817"><a name="b410261442817"></a><a name="b410261442817"></a>失败原因</strong>：用户基本权限不足。</p>
<p id="p115927360289"><a name="p115927360289"></a><a name="p115927360289"></a><strong id="b31407211333"><a name="b31407211333"></a><a name="b31407211333"></a>处理建议</strong>：查看对应数据库帐号权限是否符合迁移要求。</p>
</td>
</tr>
<tr id="row2882415112614"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p288217157263"><a name="p288217157263"></a><a name="p288217157263"></a><strong id="b10430171518285"><a name="b10430171518285"></a><a name="b10430171518285"></a>失败原因</strong>：数据库不可用。</p>
<p id="p5322805285"><a name="p5322805285"></a><a name="p5322805285"></a><strong id="b1534384193314"><a name="b1534384193314"></a><a name="b1534384193314"></a>处理建议</strong>：请联系客服人员处理。</p>
</td>
</tr>
<tr id="row131011618142618"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p12101171882613"><a name="p12101171882613"></a><a name="p12101171882613"></a><strong id="b1868111610285"><a name="b1868111610285"></a><a name="b1868111610285"></a>告警原因</strong>：选择SSL安全连接时，源库用户需设置REQUIRE SSL权限。</p>
<p id="p569732722719"><a name="p569732722719"></a><a name="p569732722719"></a><strong id="b1698182510339"><a name="b1698182510339"></a><a name="b1698182510339"></a>处理建议</strong>：该提示不影响迁移流程，但是如果确定需要SSL安全连接，建议在源库设置迁移帐号的REQUIRE SSL权限。</p>
</td>
</tr>
<tr id="row445016206487"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p18231184804812"><a name="p18231184804812"></a><a name="p18231184804812"></a><strong id="b6765171185013"><a name="b6765171185013"></a><a name="b6765171185013"></a>告警原因</strong>：选择SSL安全连接时，目标库用户需设置REQUIRE SSL权限。</p>
<p id="p182311748164812"><a name="p182311748164812"></a><a name="p182311748164812"></a><strong id="b62801940205016"><a name="b62801940205016"></a><a name="b62801940205016"></a>处理建议</strong>：该提示不影响迁移流程，但是如果确定需要SSL安全连接，建议在目标库设置迁移帐号的REQUIRE SSL权限</p>
</td>
</tr>
<tr id="row6615172032614"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p383014622610"><a name="p383014622610"></a><a name="p383014622610"></a><strong id="b088431882814"><a name="b088431882814"></a><a name="b088431882814"></a>失败原因</strong>：源数据库用户绑定了REQUIRE SSL权限，必须通过SSL方式连接，但是没有上传证书。</p>
<p id="p13821203418275"><a name="p13821203418275"></a><a name="p13821203418275"></a><strong id="b848093310331"><a name="b848093310331"></a><a name="b848093310331"></a>处理建议</strong>：返回到<span class="uicontrol" id="uicontrol49093556112956"><a name="uicontrol49093556112956"></a><a name="uicontrol49093556112956"></a><b>源库及目标库</b></span>页面，打开SSL安全连接开关并且上传证书或者更换源数据库帐号。</p>
</td>
</tr>
<tr id="row484420785312"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p887518965315"><a name="p887518965315"></a><a name="p887518965315"></a><strong id="b8500121311536"><a name="b8500121311536"></a><a name="b8500121311536"></a>失败原因</strong>：目标数据库用户绑定了REQUIRE SSL权限，必须通过SSL方式连接，但是没有上传证书。</p>
<p id="p1887599125314"><a name="p1887599125314"></a><a name="p1887599125314"></a><strong id="b16187131616531"><a name="b16187131616531"></a><a name="b16187131616531"></a>处理建议</strong>：返回到“源库及目标库”页面，打开SSL安全连接开关并且上传证书或者更换目标数据库帐号。</p>
</td>
</tr>
<tr id="row14174945152611"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p0742113819227"><a name="p0742113819227"></a><a name="p0742113819227"></a><strong id="b594720122416"><a name="b594720122416"></a><a name="b594720122416"></a>告警原因</strong>：当前选择的是非SSL方式迁移数据库，DRS需要确保当前提供的源数据库帐号允许通过非SSL方式连接源数据库。</p>
<p id="p428895014222"><a name="p428895014222"></a><a name="p428895014222"></a><strong id="b1890672212242"><a name="b1890672212242"></a><a name="b1890672212242"></a>处理建议</strong>：请手动确保源数据库的系统表权限，或者直接尝试迁移（默认情况下的帐号都是允许非SSL连接的）。</p>
</td>
</tr>
<tr id="row53031256104844"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p42904582275"><a name="p42904582275"></a><a name="p42904582275"></a><strong id="b14119122552816"><a name="b14119122552816"></a><a name="b14119122552816"></a>失败原因</strong>：内部错误。</p>
<p id="p1193185852717"><a name="p1193185852717"></a><a name="p1193185852717"></a><strong id="b20651103816338"><a name="b20651103816338"></a><a name="b20651103816338"></a>处理建议</strong>：请联系客服人员处理。</p>
</td>
</tr>
<tr id="row1847319292394"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p33011335183915"><a name="p33011335183915"></a><a name="p33011335183915"></a><strong id="b43011635123915"><a name="b43011635123915"></a><a name="b43011635123915"></a>失败原因</strong>：源数据库开启了SSL开关，但是没有上传证书。</p>
<p id="p33011335163914"><a name="p33011335163914"></a><a name="p33011335163914"></a><strong id="b2980114663311"><a name="b2980114663311"></a><a name="b2980114663311"></a>处理建议</strong>：关闭源数据库的SSL开关，或者在源库及目标库配置页面上传SSL安全证书。</p>
</td>
</tr>
</tbody>
</table>


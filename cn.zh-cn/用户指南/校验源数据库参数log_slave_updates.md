# 校验源数据库参数log\_slave\_updates<a name="drs_11_0061"></a>

## MySQL迁移、同步和灾备场景<a name="section463012862617"></a>

**表 1**  校验源数据库参数log\_slave\_updates

<a name="table195653327432"></a>
<table><tbody><tr id="row7565632164318"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p11565132194313"><a name="p11565132194313"></a><a name="p11565132194313"></a><strong id="b6565203254311"><a name="b6565203254311"></a><a name="b6565203254311"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p3565133234318"><a name="p3565133234318"></a><a name="p3565133234318"></a>校验源数据库参数log_slave_updates。</p>
</td>
</tr>
<tr id="row145651232104317"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p5565173224315"><a name="p5565173224315"></a><a name="p5565173224315"></a><strong id="b556573254316"><a name="b556573254316"></a><a name="b556573254316"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p656563214319"><a name="p656563214319"></a><a name="p656563214319"></a>源数据库log_slave_updates参数关闭，导致迁移失败。</p>
</td>
</tr>
<tr id="row45652032164319"><th class="firstcol" rowspan="2" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1556583254317"><a name="p1556583254317"></a><a name="p1556583254317"></a><strong id="b6565832204317"><a name="b6565832204317"></a><a name="b6565832204317"></a>失败提示及<strong id="b55807361765"><a name="b55807361765"></a><a name="b55807361765"></a>处理建议</strong></strong></p>
<p id="p14314101265416"><a name="p14314101265416"></a><a name="p14314101265416"></a></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p58679261532"><a name="p58679261532"></a><a name="p58679261532"></a><strong id="b1466642645714"><a name="b1466642645714"></a><a name="b1466642645714"></a>失败原因</strong>：源数据库slave_updates_check关闭。</p>
<p id="p1512182855417"><a name="p1512182855417"></a><a name="p1512182855417"></a><strong id="b204711145585"><a name="b204711145585"></a><a name="b204711145585"></a>处理建议</strong>：在MySQL配置文件my.cnf中的[mysqld]标签下增加一行<strong id="b8874322914"><a name="b8874322914"></a><a name="b8874322914"></a>log_slave_updates=1</strong>，需要重启数据库才能生效。</p>
</td>
</tr>
<tr id="row473512322298"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p16266185513618"><a name="p16266185513618"></a><a name="p16266185513618"></a><strong id="b1266165563617"><a name="b1266165563617"></a><a name="b1266165563617"></a>失败原因</strong>：源数据库为从库且log_slave_updates参数值为OFF。</p>
<p id="p13712413302"><a name="p13712413302"></a><a name="p13712413302"></a><strong id="b1671244309"><a name="b1671244309"></a><a name="b1671244309"></a>处理建议</strong>：将源数据库的log_slave_updates参数设置为ON，需要重启数据库才能生效。</p>
</td>
</tr>
<tr id="row5267125713319"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.5.1"><p id="p53141612145413"><a name="p53141612145413"></a><a name="p53141612145413"></a><strong id="b144823223549"><a name="b144823223549"></a><a name="b144823223549"></a>告警提示及<strong id="b44827225549"><a name="b44827225549"></a><a name="b44827225549"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.5.1 "><p id="p1626775716338"><a name="p1626775716338"></a><a name="p1626775716338"></a><strong id="b2045715327349"><a name="b2045715327349"></a><a name="b2045715327349"></a>告警原因：</strong>源数据库为主库且log_slave_updates参数值为OFF。</p>
<p id="p10515734113413"><a name="p10515734113413"></a><a name="p10515734113413"></a><strong id="b866914353412"><a name="b866914353412"></a><a name="b866914353412"></a>处理建议：</strong>建议将源数据库的log_slave_updates参数设置为ON，需要重启数据库才能生效。如果不发生主从倒换，可不做修改。</p>
</td>
</tr>
</tbody>
</table>


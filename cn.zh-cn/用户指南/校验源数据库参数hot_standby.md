# 校验源数据库参数hot\_standby<a name="drs_11_0056"></a>

## PostgreSQL迁移场景<a name="section1967111015391"></a>

**表 1**  校验源数据库参数hot\_standby

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p12789050113415"><a name="p12789050113415"></a><a name="p12789050113415"></a>校验源数据库参数hot_standby。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p16970716173516"><a name="p16970716173516"></a><a name="p16970716173516"></a>源数据库参数hot_standby必须开启，否则，可能导致迁移失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" rowspan="3" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>失败提示及<strong id="b55807361765"><a name="b55807361765"></a><a name="b55807361765"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p26291645125215"><a name="p26291645125215"></a><a name="p26291645125215"></a><strong id="b1825618155712"><a name="b1825618155712"></a><a name="b1825618155712"></a>失败原因</strong>：源数据库参数<span class="parmname" id="parmname7550193393415"><a name="parmname7550193393415"></a><a name="parmname7550193393415"></a>“hot_standby”</span>必须开启。</p>
<p id="p362314420394"><a name="p362314420394"></a><a name="p362314420394"></a><strong id="b98211451277"><a name="b98211451277"></a><a name="b98211451277"></a>处理建议</strong>：建议修改配置文件postgresql.conf中的<span class="parmname" id="parmname215933403317"><a name="parmname215933403317"></a><a name="parmname215933403317"></a>“hot_standby”</span>参数为<span class="parmvalue" id="parmvalue17721193773316"><a name="parmvalue17721193773316"></a><a name="parmvalue17721193773316"></a>“on”</span>，重启数据库生效。</p>
</td>
</tr>
<tr id="row082917333470"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p79614275530"><a name="p79614275530"></a><a name="p79614275530"></a><strong id="b3838321145715"><a name="b3838321145715"></a><a name="b3838321145715"></a>失败原因</strong>：用户基本权限不足。</p>
<p id="p17341101345410"><a name="p17341101345410"></a><a name="p17341101345410"></a><strong id="b20821164713715"><a name="b20821164713715"></a><a name="b20821164713715"></a>处理建议</strong>：查看对应的数据库帐号权限是否符合迁移要求。</p>
</td>
</tr>
<tr id="row7266537154716"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p117543371522"><a name="p117543371522"></a><a name="p117543371522"></a><strong id="b1227672515714"><a name="b1227672515714"></a><a name="b1227672515714"></a>失败原因</strong>：内部错误。</p>
<p id="p1490342055417"><a name="p1490342055417"></a><a name="p1490342055417"></a><strong id="b1082010491075"><a name="b1082010491075"></a><a name="b1082010491075"></a>处理建议</strong>：请联系客服人员处理。</p>
</td>
</tr>
</tbody>
</table>


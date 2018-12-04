# 校验源数据库参数full\_page\_writes<a name="drs_11_0057"></a>

## PostgreSQL数据库<a name="section2386145716404"></a>

**表 1**  校验源数据库参数full\_page\_writes

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p12789050113415"><a name="p12789050113415"></a><a name="p12789050113415"></a>校验源数据库参数full_page_writes。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p16970716173516"><a name="p16970716173516"></a><a name="p16970716173516"></a>源数据库参数full_page_writes必须开启，否则，可能导致迁移失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" rowspan="3" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>失败提示及处理建议</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p7680162855311"><a name="p7680162855311"></a><a name="p7680162855311"></a><strong id="b1571420165712"><a name="b1571420165712"></a><a name="b1571420165712"></a>失败原因</strong>：源数据库参数<span class="parmname" id="parmname96901237203417"><a name="parmname96901237203417"></a><a name="parmname96901237203417"></a><b>full_page_writes</b></span>必须开启。</p>
<p id="p18751578542"><a name="p18751578542"></a><a name="p18751578542"></a><strong id="b711814118810"><a name="b711814118810"></a><a name="b711814118810"></a>处理建议</strong>：建议修改配置文件postgresql.conf中的<span class="parmname" id="parmname1722114422337"><a name="parmname1722114422337"></a><a name="parmname1722114422337"></a><b>full_page_writes</b></span>参数为<span class="parmvalue" id="parmvalue1475316461332"><a name="parmvalue1475316461332"></a><a name="parmvalue1475316461332"></a><b>on</b></span>，重启数据库生效。</p>
</td>
</tr>
<tr id="row10235710144711"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p79614275530"><a name="p79614275530"></a><a name="p79614275530"></a><strong id="b3838321145715"><a name="b3838321145715"></a><a name="b3838321145715"></a>失败原因</strong>：用户基本权限不足。</p>
<p id="p17341101345410"><a name="p17341101345410"></a><a name="p17341101345410"></a><strong id="b88521821814"><a name="b88521821814"></a><a name="b88521821814"></a>处理建议</strong>：查看对应的数据库帐号权限是否符合迁移要求。</p>
</td>
</tr>
<tr id="row5578151420476"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p117543371522"><a name="p117543371522"></a><a name="p117543371522"></a><strong id="b1227672515714"><a name="b1227672515714"></a><a name="b1227672515714"></a>失败原因</strong>：内部错误。</p>
<p id="p1490342055417"><a name="p1490342055417"></a><a name="p1490342055417"></a><strong id="b10977142081"><a name="b10977142081"></a><a name="b10977142081"></a>处理建议</strong>：请联系客服人员处理。</p>
</td>
</tr>
</tbody>
</table>


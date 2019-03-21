# 数据库参数SQL\_MODE的一致性检查<a name="drs_11_0059"></a>

## MySQL数据库<a name="section052155410574"></a>

**表 1**  数据库参数SQL\_MODE的一致性检查

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>数据库参数SQL_MODE的一致性检查。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>检查源数据库和目标数据库的SQL_MODE参数值是否一致，若不一致，可能会导致迁移失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>失败提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><a name="ul212111382479"></a><a name="ul212111382479"></a><ul id="ul212111382479"><li>如果您进行的是入云操作，请参考如下处理方式。<p id="p718111110460"><a name="p718111110460"></a><a name="p718111110460"></a><strong id="b131811011174614"><a name="b131811011174614"></a><a name="b131811011174614"></a>失败原因</strong>：源数据库和目标数据库的系统参数SQL_MODE不一致。</p>
<p id="p15181161110463"><a name="p15181161110463"></a><a name="p15181161110463"></a><strong id="b31810115463"><a name="b31810115463"></a><a name="b31810115463"></a>处理建议</strong>：建议通过新建参数组修改目标数据库的SQL_MODE参数值，使其与源数据库的参数值保持一致，具体方法请参见<a href="https://support.huaweicloud.com/usermanual-rds/zh-cn_topic_parameter_group.html" target="_blank" rel="noopener noreferrer">新建参数组</a>。</p>
</li><li>如果您进行的是出云操作，请参考如下处理方式。<p id="p03630523425"><a name="p03630523425"></a><a name="p03630523425"></a><strong id="b62391123174314"><a name="b62391123174314"></a><a name="b62391123174314"></a>告警原因</strong>：源数据库和目标数据库的系统参数SQL_MODE的值不一致。</p>
<p id="p1227041812436"><a name="p1227041812436"></a><a name="p1227041812436"></a><strong id="b870912210455"><a name="b870912210455"></a><a name="b870912210455"></a>处理建议</strong>：建议修改目标数据库参数SQL_MODE值，使其与源数据库的参数值保持一致。</p>
</li></ul>
</td>
</tr>
</tbody>
</table>


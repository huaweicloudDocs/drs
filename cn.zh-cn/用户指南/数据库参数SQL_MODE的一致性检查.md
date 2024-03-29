# 数据库参数SQL\_MODE的一致性检查<a name="drs_11_0059"></a>

## MySQL场景<a name="section052155410574"></a>

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
<tr id="row212432224711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>不通过提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><a name="ul212111382479"></a><a name="ul212111382479"></a><ul id="ul212111382479"><li>如果您进行的是入云操作，请参考如下处理方式。<p id="p718111110460"><a name="p718111110460"></a><a name="p718111110460"></a><strong id="b131811011174614"><a name="b131811011174614"></a><a name="b131811011174614"></a>不通过原因</strong>：源数据库和目标数据库的系统参数SQL_MODE不一致。</p>
<p id="p3638135194318"><a name="p3638135194318"></a><a name="p3638135194318"></a><strong id="b13638125117430"><a name="b13638125117430"></a><a name="b13638125117430"></a>处理建议</strong>：建议目标数据库SQL_MODE取值保持和源库一致，并确保源库和目标库不包含禁止值，具体修改方法请参见<a href="https://support.huaweicloud.com/usermanual-rds/rds_configuration.html" target="_blank" rel="noopener noreferrer">编辑参数</a> 。如果涉及MyISAM表的迁移，目标数据库SQL_MODE参数取值中不能包含NO_ENGINE_SUBSTITUTION。</p>
</li><li>如果您进行的是出云操作，请参考如下处理方式。<p id="p03630523425"><a name="p03630523425"></a><a name="p03630523425"></a><strong id="b62391123174314"><a name="b62391123174314"></a><a name="b62391123174314"></a>待确认原因</strong>：源数据库和目标数据库的系统参数SQL_MODE的值不一致。</p>
<p id="p1227041812436"><a name="p1227041812436"></a><a name="p1227041812436"></a><strong id="b870912210455"><a name="b870912210455"></a><a name="b870912210455"></a>处理建议</strong>：建议目标数据库SQL_MODE取值保持和源库一致，并确保源库和目标库不包含禁止值。</p>
</li></ul>
</td>
</tr>
</tbody>
</table>


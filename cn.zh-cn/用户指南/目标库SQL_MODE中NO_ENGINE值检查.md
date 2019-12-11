# 目标库SQL\_MODE中NO\_ENGINE值检查<a name="drs_11_0228"></a>

## MySQL迁移和同步场景<a name="section052155410574"></a>

**表 1**  目标库SQL\_MODE中NO\_ENGINE值检查

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>目标库SQL_MODE中NO_ENGINE值检查。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>迁移的对象中包含引擎为MyISAM的表，目标数据库SQL_MODE不能包含NO_ENGINE_SUBSTITUTION参数，否则可能会导致迁移失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>失败提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p6240286333"><a name="p6240286333"></a><a name="p6240286333"></a><strong id="b3240382333"><a name="b3240382333"></a><a name="b3240382333"></a>失败原因</strong>：目标数据库含有NO_ENGINE_SUBSTITUTION参数。</p>
<p id="p173911223615"><a name="p173911223615"></a><a name="p173911223615"></a><strong id="b14886165111516"><a name="b14886165111516"></a><a name="b14886165111516"></a>处理建议</strong>：建议去除目标数据库SQl_MODE中NO_ENGINE_SUBSTITUTION参数，具体方法请参见《关系型数据库用户指南》中“<a href="https://support.huaweicloud.com/usermanual-rds/zh-cn_topic_configuration.html" target="_blank" rel="noopener noreferrer">编辑参数</a>”章节。</p>
</td>
</tr>
</tbody>
</table>


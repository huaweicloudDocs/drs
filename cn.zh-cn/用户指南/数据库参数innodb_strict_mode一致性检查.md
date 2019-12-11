# 数据库参数innodb\_strict\_mode一致性检查<a name="drs_11_0060"></a>

## MySQL迁移场景<a name="section99687715015"></a>

**表 1**  数据库参数innodb\_strict\_mode一致性检查

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>数据库参数innodb_strict_mode一致性检查。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>检查源数据库和目标数据库的innodb_strict_mode参数值是否一致，若不一致，可能会导致迁移失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>失败提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><a name="ul1451911019512"></a><a name="ul1451911019512"></a><ul id="ul1451911019512"><li>如果您进行的是入云操作，请参考如下处理方式。<p id="p13894141513616"><a name="p13894141513616"></a><a name="p13894141513616"></a><strong id="b0894181517618"><a name="b0894181517618"></a><a name="b0894181517618"></a>失败原因</strong>：源数据库和目标数据库的系统参数innodb_strict_mode不一致。</p>
<p id="p16506115843913"><a name="p16506115843913"></a><a name="p16506115843913"></a><strong id="b05061058133914"><a name="b05061058133914"></a><a name="b05061058133914"></a>处理建议</strong>：建议通过新建参数组修改目标数据库的innodb_strict_mode参数值，使其与源数据库的参数值保持一致，具体方法请参见<a href="https://support.huaweicloud.com/usermanual-rds/zh-cn_topic_parameter_group.html" target="_blank" rel="noopener noreferrer">新建参数组</a>。</p>
</li><li>如果您进行的是出云操作，请参考如下处理方式。<p id="p19373134915523"><a name="p19373134915523"></a><a name="p19373134915523"></a><strong id="b1237320492523"><a name="b1237320492523"></a><a name="b1237320492523"></a>失败原因</strong>：源数据库和目标数据库的系统参数innodb_strict_mode不一致。</p>
<p id="p83731849145212"><a name="p83731849145212"></a><a name="p83731849145212"></a><strong id="b15373194920526"><a name="b15373194920526"></a><a name="b15373194920526"></a>处理建议</strong>：建议修改目标库参数innodb_strict_mode值，使其与源数据库的参数值保持一致。</p>
</li></ul>
</td>
</tr>
</tbody>
</table>


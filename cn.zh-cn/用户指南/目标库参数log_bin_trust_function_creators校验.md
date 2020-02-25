# 目标库参数log\_bin\_trust\_function\_creators校验<a name="drs_11_0225"></a>

## MySQL迁移场景<a name="section1238917511343"></a>

**表 1**  目标库参数log\_bin\_trust\_function\_creators校验

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>目标库参数log_bin_trust_function_creators校验。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>RDS for MySQL到MySQL出云场景下，所选的迁移对象包含自定义函数，但目标数据库不支持创建自定义函数，可能会导致迁移失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>失败提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p18705213564"><a name="p18705213564"></a><a name="p18705213564"></a><strong id="b16814162110612"><a name="b16814162110612"></a><a name="b16814162110612"></a>失败原因</strong>：目标数据库不支持自定义函数。</p>
<p id="p173911223615"><a name="p173911223615"></a><a name="p173911223615"></a><strong id="b10699340356"><a name="b10699340356"></a><a name="b10699340356"></a>处理建议</strong>：请检查目标数据库my.cnf文件中是否存在参数log_bin_trust_function_creators=on，若不存在则在my.cnf中加上该参数， 并重启目标数据库使之生效。</p>
</td>
</tr>
</tbody>
</table>


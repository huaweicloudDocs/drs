# 目标库的GTID功能检查<a name="drs_11_0400"></a>

## MySQL灾备场景<a name="section1238917511343"></a>

**表 1**  目标库的GTID功能检查

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>目标库的GTID功能检查。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>在进行数据灾备时，需要目标数据库开启GTID功能，若未开启，可能会导致迁移失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>告警提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p18705213564"><a name="p18705213564"></a><a name="p18705213564"></a><strong id="b16814162110612"><a name="b16814162110612"></a><a name="b16814162110612"></a>失败原因</strong>：目标数据库GTID未开启。</p>
<p id="p392115761410"><a name="p392115761410"></a><a name="p392115761410"></a><strong id="b169211057131415"><a name="b169211057131415"></a><a name="b169211057131415"></a>处理建议</strong>：通过修改数据库配置文件将源数据库和目标数据库的GTID开启，重启数据库后生效。</p>
<p id="p11981216157"><a name="p11981216157"></a><a name="p11981216157"></a>参考命令如下：</p>
<pre class="codeblock" id="codeblock4526101912151"><a name="codeblock4526101912151"></a><a name="codeblock4526101912151"></a>gtid_mode = on;
log_slave_updates = true; 
enforce_gtid_consistency = on;</pre>
</td>
</tr>
</tbody>
</table>


# 源数据库GTID状态检查<a name="drs_11_0020"></a>

## 源数据库为MySQL数据库<a name="section629895911207"></a>

**表 1**  源数据库GTID状态检查

<a name="table1442354814017"></a>
<table><tbody><tr id="row1543984894010"><th class="firstcol" valign="top" width="8.459999999999999%" id="mcps1.2.3.1.1"><p id="p5439144814407"><a name="p5439144814407"></a><a name="p5439144814407"></a><strong id="b943904844016"><a name="b943904844016"></a><a name="b943904844016"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.53999999999999%" headers="mcps1.2.3.1.1 "><p id="p319214103234"><a name="p319214103234"></a><a name="p319214103234"></a><span class="keyword" id="keyword193922460382"><a name="keyword193922460382"></a><a name="keyword193922460382"></a>源数据库GTID状态</span>检查。</p>
</td>
</tr>
<tr id="row0454148134018"><th class="firstcol" valign="top" width="8.459999999999999%" id="mcps1.2.3.2.1"><p id="p1145414834016"><a name="p1145414834016"></a><a name="p1145414834016"></a><strong id="b154701348174013"><a name="b154701348174013"></a><a name="b154701348174013"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.53999999999999%" headers="mcps1.2.3.2.1 "><p id="p1247064818407"><a name="p1247064818407"></a><a name="p1247064818407"></a>源数据库GTID状态为开启才可以进行迁移。</p>
</td>
</tr>
<tr id="row7517104874012"><th class="firstcol" valign="top" width="8.459999999999999%" id="mcps1.2.3.3.1"><p id="p6485134834018"><a name="p6485134834018"></a><a name="p6485134834018"></a><strong id="b448554810404"><a name="b448554810404"></a><a name="b448554810404"></a>告警提示及处理建议</strong></p>
</th>
<td class="cellrowborder" valign="top" width="91.53999999999999%" headers="mcps1.2.3.3.1 "><p id="p2728453337"><a name="p2728453337"></a><a name="p2728453337"></a><strong id="b3733349123219"><a name="b3733349123219"></a><a name="b3733349123219"></a>告警原因</strong>：源数据库GTID关闭，开启GTID对于迁移任务灾难恢复和目标数据库重建有可靠性和性能上的优势，建议开启GTID。</p>
<p id="p13682195863313"><a name="p13682195863313"></a><a name="p13682195863313"></a><strong id="b1997314917341"><a name="b1997314917341"></a><a name="b1997314917341"></a>处理建议</strong>：</p>
<p id="p189451887427"><a name="p189451887427"></a><a name="p189451887427"></a>通过修改数据库配置文件中如下三个参数开启GTID，然后重启数据库。</p>
<pre class="codeblock" id="codeblock1299223964210"><a name="codeblock1299223964210"></a><a name="codeblock1299223964210"></a>gtid_mode = on
log_slave_updates = true
enforce_gtid_consistency = on</pre>
</td>
</tr>
</tbody>
</table>


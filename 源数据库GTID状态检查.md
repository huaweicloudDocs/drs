# 源数据库GTID状态检查<a name="drs_11_0020"></a>

## MySQL迁移场景<a name="section629895911207"></a>

**表 1**  源数据库GTID状态检查

<a name="table1442354814017"></a>
<table><tbody><tr id="row1543984894010"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p5439144814407"><a name="p5439144814407"></a><a name="p5439144814407"></a><strong id="b943904844016"><a name="b943904844016"></a><a name="b943904844016"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p319214103234"><a name="p319214103234"></a><a name="p319214103234"></a><span class="keyword" id="keyword193922460382"><a name="keyword193922460382"></a><a name="keyword193922460382"></a>源数据库GTID状态</span>检查。</p>
</td>
</tr>
<tr id="row0454148134018"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1145414834016"><a name="p1145414834016"></a><a name="p1145414834016"></a><strong id="b154701348174013"><a name="b154701348174013"></a><a name="b154701348174013"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p1247064818407"><a name="p1247064818407"></a><a name="p1247064818407"></a>源数据库GTID状态为开启才可以进行迁移。</p>
</td>
</tr>
<tr id="row7517104874012"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p6485134834018"><a name="p6485134834018"></a><a name="p6485134834018"></a><strong id="b448554810404"><a name="b448554810404"></a><a name="b448554810404"></a>告警提示及<strong id="b14490151682817"><a name="b14490151682817"></a><a name="b14490151682817"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p1767071520417"><a name="p1767071520417"></a><a name="p1767071520417"></a><strong id="b36701158410"><a name="b36701158410"></a><a name="b36701158410"></a>告警原因</strong>：源数据库GTID关闭，开启GTID对于迁移任务灾难恢复和目标数据库重建有可靠性和性能上的优势，建议开启GTID（请注意，源数据库主备切换会导致任务失败）。</p>
<p id="p13682195863313"><a name="p13682195863313"></a><a name="p13682195863313"></a><strong id="b1997314917341"><a name="b1997314917341"></a><a name="b1997314917341"></a>处理建议</strong>：</p>
<a name="ul14588102134310"></a><a name="ul14588102134310"></a><ul id="ul14588102134310"><li>如果源数据库版本为MySQL 5.5，请忽略此告警。</li><li>如果源数据库版本为MySQL 5.6及以上版本，通过修改数据库配置文件中如下三个参数开启GTID，然后重启数据库。<pre class="codeblock" id="codeblock1299223964210"><a name="codeblock1299223964210"></a><a name="codeblock1299223964210"></a>gtid_mode = on
log_slave_updates = true
enforce_gtid_consistency = on</pre>
</li></ul>
</td>
</tr>
</tbody>
</table>


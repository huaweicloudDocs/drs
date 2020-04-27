# 源数据库参数server\_id是否符合增量迁移要求<a name="drs_11_0018"></a>

## MySQL迁移场景<a name="section8961123011172"></a>

**表 1**  源数据库参数server\_id是否符合增量迁移要求

<a name="table4980162018737"></a>
<table><tbody><tr id="row2782383618737"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p3913823218737"><a name="p3913823218737"></a><a name="p3913823218737"></a><strong id="b1669976818737"><a name="b1669976818737"></a><a name="b1669976818737"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p6629537918847"><a name="p6629537918847"></a><a name="p6629537918847"></a><span class="keyword" id="keyword621114493815"><a name="keyword621114493815"></a><a name="keyword621114493815"></a>源数据库参数server_id</span>是否符合增量迁移要求。</p>
</td>
</tr>
<tr id="row2742650018737"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p695405318737"><a name="p695405318737"></a><a name="p695405318737"></a><strong id="b6258648518737"><a name="b6258648518737"></a><a name="b6258648518737"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p4040102118352"><a name="p4040102118352"></a><a name="p4040102118352"></a>检查源数据库的server_id是否符合增量迁移要求。</p>
</td>
</tr>
<tr id="row5862944518737"><th class="firstcol" rowspan="4" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p5136462818737"><a name="p5136462818737"></a><a name="p5136462818737"></a><strong id="b5962847118737"><a name="b5962847118737"></a><a name="b5962847118737"></a>失败提示及<strong id="b14490151682817"><a name="b14490151682817"></a><a name="b14490151682817"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p177448299308"><a name="p177448299308"></a><a name="p177448299308"></a><strong id="b14119122552816"><a name="b14119122552816"></a><a name="b14119122552816"></a>失败原因</strong>：源数据库连接失败，导致该项检查无法进行。</p>
<p id="p161016291303"><a name="p161016291303"></a><a name="p161016291303"></a><strong id="b8714125723313"><a name="b8714125723313"></a><a name="b8714125723313"></a>处理建议</strong>：查看源数据连接是否成功。</p>
</td>
</tr>
<tr id="row129868449299"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p1598634418294"><a name="p1598634418294"></a><a name="p1598634418294"></a><strong id="b158541237153019"><a name="b158541237153019"></a><a name="b158541237153019"></a>失败原因</strong>：用户基本权限不足。</p>
<p id="p14314118183010"><a name="p14314118183010"></a><a name="p14314118183010"></a><strong id="b88918023410"><a name="b88918023410"></a><a name="b88918023410"></a>处理建议</strong>：查看对应数据库帐号权限是否符合迁移要求。</p>
</td>
</tr>
<tr id="row17970104713299"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p1897064718297"><a name="p1897064718297"></a><a name="p1897064718297"></a><strong id="b972103943015"><a name="b972103943015"></a><a name="b972103943015"></a>失败原因</strong>：源数据库server_id不符合增量迁移要求。</p>
<p id="p52918532305"><a name="p52918532305"></a><a name="p52918532305"></a><strong id="b1964112193417"><a name="b1964112193417"></a><a name="b1964112193417"></a>处理建议</strong>：</p>
<p id="p11886275308"><a name="p11886275308"></a><a name="p11886275308"></a>执行如下命令，修改server_id：</p>
<p id="p1485901894333"><a name="p1485901894333"></a><a name="p1485901894333"></a><strong id="b2769716794333"><a name="b2769716794333"></a><a name="b2769716794333"></a>set global server_id=n</strong></p>
<p id="p48931414153020"><a name="p48931414153020"></a><a name="p48931414153020"></a><strong id="b376778194358"><a name="b376778194358"></a><a name="b376778194358"></a>n</strong>表示源数据库的server_id，如果源数据库版本为MySQL5.6，n的取值范围在2-4294967296之间；如果源数据库版本为MySQL5.5和MySQL5.7，n的取值范围在1-4294967296之间。</p>
</td>
</tr>
<tr id="row360311618737"><td class="cellrowborder" valign="top" headers="mcps1.2.3.3.1 "><p id="p1401991693319"><a name="p1401991693319"></a><a name="p1401991693319"></a><strong id="b1679120406304"><a name="b1679120406304"></a><a name="b1679120406304"></a>失败原因</strong>：内部错误。</p>
<p id="p18751132273017"><a name="p18751132273017"></a><a name="p18751132273017"></a><strong id="b20105364349"><a name="b20105364349"></a><a name="b20105364349"></a>处理建议</strong>：请联系客服人员处理。</p>
</td>
</tr>
</tbody>
</table>


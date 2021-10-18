# 检查分片节点是否和mongos节点属于同一个集群<a name="drs_16_0105"></a>

## MongoDB数据库迁移场景<a name="section834844911539"></a>

**表 1**  检查分片节点是否和mongos节点属于同一个集群

<a name="table1286312219628"></a>
<table><tbody><tr id="row1333815319628"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p16418526191940"><a name="p16418526191940"></a><a name="p16418526191940"></a><strong id="b13549013191940"><a name="b13549013191940"></a><a name="b13549013191940"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p59157410191053"><a name="p59157410191053"></a><a name="p59157410191053"></a>检查分片节点是否和mongos节点属于同一个集群。</p>
</td>
</tr>
<tr id="row59198819628"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p12227812191940"><a name="p12227812191940"></a><a name="p12227812191940"></a><strong id="b42941445191940"><a name="b42941445191940"></a><a name="b42941445191940"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p2174934014558"><a name="p2174934014558"></a><a name="p2174934014558"></a>分片节点和mongos节点若不属于同一个集群，则会导致迁移失败。</p>
</td>
</tr>
<tr id="row5971331319628"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p31582987191940"><a name="p31582987191940"></a><a name="p31582987191940"></a><strong id="b15811431191940"><a name="b15811431191940"></a><a name="b15811431191940"></a>待确认提示及<strong id="b117671048113514"><a name="b117671048113514"></a><a name="b117671048113514"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p125951206366"><a name="p125951206366"></a><a name="p125951206366"></a><strong id="b35951920103617"><a name="b35951920103617"></a><a name="b35951920103617"></a>不通过原因：</strong>分片节点和mongos节点不是同一个集群。</p>
<p id="p12728194805510"><a name="p12728194805510"></a><a name="p12728194805510"></a><strong id="b019935955510"><a name="b019935955510"></a><a name="b019935955510"></a>处理建议：</strong>返回测试连接界面，更新正确的分片信息，确认输入的分片节点是和mongos属于同一个集群。</p>
</td>
</tr>
</tbody>
</table>


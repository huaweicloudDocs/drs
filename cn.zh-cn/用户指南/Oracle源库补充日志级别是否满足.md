# Oracle源库补充日志级别是否满足<a name="drs_15_0026"></a>

## Oracle-\>MySQL、Oracle-\>PostgreSQL、Oracle-\>TaurusDB、Oracle-\>GaussDB、Oracle-\>MRS kafka迁移、同步场景<a name="section715117526252"></a>

**表 1**  Oracle源库补充日志级别是否满足

<a name="table1615135220255"></a>
<table><tbody><tr id="row11151452172515"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p1415117521250"><a name="p1415117521250"></a><a name="p1415117521250"></a><strong id="b41511352192518"><a name="b41511352192518"></a><a name="b41511352192518"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p715105214254"><a name="p715105214254"></a><a name="p715105214254"></a>Oracle源库补充日志级别是否满足。</p>
</td>
</tr>
<tr id="row315125282518"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p19152452152513"><a name="p19152452152513"></a><a name="p19152452152513"></a><strong id="b1152752192517"><a name="b1152752192517"></a><a name="b1152752192517"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p715225211259"><a name="p715225211259"></a><a name="p715225211259"></a>Oracle源库未开启库级补充日志或级别不满足要求，会导致迁移/同步失败。</p>
</td>
</tr>
<tr id="row15152145222510"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p315225219255"><a name="p315225219255"></a><a name="p315225219255"></a><strong id="b1615212529254"><a name="b1615212529254"></a><a name="b1615212529254"></a>失败提示及<strong id="b815205211254"><a name="b815205211254"></a><a name="b815205211254"></a>处理建议</strong></strong></p>
<p id="p18152752122511"><a name="p18152752122511"></a><a name="p18152752122511"></a></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p11152145211259"><a name="p11152145211259"></a><a name="p11152145211259"></a><strong id="b151528526257"><a name="b151528526257"></a><a name="b151528526257"></a>失败原因：</strong>Oracle源库补充日志级别不满足。</p>
<p id="p176622043163112"><a name="p176622043163112"></a><a name="p176622043163112"></a><strong id="b16624433312"><a name="b16624433312"></a><a name="b16624433312"></a>处理建议：</strong>在源库中，执行以下操作中的任意一项。</p>
<a name="ul13642121773215"></a><a name="ul13642121773215"></a><ul id="ul13642121773215"><li>开启库级ALL级别的补充日志：alter database add supplemental log data (all) columns。</li><li>在ORACLE源库中开启库级主键和唯一键级别的补充日志：alter database add supplemental log data (primary key,unique) columns。</li><li>在ORACLE源库中开启最小补充日志：alter database add supplemental log data，并为每张待同步表开启表级all级别或主键和唯一键级别的补充日志：alter table TABLE_NAME add supplemental log data(all) columns。</li></ul>
</td>
</tr>
</tbody>
</table>


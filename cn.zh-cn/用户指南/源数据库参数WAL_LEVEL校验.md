# 源数据库参数WAL\_LEVEL校验<a name="drs_11_0100"></a>

## PostgreSQL迁移场景<a name="section1748856803"></a>

**表 1**  源数据库参数WAL\_LEVEL校验

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.1.1 "><p id="p01081022104711"><a name="p01081022104711"></a><a name="p01081022104711"></a>源数据库参数WAL_LEVEL校验。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>源数据库版本是PostgreSQL9.5时，参数wal_level必须是配置成hot_standby，源数据库版本是PostgreSQL9.6时，参数wal_level必须是配置成replica，同步任务wal_level必须配置成logical。否则，可能会导致同步失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>失败提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="89%" headers="mcps1.2.3.3.1 "><p id="p18705213564"><a name="p18705213564"></a><a name="p18705213564"></a><strong id="b16814162110612"><a name="b16814162110612"></a><a name="b16814162110612"></a>失败原因</strong>：源数据库参数wal_level配置错误。</p>
<p id="p10194121217610"><a name="p10194121217610"></a><a name="p10194121217610"></a><strong id="b12194131219616"><a name="b12194131219616"></a><a name="b12194131219616"></a>处理建议</strong>：建议修改配置文件postgresql.conf中的wal_level参数，重启数据库生效。</p>
</td>
</tr>
</tbody>
</table>


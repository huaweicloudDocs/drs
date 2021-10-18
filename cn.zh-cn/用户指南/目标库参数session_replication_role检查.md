# 目标库参数session\_replication\_role检查<a name="drs_03_1130"></a>

## PostgreSQL-\>PostgreSQL迁移、同步<a name="section115017217222"></a>

**表 1**  目标库参数session\_replication\_role检查

<a name="table18108192214474"></a>
<table><tbody><tr id="row19108192294711"><th class="firstcol" valign="top" width="11.06%" id="mcps1.2.3.1.1"><p id="p191087222477"><a name="p191087222477"></a><a name="p191087222477"></a><strong id="b13108162214473"><a name="b13108162214473"></a><a name="b13108162214473"></a>预检查项</strong></p>
</th>
<td class="cellrowborder" valign="top" width="88.94%" headers="mcps1.2.3.1.1 "><p id="p1546615199234"><a name="p1546615199234"></a><a name="p1546615199234"></a>目标库参数session_replication_role检查。</p>
</td>
</tr>
<tr id="row3108132254714"><th class="firstcol" valign="top" width="11.06%" id="mcps1.2.3.2.1"><p id="p1710810224473"><a name="p1710810224473"></a><a name="p1710810224473"></a><strong id="b510892211472"><a name="b510892211472"></a><a name="b510892211472"></a>描述</strong></p>
</th>
<td class="cellrowborder" valign="top" width="88.94%" headers="mcps1.2.3.2.1 "><p id="p15372705185323"><a name="p15372705185323"></a><a name="p15372705185323"></a>目标数据库参数session_replication_role建议配置为replica，否则当迁移的表具有关联的外键约束或者触发器时，可能会造成数据同步失败。</p>
</td>
</tr>
<tr id="row212432224711"><th class="firstcol" valign="top" width="11.06%" id="mcps1.2.3.3.1"><p id="p1412462211472"><a name="p1412462211472"></a><a name="p1412462211472"></a><strong id="b111246227470"><a name="b111246227470"></a><a name="b111246227470"></a>待确认提示及<strong id="b15891153114115"><a name="b15891153114115"></a><a name="b15891153114115"></a>处理建议</strong></strong></p>
</th>
<td class="cellrowborder" valign="top" width="88.94%" headers="mcps1.2.3.3.1 "><p id="p11557124313013"><a name="p11557124313013"></a><a name="p11557124313013"></a><strong id="b96922171213"><a name="b96922171213"></a><a name="b96922171213"></a>待确认原因：</strong>目标数据库参数session_replication_role未配置为replica。</p>
<p id="p355811437010"><a name="p355811437010"></a><a name="p355811437010"></a><strong id="b15111935014"><a name="b15111935014"></a><a name="b15111935014"></a>处理建议：</strong>建议将目标数据库参数session_replication_role设置为replica。自建数据库请使用superuser权限用户，执行如下命令进行修改："alter database set session_replication_role to replica;"； 华为云数据库rds，请在rds实例的参数修改页面选择session_replication_role参数修改。</p>
</td>
</tr>
</tbody>
</table>


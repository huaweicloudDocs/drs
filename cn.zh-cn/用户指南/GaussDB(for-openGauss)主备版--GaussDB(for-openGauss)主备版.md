# GaussDB\(for openGauss\)主备版-\>GaussDB\(for openGauss\)主备版<a name="drs_04_0461"></a>

## 操作要求<a name="section49716619118"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table13588832007"></a>
<table><thead align="left"><tr id="row25883321603"><th class="cellrowborder" valign="top" width="18.18%" id="mcps1.2.3.1.1"><p id="p1058973210012"><a name="p1058973210012"></a><a name="p1058973210012"></a><strong id="b18589103215010"><a name="b18589103215010"></a><a name="b18589103215010"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.82000000000001%" id="mcps1.2.3.1.2"><p id="p185891232501"><a name="p185891232501"></a><a name="p185891232501"></a><strong id="b35891332308"><a name="b35891332308"></a><a name="b35891332308"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row458912321000"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p258915321016"><a name="p258915321016"></a><a name="p258915321016"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul659016321207"></a><a name="ul659016321207"></a><ul id="ul659016321207"><li><a href="#table1321975211">表 环境要求</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>该链路不支持SSL安全连接。</li><li>一个同步任务只能对一个数据库进行数据同步，如果一个GaussDB(for openGauss)实例下有多个数据库需要同步，则需要为每个数据库创建实时同步任务。</li></ul>
</td>
</tr>
<tr id="row55917321508"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p175912325018"><a name="p175912325018"></a><a name="p175912325018"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul94850392720"></a><a name="ul94850392720"></a><ul id="ul94850392720"><li>实时同步过程中，受限于<span id="text107111244141214"><a name="text107111244141214"></a><a name="text107111244141214"></a>GaussDB(for openGauss)</span>逻辑复制功能，不支持DDL语句的同步。一般情况下，不建议同步过程中进行DDL操作。</li><li>实时同步过程中，修改源库的用户名、密码、IP和端口，可能会导致同步任务失败。</li></ul>
<a name="ul175916322017"></a><a name="ul175916322017"></a><ul id="ul175916322017"><li>源库表的主键及唯一约束必须包含分布列，否则无法成功同步表结构，需要用户手动在目标库创建表结构后重试任务。</li><li>对象名映射时，包含smallserial, serial, bigserial 这3个类型的表不支持schema映射。</li><li>列加工时，分区键不可以被过滤。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section159820671116"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table1321975211"></a>
<table><thead align="left"><tr id="row182201058117"><th class="cellrowborder" valign="top" width="18.18%" id="mcps1.2.3.1.1"><p id="p172201551013"><a name="p172201551013"></a><a name="p172201551013"></a><strong id="b1322020518116"><a name="b1322020518116"></a><a name="b1322020518116"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.82000000000001%" id="mcps1.2.3.1.2"><p id="p22204518111"><a name="p22204518111"></a><a name="p22204518111"></a><strong id="b15220455112"><a name="b15220455112"></a><a name="b15220455112"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row62211755115"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p19221351914"><a name="p19221351914"></a><a name="p19221351914"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul656452073510"></a><a name="ul656452073510"></a><ul id="ul656452073510"><li>源数据库端需要同时拥有以下权限：<a name="ul141507123018"></a><a name="ul141507123018"></a><ul id="ul141507123018"><li>库级权限：需要使用root或其他有Sysadmin角色的DATABASE用户登录postgres基库，赋予用户DATABASE的CONNECT权限以及REPLICATION权限。</li><li>SCHEMA级权限：需要使用 root、或其他有Sysadmin角色的DATABASE用户、或目标数据库的OWNER用户登入目标数据库，赋予用户SCHEMA的USAGE权限。</li><li>表级权限：需要使用 root、或其他有Sysadmin角色的DATABASE用户、或目标数据库的OWNER用户登入目标数据库 ，赋予用户SCHEMA下所有表的SELECT权限。</li></ul>
</li><li>目标数据库端必须同时拥有以下权限：<a name="ul132617565125"></a><a name="ul132617565125"></a><ul id="ul132617565125"><li>库级权限：需要使用root或其他有Sysadmin角色的DATABASE用户登录postgres基库，赋予用户DATABASE的CREATE、CONNECT权限。</li><li>SCHEMA级权限：需要使用 root、或其他有Sysadmin角色的DATABASE用户、或目标数据库的OWNER用户登入目标数据库，赋予用户SCHEMA的CREATE、USAGE权限。</li><li>表级权限：需要使用 root、或其他有Sysadmin角色的DATABASE用户、或目标数据库的OWNER用户登入目标数据库 ，赋予用户SCHEMA下所有表的SELECT，UPDATE，INSERT和DELETE权限。</li></ul>
</li></ul>
</td>
</tr>
<tr id="row22213516111"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p82221752015"><a name="p82221752015"></a><a name="p82221752015"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul76031410104519"></a><a name="ul76031410104519"></a><ul id="ul76031410104519"><li>全量同步时仅支持表数据、表结构和索引约束的同步。</li><li>增量同步时仅支持表数据的实时同步。</li><li>增量同步不支持列存表、压缩表、非日志表、临时表数据同步。</li></ul>
</td>
</tr>
<tr id="row2223955112"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p14223185617"><a name="p14223185617"></a><a name="p14223185617"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul714371816441"></a><a name="ul714371816441"></a><ul id="ul714371816441"><li><span id="text18148483176"><a name="text18148483176"></a><a name="text18148483176"></a>GaussDB(for openGauss)</span>同步的表必须有主键，如果没有主键，需要设置无主键表的复制属性为full。</li><li><span id="text7721171821317"><a name="text7721171821317"></a><a name="text7721171821317"></a>GaussDB(for openGauss)</span>源数据库日志模式(wal_level)必须为logical。</li><li>源数据库中的库名和表名不能包含：+%"&lt;&gt;'\以及非ASCII字符。</li><li>源库必须是本云<span id="text0224721141318"><a name="text0224721141318"></a><a name="text0224721141318"></a>GaussDB(for openGauss)</span>主备版实例。</li></ul>
</td>
</tr>
<tr id="row1422495219"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p16224654119"><a name="p16224654119"></a><a name="p16224654119"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="zh-cn_topic_0000001121374119_ul74299512319"></a><a name="zh-cn_topic_0000001121374119_ul74299512319"></a><ul id="zh-cn_topic_0000001121374119_ul74299512319"><li>目标库必须是本云<span id="zh-cn_topic_0000001121374119_text179311840151211"><a name="zh-cn_topic_0000001121374119_text179311840151211"></a><a name="zh-cn_topic_0000001121374119_text179311840151211"></a>GaussDB(for openGauss)</span>主备版实例。</li></ul>
</td>
</tr>
</tbody>
</table>


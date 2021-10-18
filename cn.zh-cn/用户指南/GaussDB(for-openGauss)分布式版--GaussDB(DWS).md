# GaussDB\(for openGauss\)分布式版-\>GaussDB\(DWS\)<a name="drs_11_0437"></a>

## 操作要求<a name="section1610153915412"></a>

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
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul659016321207"></a><a name="ul659016321207"></a><ul id="ul659016321207"><li><a href="#table1321975211">表 环境要求</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>不建议在数据库中使用非精确数值类型做主键，该特性影响 DRS 增量场景下对 UPDATE、DELETE语句的同步，同时也会导致内容比对不可用。</li><li>一个同步任务只能对一个数据库进行数据同步，如果一个GaussDB(for openGauss)实例下有多个数据库需要同步，则需要为每个数据库创建实时同步任务。</li><li>源库表的主键及唯一约束必须包含分布列，否则无法成功同步表结构，需要用户手动在目标库创建表结构后重试任务。</li></ul>
</td>
</tr>
<tr id="row55917321508"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p175912325018"><a name="p175912325018"></a><a name="p175912325018"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul175916322017"></a><a name="ul175916322017"></a><ul id="ul175916322017"><li>实时同步过程中，受限于<span id="text911833715375"><a name="text911833715375"></a><a name="text911833715375"></a>GaussDB(for openGauss)</span>逻辑复制功能，不支持DDL语句的同步。一般情况下，不建议同步过程中进行DDL操作。</li><li>对于同步中的数据库对象，在同步期间，目标库不能进行写入操作，否则会导致数据不一致。</li><li>实时同步过程中，修改源库的用户名、密码、IP和端口，可能会导致同步任务失败。</li><li>同步仅支持同步表数据、表结构和索引，同步前需要用户在目标库手动建表。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section165311339195419"></a>

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
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul62211451315"></a><a name="ul62211451315"></a><ul id="ul62211451315"><li>增量同步场景：<a name="ul1684015419351"></a><a name="ul1684015419351"></a><ul id="ul1684015419351"><li>源数据库帐号需要具备如下角色：<p id="p15431185611355"><a name="p15431185611355"></a><a name="p15431185611355"></a>拥有sysadmin或同时拥有replication以及表和schema的select权限。</p>
</li><li>目标数据库帐号需要具备如下角色或权限：<p id="p64261428133316"><a name="p64261428133316"></a><a name="p64261428133316"></a>具有每张表的如下权限：insert、select、update、delete、connect、create、references。</p>
</li></ul>
</li><li>全量同步场景：<a name="ul11419149113712"></a><a name="ul11419149113712"></a><ul id="ul11419149113712"><li>源数据库账户需要具备如下角色：<p id="p1981013333813"><a name="p1981013333813"></a><a name="p1981013333813"></a>拥有sysadmin或具有表和schema的select权限。</p>
</li><li>目标数据库帐号需要具备如下角色或权限：<p id="p39611126153511"><a name="p39611126153511"></a><a name="p39611126153511"></a>具有每张表的如下权限：insert、select、update、delete、connect、create、references。</p>
</li></ul>
</li></ul>
</td>
</tr>
<tr id="row22213516111"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p82221752015"><a name="p82221752015"></a><a name="p82221752015"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul12221452115"></a><a name="ul12221452115"></a><ul id="ul12221452115"><li>全量同步时仅支持表数据、表结构和索引约束的同步。</li><li>增量同步时仅支持表数据的实时同步。</li><li>增量同步不支持列存表、压缩表、非日志表、临时表数据同步。</li><li>不支持无主键表的同步。</li></ul>
</td>
</tr>
<tr id="row2223955112"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p14223185617"><a name="p14223185617"></a><a name="p14223185617"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul714371816441"></a><a name="ul714371816441"></a><ul id="ul714371816441"><li><span id="text7721171821317"><a name="text7721171821317"></a><a name="text7721171821317"></a>GaussDB(for openGauss)</span>源数据库日志模式(wal_level)必须为logical。</li><li>源数据库中的库名和表名不能包含：+%"&lt;&gt;'\以及非ASCII字符。</li><li>源库必须是本云<span id="text0224721141318"><a name="text0224721141318"></a><a name="text0224721141318"></a>GaussDB(for openGauss)</span>分布式版实例。</li></ul>
</td>
</tr>
<tr id="row1422495219"><td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.3.1.1 "><p id="p16224654119"><a name="p16224654119"></a><a name="p16224654119"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.82000000000001%" headers="mcps1.2.3.1.2 "><a name="ul1422465312"></a><a name="ul1422465312"></a><ul id="ul1422465312"><li>增量同步时必须先在目标实例中手动创建SCHEMA和表。</li><li>增量同步的表要禁用外键，因为DRS并行回放会使得不同表之间的写入顺序和源库不一致，可能会触发外键约束限制，造成同步失败。</li></ul>
</td>
</tr>
</tbody>
</table>


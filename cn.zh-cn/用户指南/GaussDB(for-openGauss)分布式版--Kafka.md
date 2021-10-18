# GaussDB\(for openGauss\)分布式版-\>Kafka<a name="drs_11_0454"></a>

## 操作要求<a name="section1610153915412"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table176671194291"></a>
<table><thead align="left"><tr id="row866817932916"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p1766810912299"><a name="p1766810912299"></a><a name="p1766810912299"></a><strong id="b866816932911"><a name="b866816932911"></a><a name="b866816932911"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p7668129102914"><a name="p7668129102914"></a><a name="p7668129102914"></a><strong id="b56683915291"><a name="b56683915291"></a><a name="b56683915291"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row11668199294"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p9668991296"><a name="p9668991296"></a><a name="p9668991296"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul166688942920"></a><a name="ul166688942920"></a><ul id="ul166688942920"><li><a href="#table156691396290">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>创建同步任务时，不允许将目标库设为只读。</li><li>数据类型不兼容时，可能引起同步失败。</li><li>一个同步任务只能对一个数据库进行数据同步，如果一个GaussDB(for openGauss)实例下有多个数据库需要同步，则需要为每个数据库创建实时同步任务。</li></ul>
</td>
</tr>
<tr id="row266910919293"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p866918932915"><a name="p866918932915"></a><a name="p866918932915"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul175916322017"></a><a name="ul175916322017"></a><ul id="ul175916322017"><li>实时同步过程中，受限于<span id="text911833715375"><a name="text911833715375"></a><a name="text911833715375"></a>GaussDB(for openGauss)</span>逻辑复制功能，不支持DDL语句的同步。一般情况下，不建议同步过程中进行DDL操作。</li></ul>
<a name="ul1366959112914"></a><a name="ul1366959112914"></a><ul id="ul1366959112914"><li>实时同步过程中，如果修改了源库的用户名、密码，会导致同步任务失败，需要在数据复制服务控制台将上述信息重新修改正确，然后重试任务可继续进行实时同步。一般情况下不建议在同步过程中修改上述信息。</li><li>实时同步过程中，如果修改了源库端口，会导致同步任务失败。针对该情况，系统自动更新为正确的端口，重试任务后即可进行同步。一般情况下不建议在同步过程中修改端口。</li><li>实时同步过程中，对于因修改IP地址导致同步任务失败的情况，系统自动更新为正确的IP地址，需要重试任务可继续进行同步。一般情况下，不建议修改IP地址。</li><li>选择表级对象迁移时，同步过程中不建议对表进行重命名操作。</li><li>该链路不支持SSL安全连接。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section165311339195419"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table156691396290"></a>
<table><thead align="left"><tr id="row206693912292"><th class="cellrowborder" valign="top" width="18.29%" id="mcps1.2.3.1.1"><p id="p56691994299"><a name="p56691994299"></a><a name="p56691994299"></a><strong id="b196695912912"><a name="b196695912912"></a><a name="b196695912912"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.71000000000001%" id="mcps1.2.3.1.2"><p id="p567014932912"><a name="p567014932912"></a><a name="p567014932912"></a><strong id="b18670693293"><a name="b18670693293"></a><a name="b18670693293"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row16701396299"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p66704952917"><a name="p66704952917"></a><a name="p66704952917"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul5670398296"></a><a name="ul5670398296"></a><ul id="ul5670398296"><li>源数据库帐户需要具备如下权限：拥有sysadmin或同时拥有replication权限。</li></ul>
</td>
</tr>
<tr id="row1967059102918"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p767029132911"><a name="p767029132911"></a><a name="p767029132911"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul12221452115"></a><a name="ul12221452115"></a><ul id="ul12221452115"><li>增量同步时仅支持表数据的实时同步。</li><li>同步不支持列存表、压缩表、非日志表、临时表数据同步。</li><li>增量同步不支持无主键且无主键表的复制属性不为full的同步。</li></ul>
</td>
</tr>
<tr id="row196701498297"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p36705913294"><a name="p36705913294"></a><a name="p36705913294"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul714371816441"></a><a name="ul714371816441"></a><ul id="ul714371816441"><li><span id="text7721171821317"><a name="text7721171821317"></a><a name="text7721171821317"></a>GaussDB(for openGauss)</span>源数据库日志模式(wal_level)必须为logical。</li><li>源数据库中的库名和表名不能包含：+%"&lt;&gt;'\以及非ASCII字符。</li><li>源库必须是本云<span id="text0224721141318"><a name="text0224721141318"></a><a name="text0224721141318"></a>GaussDB(for openGauss)</span>分布式版实例。</li></ul>
</td>
</tr>
<tr id="row1167118916290"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p1467189102915"><a name="p1467189102915"></a><a name="p1467189102915"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul02047619207"></a><a name="ul02047619207"></a><ul id="ul02047619207"><li>消费时 isolation.level 参数为read_committed。</li><li>目标库为普通Kafka。</li></ul>
</td>
</tr>
</tbody>
</table>


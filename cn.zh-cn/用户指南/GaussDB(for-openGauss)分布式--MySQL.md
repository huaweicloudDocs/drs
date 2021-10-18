# GaussDB\(for openGauss\)分布式-\>MySQL<a name="drs_04_0121"></a>

## 使用技巧（需要人为配合）<a name="section449714073815"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1691943218231)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   全量同步会对源数据库增加50MB/s的查询压力，以及2\~4个核的CPU压力。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section1691943218231"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table6180053181813"></a>
<table><thead align="left"><tr id="row14181125318189"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p3181105341816"><a name="p3181105341816"></a><a name="p3181105341816"></a><strong id="b7181105311816"><a name="b7181105311816"></a><a name="b7181105311816"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p171817536189"><a name="p171817536189"></a><a name="p171817536189"></a><strong id="b018155316182"><a name="b018155316182"></a><a name="b018155316182"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row41811653191812"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p20181155321812"><a name="p20181155321812"></a><a name="p20181155321812"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul01811534183"></a><a name="ul01811534183"></a><ul id="ul01811534183"><li><a href="#table176392213198">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li><li>一个同步任务只能对一个数据库进行数据同步，如果一个GaussDB(for openGauss)实例下有多个数据库需要同步，则需要为每个数据库创建实时同步任务。</li></ul>
</td>
</tr>
<tr id="row191815531186"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p018145341815"><a name="p018145341815"></a><a name="p018145341815"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul5181135314189"></a><a name="ul5181135314189"></a><ul id="ul5181135314189"><li><span id="text1818117533188"><a name="text1818117533188"></a><a name="text1818117533188"></a>实时同步</span>过程中，如果修改了源库的用户名、密码，连接断开后会导致同步任务失败，需要在数据复制服务控制台将上述信息重新修改正确，然后重试任务可继续进行<span id="text018114533187"><a name="text018114533187"></a><a name="text018114533187"></a>实时同步</span>。一般情况下不建议在同步过程中修改上述信息。</li><li><span id="text10182165316181"><a name="text10182165316181"></a><a name="text10182165316181"></a>实时同步</span>过程中，如果修改了源库端口，会导致同步任务失败。一般情况下不建议在同步过程中修改端口。</li><li><span id="text1182453131813"><a name="text1182453131813"></a><a name="text1182453131813"></a>实时同步</span>过程中，对于因修改IP地址导致同步任务失败的情况。一般情况下，不建议修改IP地址。</li><li><span id="text18182353151815"><a name="text18182353151815"></a><a name="text18182353151815"></a>实时同步</span>过程中，受限于openGauss逻辑复制功能，不支持DDL语句的同步。一般情况下，不建议同步过程中进行DDL操作。</li><li><span id="text8182753171812"><a name="text8182753171812"></a><a name="text8182753171812"></a>实时同步</span>过程中，受限于openGauss逻辑复制功能，不支持列存表、压缩表、非日志表数据同步。</li><li><span id="text1182175331811"><a name="text1182175331811"></a><a name="text1182175331811"></a>实时同步</span>过程中，不保证分布式事务的一致性。</li><li>表结构信息在源库中保存为大写，在同步时，如果目标库表名称与源库大小写不一致，需要手动添加对象名映射。</li><li>该链路不支持SSL安全连接。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section86695405239"></a>

实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

**表 2**  环境要求

<a name="table176392213198"></a>
<table><thead align="left"><tr id="row463917213198"><th class="cellrowborder" valign="top" width="18.29%" id="mcps1.2.3.1.1"><p id="p17639192191919"><a name="p17639192191919"></a><a name="p17639192191919"></a><strong id="b16639122161912"><a name="b16639122161912"></a><a name="b16639122161912"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.71000000000001%" id="mcps1.2.3.1.2"><p id="p763910261911"><a name="p763910261911"></a><a name="p763910261911"></a><strong id="b363982141911"><a name="b363982141911"></a><a name="b363982141911"></a>使用限制</strong>（DRS自动检查）</p>
</th>
</tr>
</thead>
<tbody><tr id="row1163915211191"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p1263962101910"><a name="p1263962101910"></a><a name="p1263962101910"></a>数据库权限设置</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul176394231910"></a><a name="ul176394231910"></a><ul id="ul176394231910"><li>源数据库帐户需要具备如下角色：replication或sysadmin。</li></ul>
</td>
</tr>
<tr id="row1663922161912"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p1063912161912"><a name="p1063912161912"></a><a name="p1063912161912"></a>同步对象约束</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul163922161919"></a><a name="ul163922161919"></a><ul id="ul163922161919"><li>仅支持表数据的同步。</li></ul>
<a name="ul36391328199"></a><a name="ul36391328199"></a><ul id="ul36391328199"><li>不支持列存表、压缩表、非日志表、临时表数据同步。</li><li>不支持DDL的同步。</li><li>不支持无主键表的同步。</li><li>支持的数据类型有INTEGER、BIGINT、SMALLINT、TINYINT、SERIAL、SMALLSERIAL、BIGSERIAL、FLOAT、DOUBLEPRECISION、DATE、TIME WITHOUT TIME ZONE、TIMESTAMP WITHOUT TIME ZONE、CHAR(n)、VARCHAR(n)、TEXT。</li></ul>
</td>
</tr>
<tr id="row1464013201916"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p1764072141913"><a name="p1764072141913"></a><a name="p1764072141913"></a>源数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul464015281918"></a><a name="ul464015281918"></a><ul id="ul464015281918"><li><span id="text464013241918"><a name="text464013241918"></a><a name="text464013241918"></a>GaussDB(for openGauss)</span>源数据库日志模式(wal_level)必须为logical。</li><li>源数据库中的库名不能包含：+%"&lt;&gt;'\以及非ASCII字符。</li><li>源数据库中的表名不能包含：+%"&lt;&gt;'\以及非ASCII字符。</li></ul>
</td>
</tr>
<tr id="row1464016216192"><td class="cellrowborder" valign="top" width="18.29%" headers="mcps1.2.3.1.1 "><p id="p86405201918"><a name="p86405201918"></a><a name="p86405201918"></a>目标数据库要求</p>
</td>
<td class="cellrowborder" valign="top" width="81.71000000000001%" headers="mcps1.2.3.1.2 "><a name="ul464019281914"></a><a name="ul464019281914"></a><ul id="ul464019281914"><li>目标库为自建MySQL数据库。</li><li>同步前，需要在目标库提前创建表。</li><li>目标中间件帐户需要具备以下基本权限：CREATE、DROP、ALTER、 INDEX、 INSERT、DELETE、 UPDATE、 SELECT， 同时必须具备扩展权限、全表Select权限。</li></ul>
</td>
</tr>
</tbody>
</table>


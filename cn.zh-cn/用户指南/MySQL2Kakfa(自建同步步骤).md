# MySQL-\>Kafka<a name="drs_04_0128"></a>

## 使用技巧（需要人为配合）<a name="section98341051155812"></a>

推荐**提前2-3天**启动任务，并配合如下使用技巧和[操作要求](#section1691943218231)，以确保任务稳定运行。

-   基于以下原因，建议您结合定时启动功能，选择业务低峰期开始运行同步任务。
    -   同步无主键表时，为了确保数据一致性，会存在3s以内的单表级锁定。
    -   正在同步的数据被其他事务长时间锁死，可能导致读数据超时。
    -   由于MySQL固有特点限制，CPU资源紧张时，存储引擎为Tokudb的表，读取速度可能下降至10%。

-   建议您结合数据对比的“稍后启动“功能，选择业务低峰期进行数据对比，以便得到更为具有参考性的对比结果。由于同步具有轻微的时差，在数据持续操作过程中进行对比任务，可能会出现少量数据不一致对比结果，从而失去参考意义。

## 操作要求<a name="section1691943218231"></a>

针对一些无法预知或人为因素及环境突变导致同步失败的情况，数据复制服务提供以下常见的操作限制，供您在同步过程中参考。

**表 1**  操作要求

<a name="table1911195918117"></a>
<table><thead align="left"><tr id="row131111359911"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p811113597115"><a name="p811113597115"></a><a name="p811113597115"></a><strong id="b511115591113"><a name="b511115591113"></a><a name="b511115591113"></a>类型名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p1111259314"><a name="p1111259314"></a><a name="p1111259314"></a><strong id="b1911165912112"><a name="b1911165912112"></a><a name="b1911165912112"></a>操作限制</strong>（需要人为配合）</p>
</th>
</tr>
</thead>
<tbody><tr id="row20112185916111"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p9112125917117"><a name="p9112125917117"></a><a name="p9112125917117"></a>注意事项</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul511205912116"></a><a name="ul511205912116"></a><ul id="ul511205912116"><li><a href="#table73311712526">表2</a>中的环境要求均不允许在同步过程中修改，直至同步结束。</li><li>相互关联的数据对象要确保同时同步，避免因关联对象缺失，导致同步失败。常见的关联关系：视图引用表、视图引用视图、存储过程/函数/触发器引用视图/表、主外键关联表等。</li><li>不支持外键级联操作。</li><li>若专属计算集群不支持4vCPU/8G或以上规格实例，则无法创建同步任务。</li></ul>
</td>
</tr>
<tr id="row11121159215"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1011265917113"><a name="p1011265917113"></a><a name="p1011265917113"></a>操作须知</p>
</td>
<td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul31121859818"></a><a name="ul31121859818"></a><ul id="ul31121859818"><li>同步程中，不允许删除和修改源库的用户名、密码、权限，或修改目标数据库的端口号。</li><li>不支持强制清理binlog，否则会导致同步任务失败。</li><li>当在同步过程中，对MyISAM表执行修改操作时，可能造成数据不一致。</li><li>选择表级对象同步时，同步过程中不建议对表进行重命名操作。</li></ul>
</td>
</tr>
</tbody>
</table>

## 环境要求<a name="section86695405239"></a>

-   实时同步对环境有一些特定的要求，请确保环境配置满足以下条件。该类型的要求系统会自动检查，并给出处理建议。

    **表 2**  环境要求

    <a name="table73311712526"></a>
    <table><thead align="left"><tr id="row533116125210"><th class="cellrowborder" valign="top" width="18.32%" id="mcps1.2.3.1.1"><p id="p0331112323"><a name="p0331112323"></a><a name="p0331112323"></a><strong id="b1333141217210"><a name="b1333141217210"></a><a name="b1333141217210"></a>类型名称</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="81.67999999999999%" id="mcps1.2.3.1.2"><p id="p17331312122"><a name="p17331312122"></a><a name="p17331312122"></a><strong id="b63319128213"><a name="b63319128213"></a><a name="b63319128213"></a>使用限制</strong>（DRS自动检查）</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row93311112726"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p9332012228"><a name="p9332012228"></a><a name="p9332012228"></a>数据库权限设置</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul103328121023"></a><a name="ul103328121023"></a><ul id="ul103328121023"><li>源数据库帐户需要具备如下权限：SELECT、SHOW VIEW、EVENT、LOCK TABLES、REPLICATION SLAVE、REPLICATION CLIENT、RELOAD。</li></ul>
    </td>
    </tr>
    <tr id="row16332111215216"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p333219121325"><a name="p333219121325"></a><a name="p333219121325"></a>同步对象约束</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul033231216210"></a><a name="ul033231216210"></a><ul id="ul033231216210"><li>支持表数据的同步。</li></ul>
    <a name="ul14332121219214"></a><a name="ul14332121219214"></a><ul id="ul14332121219214"><li>不支持非MyISAM和非InnoDB表的同步。</li></ul>
    </td>
    </tr>
    <tr id="row533211212220"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p1933216125211"><a name="p1933216125211"></a><a name="p1933216125211"></a>源数据库要求</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><a name="ul1133261218215"></a><a name="ul1133261218215"></a><ul id="ul1133261218215"><li>MySQL源数据库的binlog日志必须打开，且binlog日志格式必须为Row格式。</li><li>在磁盘空间允许的情况下，建议源数据库binlog保存时间越长越好，建议为3天。</li><li>源数据库expire_logs_days参数值为0，可能会导致同步失败。</li><li>增量同步时，必须设置MySQL源数据库的server_id。如果源数据库版本小于或等于MySQL5.6，server_id的取值范围在2－4294967296之间；如果源数据库版本等于MySQL5.7，server_id的取值范围在1－4294967296之间。</li><li>源数据库中的库、表名不能包含：'&lt;`&gt;/\以及非ASCII字符。</li></ul>
    </td>
    </tr>
    <tr id="row433371219214"><td class="cellrowborder" valign="top" width="18.32%" headers="mcps1.2.3.1.1 "><p id="p93333121123"><a name="p93333121123"></a><a name="p93333121123"></a>目标数据库要求</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.67999999999999%" headers="mcps1.2.3.1.2 "><p id="p183331512624"><a name="p183331512624"></a><a name="p183331512624"></a>消费时 isolation.level 参数为read_committed。</p>
    </td>
    </tr>
    </tbody>
    </table>



# 场景一：创建RDS全量备份迁移任务<a name="drs_02_0010"></a>

介绍RDS全量备份场景下的备份迁移。您可以通过本云上Microsoft SQL Server数据库实例的全量备份，对已有的Microsoft SQL Server实例进行备份数据迁移。

本小节主要介绍通过数据复制服务管理控制台创建备份迁移任务的配置流程。

## 前提条件<a name="section2097363117427"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   满足备份移支持的数据库类型，参见[备份迁移](https://support.huaweicloud.com/productdesc-drs/drs_01_0303.html)。
-   满足备份迁移的限制条件，参见[使用须知](使用须知.md)。

## 操作步骤<a name="zh-cn_topic_0060142340_section52562732171832"></a>

1.  在“备份迁移管理”页面，单击“创建迁移任务”。
2.  在“选定备份”页面输入任务名称和描述，填选备份文件信息，单击“下一步”。

    **图 1**  任务信息<a name="fig54436859105750"></a>  
    ![](figures/任务信息.png "任务信息")

    **表 1**  任务信息

    <a name="table968763915219"></a>
    <table><thead align="left"><tr id="row106877396213"><th class="cellrowborder" valign="top" width="19%" id="mcps1.2.3.1.1"><p id="p14687203982110"><a name="p14687203982110"></a><a name="p14687203982110"></a><strong id="b4140457172110"><a name="b4140457172110"></a><a name="b4140457172110"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="81%" id="mcps1.2.3.1.2"><p id="p16687163914215"><a name="p16687163914215"></a><a name="p16687163914215"></a><strong id="b1887395952116"><a name="b1887395952116"></a><a name="b1887395952116"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row4687103922113"><td class="cellrowborder" valign="top" width="19%" headers="mcps1.2.3.1.1 "><p id="p168723914216"><a name="p168723914216"></a><a name="p168723914216"></a>任务名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="81%" headers="mcps1.2.3.1.2 "><p id="p156871239182110"><a name="p156871239182110"></a><a name="p156871239182110"></a>任务名称在4-50位之间，必须以字母开头，不区分大小写，可以包含字母、数字、中划线或下划线，不能包含其他特殊字符。</p>
    </td>
    </tr>
    <tr id="row1068718396218"><td class="cellrowborder" valign="top" width="19%" headers="mcps1.2.3.1.1 "><p id="p5687123910215"><a name="p5687123910215"></a><a name="p5687123910215"></a>描述</p>
    </td>
    <td class="cellrowborder" valign="top" width="81%" headers="mcps1.2.3.1.2 "><p id="p2687103912110"><a name="p2687103912110"></a><a name="p2687103912110"></a>描述不能超过256位，且不能包含! = &lt; &gt; &amp; ' " \ 特殊字符。</p>
    </td>
    </tr>
    </tbody>
    </table>

    **图 2**  备份文件信息<a name="fig8169113617012"></a>  
    ![](figures/备份文件信息.png "备份文件信息")

    **表 2**  备份文件信息

    <a name="table13414113982219"></a>
    <table><thead align="left"><tr id="row194146391228"><th class="cellrowborder" valign="top" width="19%" id="mcps1.2.3.1.1"><p id="p1414203932212"><a name="p1414203932212"></a><a name="p1414203932212"></a><strong id="b1061616292310"><a name="b1061616292310"></a><a name="b1061616292310"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="81%" id="mcps1.2.3.1.2"><p id="p18414183915220"><a name="p18414183915220"></a><a name="p18414183915220"></a><strong id="b1564813213237"><a name="b1564813213237"></a><a name="b1564813213237"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row8414153942215"><td class="cellrowborder" valign="top" width="19%" headers="mcps1.2.3.1.1 "><p id="p341463913229"><a name="p341463913229"></a><a name="p341463913229"></a>数据库类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="81%" headers="mcps1.2.3.1.2 "><p id="p5414183962216"><a name="p5414183962216"></a><a name="p5414183962216"></a>选择Microsoft SQL Server数据库引擎。</p>
    </td>
    </tr>
    <tr id="row16414103913221"><td class="cellrowborder" valign="top" width="19%" headers="mcps1.2.3.1.1 "><p id="p241443913229"><a name="p241443913229"></a><a name="p241443913229"></a>备份文件来源</p>
    </td>
    <td class="cellrowborder" valign="top" width="81%" headers="mcps1.2.3.1.2 "><p id="p16414839102213"><a name="p16414839102213"></a><a name="p16414839102213"></a>选择RDS全量备份。</p>
    <div class="note" id="note183691511162419"><a name="note183691511162419"></a><a name="note183691511162419"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p336918118249"><a name="p336918118249"></a><a name="p336918118249"></a>请选择状态为“备份完成”的RDS备份文件。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row02331340195110"><td class="cellrowborder" valign="top" width="19%" headers="mcps1.2.3.1.1 "><p id="p172341340155118"><a name="p172341340155118"></a><a name="p172341340155118"></a>企业项目</p>
    </td>
    <td class="cellrowborder" valign="top" width="81%" headers="mcps1.2.3.1.2 "><p id="p1838735920597"><a name="p1838735920597"></a><a name="p1838735920597"></a>对于已成功关联企业项目的用户，仅需在“企业项目”下拉框中选择目标项目。</p>
    <p id="p3387259195913"><a name="p3387259195913"></a><a name="p3387259195913"></a>如果需要自定义企业项目，请前往项目管理服务进行创建。关于如何创建项目，详见《项目管理用户指南》。</p>
    </td>
    </tr>
    <tr id="row65443568514"><td class="cellrowborder" valign="top" width="19%" headers="mcps1.2.3.1.1 "><p id="p1611410526"><a name="p1611410526"></a><a name="p1611410526"></a>标签</p>
    </td>
    <td class="cellrowborder" valign="top" width="81%" headers="mcps1.2.3.1.2 "><p id="p27631913145915"><a name="p27631913145915"></a><a name="p27631913145915"></a>可选配置，对迁移任务的标识。使用标签可方便管理您的迁移任务。每个任务最多支持10个标签配额。</p>
    <p id="p142164113522"><a name="p142164113522"></a><a name="p142164113522"></a>任务创建成功后，您可以单击实例名称，在<span class="uicontrol" id="uicontrol620412527"><a name="uicontrol620412527"></a><a name="uicontrol620412527"></a>“标签”</span>页签下查看对应标签。关于标签的详细操作，请参见<a href="https://support.huaweicloud.com/usermanual-drs/drs_backup_tag.html" target="_blank" rel="noopener noreferrer">标签管理</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“选定目标”页面，填选数据库信息，单击“下一步”。

    **图 3**  数据库信息<a name="fig17927191919218"></a>  
    ![](figures/数据库信息.png "数据库信息")

    **表 3**  数据库信息

    <a name="table132912537253"></a>
    <table><thead align="left"><tr id="row4291105332513"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.3.1.1"><p id="p10291185332515"><a name="p10291185332515"></a><a name="p10291185332515"></a><strong id="b6150191242614"><a name="b6150191242614"></a><a name="b6150191242614"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="80%" id="mcps1.2.3.1.2"><p id="p929120535256"><a name="p929120535256"></a><a name="p929120535256"></a><strong id="b8150201218262"><a name="b8150201218262"></a><a name="b8150201218262"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row92911853122519"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p929175322517"><a name="p929175322517"></a><a name="p929175322517"></a>目标RDS实例名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p136051966296"><a name="p136051966296"></a><a name="p136051966296"></a>选择目标RDS实例。若没有合适的目标数据库实例，请先创建目标数据库实例，具体操作及注意事项参见《关系型数据库快速入门》中“SQL Server快速入门”下的“<a href="https://support.huaweicloud.com/qs-rds/rds_04_0061.html" target="_blank" rel="noopener noreferrer">购买实例</a>”章节。</p>
    </td>
    </tr>
    <tr id="row13291195322519"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p1329135302517"><a name="p1329135302517"></a><a name="p1329135302517"></a>待还原数据库名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p1763044353"><a name="p1763044353"></a><a name="p1763044353"></a>选中目标RDS实例后，自动展示该实例的所有待还原数据库，可根据需要选择待还原的数据库，并且支持重命名。</p>
    <a name="ul1128414535510"></a><a name="ul1128414535510"></a><ul id="ul1128414535510"><li>待还原数据库名称：待还原数据库的原名称。</li><li>数据库新名称：区分大小写，长度在1~64个字符之间，可以包含字母，数字、中划线和下划线，不能包含其他特殊字符。不设置，则使用原数据库名称备份恢复，设置后，使用新名称备份恢复。</li></ul>
    <div class="note" id="note8261831202420"><a name="note8261831202420"></a><a name="note8261831202420"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p20877236161611"><a name="p20877236161611"></a><a name="p20877236161611"></a>待还原数据库支持重命名，最大配额为100个。</p>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

4.  在“信息确认”页面核对配置详情后，勾选协议，单击“下一步”。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >SQL Server自身的工作原理是备份文件恢复到新的数据库后，非聚集索引表的索引信息将会失效需要立即重建。如果源数据库里存在大量非聚集索引表，备份迁移后请在目标库进行索引重建，以避免数据库未来使用中性能出现重大下降。同时备份文件里仅保存数据库级信息，在SQL Server实例中还有一些配置需要主动识别并手工完成迁移，如login，权限，DBlink，job等，如果源数据库包含这部分配置，请参考[《最佳实践》](https://support.huaweicloud.com/bestpractice-drs/drs_04_0008.html)进行迁移补充工作。

5.  在“备份迁移管理“页面任务列表中，观察对应的恢复任务的状态为“恢复中”，恢复成功后，任务状态显示“成功“。


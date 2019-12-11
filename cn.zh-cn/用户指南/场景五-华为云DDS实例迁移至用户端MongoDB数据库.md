# 场景五：华为云DDS实例迁移至用户端MongoDB数据库<a name="drs_03_0104"></a>

数据复制服务提供出云的功能，可以将本云上的数据库迁移至用户端数据库，方便进行数据回流处理。

本章节将以公网网络方式为示例，介绍DDS实例迁移至用户端MongoDB数据库的任务配置流程，其他网络方式的配置流程类似。

目前数据复制服务支持每个用户最多可创建5个在线迁移任务。

## 前提条件<a name="section13357255114314"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   参见[在线迁移](https://support.huaweicloud.com/productdesc-drs/drs_01_0301.html)。
-   参见[使用须知](https://support.huaweicloud.com/qs-drs/drs_online_migration.html)。

## 操作步骤<a name="section11254113313612"></a>

1.  在“在线迁移管理“页面，单击“创建迁移任务“，进入创建迁移任务页面。
2.  在“迁移实例”页面，填选任务名称、通知收件人信息、描述、迁移实例信息，单击“下一步”。

    **图 1**  迁移任务信息<a name="fig1473012110109"></a>  
    ![](figures/迁移任务信息-42.png "迁移任务信息-42")

    **表 1**  任务和描述

    <a name="table8146244204420"></a>
    <table><thead align="left"><tr id="row55731924204420"><th class="cellrowborder" valign="top" width="18.42%" id="mcps1.2.3.1.1"><p id="p17991967204420"><a name="p17991967204420"></a><a name="p17991967204420"></a><strong id="b1611223511352"><a name="b1611223511352"></a><a name="b1611223511352"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="81.58%" id="mcps1.2.3.1.2"><p id="p48063227204420"><a name="p48063227204420"></a><a name="p48063227204420"></a><strong id="b3002268111352"><a name="b3002268111352"></a><a name="b3002268111352"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row807311204420"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p65392260204420"><a name="p65392260204420"></a><a name="p65392260204420"></a>任务名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p62281730204420"><a name="p62281730204420"></a><a name="p62281730204420"></a>任务名称在4位到64位之间，必须以字母开头，不区分大小写，可以包含字母、数字、中划线或下划线，不能包含其他的特殊字符。</p>
    </td>
    </tr>
    <tr id="row1080215433911"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p158027493912"><a name="p158027493912"></a><a name="p158027493912"></a>任务异常通知设置</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p38891258184013"><a name="p38891258184013"></a><a name="p38891258184013"></a>该项为可选参数，开启之后，需要填写手机号码或者邮箱作为指定收件人。当迁移任务状态异常时，系统将发送通知给指定收件人。</p>
    <div class="note" id="note158461433104913"><a name="note158461433104913"></a><a name="note158461433104913"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p138461333114917"><a name="p138461333114917"></a><a name="p138461333114917"></a>收到确认短信或邮件之后，需要在48小时内处理，否则该功能订阅无效。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row157731032102814"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p1677373232818"><a name="p1677373232818"></a><a name="p1677373232818"></a>时延阈值</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p6681185532914"><a name="p6681185532914"></a><a name="p6681185532914"></a>在增量迁移阶段，源数据库和目标数据库之间的同步有时会存在一个时间差，称为时延，单位为秒。</p>
    <p id="p75251915133018"><a name="p75251915133018"></a><a name="p75251915133018"></a>时延阈值设置是指时延超过一定的值后（时间阈值范围为1—3600s），DRS可以发送告警通知给指定收件人。告警通知将在时延稳定超过设定的阈值6min后发送，避免出现由于时延波动反复发送告警通知的情况。</p>
    <div class="note" id="note47298209309"><a name="note47298209309"></a><a name="note47298209309"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul79215422094"></a><a name="ul79215422094"></a><ul id="ul79215422094"><li>首次进入增量迁移阶段，会有较多数据等待同步，存在较大的时延，属于正常情况，不在此功能的监控范围之内。</li><li>设置时间阈值之前，需要填写收件人手机号或邮箱。</li></ul>
    </div></div>
    </td>
    </tr>
    <tr id="row23664659204420"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p37789232204420"><a name="p37789232204420"></a><a name="p37789232204420"></a>描述</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p41028970204420"><a name="p41028970204420"></a><a name="p41028970204420"></a>描述不能超过256位，且不能包含!=&lt;&gt;&amp;'"特殊字符。</p>
    </td>
    </tr>
    </tbody>
    </table>

    **图 2**  迁移实例信息<a name="fig6487192516156"></a>  
    ![](figures/迁移实例信息-43.png "迁移实例信息-43")

    **表 2**  迁移实例信息

    <a name="table54580728204436"></a>
    <table><thead align="left"><tr id="row39932329204436"><th class="cellrowborder" valign="top" width="23.87%" id="mcps1.2.3.1.1"><p id="p13293221204436"><a name="p13293221204436"></a><a name="p13293221204436"></a><strong id="b2587841611355"><a name="b2587841611355"></a><a name="b2587841611355"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.13%" id="mcps1.2.3.1.2"><p id="p3009113204436"><a name="p3009113204436"></a><a name="p3009113204436"></a><strong id="b1577696211355"><a name="b1577696211355"></a><a name="b1577696211355"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row145601338145018"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p195601038135019"><a name="p195601038135019"></a><a name="p195601038135019"></a>数据流动方向</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1856013381509"><a name="p1856013381509"></a><a name="p1856013381509"></a>选择出云。</p>
    <p id="p74561120155119"><a name="p74561120155119"></a><a name="p74561120155119"></a>出云指源端数据库为本云RDS或者DDS的场景，数据复制服务要求源数据库或者目标数据库中至少有一方为本云RDS或者DDS。</p>
    </td>
    </tr>
    <tr id="row0414184610580"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1414046115813"><a name="p1414046115813"></a><a name="p1414046115813"></a>源数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p168249357197"><a name="p168249357197"></a><a name="p168249357197"></a>选择DDS。</p>
    </td>
    </tr>
    <tr id="row42411630204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p12790028204436"><a name="p12790028204436"></a><a name="p12790028204436"></a>目标数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1969552512018"><a name="p1969552512018"></a><a name="p1969552512018"></a>选择MongoDB。</p>
    </td>
    </tr>
    <tr id="row62907306204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p62327044204436"><a name="p62327044204436"></a><a name="p62327044204436"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1348173083518"><a name="p1348173083518"></a><a name="p1348173083518"></a>目前支持公网网络、VPC网络和VPN、专线网络类型，您可以根据具体的业务场景进行设置，此处场景以公网网络为示例。</p>
    <a name="ul19818056621"></a><a name="ul19818056621"></a><ul id="ul19818056621"><li>VPC网络：适合云上数据库之间的迁移。</li><li>VPN、专线网络：适合通过VPN、专线网络，实现其他云下自建数据库与云上数据库迁移、或云上跨Region的数据库之间的迁移。</li><li>公网网络：适合将其他云下或其他平台的数据库迁移到目标数据库。</li></ul>
    </td>
    </tr>
    <tr id="row658644204515"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p53350183204515"><a name="p53350183204515"></a><a name="p53350183204515"></a>源数据库实例</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p26397538204515"><a name="p26397538204515"></a><a name="p26397538204515"></a>用户需要迁移的DDS实例。</p>
    </td>
    </tr>
    <tr id="row18478341367"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p128192616518"><a name="p128192616518"></a><a name="p128192616518"></a>迁移模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><a name="ul171919713019"></a><a name="ul171919713019"></a><ul id="ul171919713019"><li>全量：该模式为数据库一次性迁移，适用于可中断业务的数据库迁移场景，全量迁移将非系统数据库的全部数据库对象和数据一次性迁移至目标端数据库，包括：集合、索引等。<div class="note" id="note1989394717302"><a name="note1989394717302"></a><a name="note1989394717302"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p12614191914218"><a name="p12614191914218"></a><a name="p12614191914218"></a>如果用户只进行全量迁移时，建议停止对源数据库的操作，否则迁移过程中源数据库产生的新数据不会同步到目标数据库。</p>
    </div></div>
    </li><li>全量+增量：该模式为数据库持续性迁移，适用于对业务中断敏感的场景，通过全量迁移过程中完成的目标端数据库的初始化后，增量迁移阶段通过解析日志等技术，将远端和目标端数据库保持数据持续一致。</li></ul>
    <div class="note" id="note3814342165119"><a name="note3814342165119"></a><a name="note3814342165119"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p118141442205110"><a name="p118141442205110"></a><a name="p118141442205110"></a>选择<span class="uicontrol" id="uicontrol24738122117"><a name="uicontrol24738122117"></a><a name="uicontrol24738122117"></a>“全量+增量”</span>迁移模式，增量迁移可以在全量迁移完成的基础上实现数据的持续同步，无需中断业务，实现迁移过程中源业务和数据库继续对外提供访问。</p>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，迁移实例创建成功后，填选源库信息和目标库信息，建议您单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，勾选协议，单击“下一步“。

    **图 3**  源库信息<a name="fig265217351194"></a>  
    ![](figures/源库信息-44.png "源库信息-44")

    **表 3**  源库信息

    <a name="table1859597219"></a>
    <table><thead align="left"><tr id="row108525962110"><th class="cellrowborder" valign="top" width="23%" id="mcps1.2.3.1.1"><p id="p1710155919217"><a name="p1710155919217"></a><a name="p1710155919217"></a><strong id="b17101859162112"><a name="b17101859162112"></a><a name="b17101859162112"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="77%" id="mcps1.2.3.1.2"><p id="p61011459162111"><a name="p61011459162111"></a><a name="p61011459162111"></a><strong id="b6101059192111"><a name="b6101059192111"></a><a name="b6101059192111"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row910120596211"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p310114597219"><a name="p310114597219"></a><a name="p310114597219"></a>数据库实例名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p15101175962114"><a name="p15101175962114"></a><a name="p15101175962114"></a>默认为创建迁移任务时选择的数据库实例，不可进行修改。</p>
    </td>
    </tr>
    <tr id="row1510175917215"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p31161059112113"><a name="p31161059112113"></a><a name="p31161059112113"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p4116195902118"><a name="p4116195902118"></a><a name="p4116195902118"></a>源数据库对应的数据库用户名。</p>
    </td>
    </tr>
    <tr id="row91161059182112"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p51167593212"><a name="p51167593212"></a><a name="p51167593212"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p915681311115"><a name="p915681311115"></a><a name="p915681311115"></a>源数据库对应的数据库用户名密码。</p>
    <div class="note" id="note5992161681118"><a name="note5992161681118"></a><a name="note5992161681118"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p19921816201112"><a name="p19921816201112"></a><a name="p19921816201112"></a>数据库用户名和密码将被系统加密暂存，直至该任务删除后清除。</p>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

    **图 4**  目标库信息<a name="fig59761234142211"></a>  
    ![](figures/目标库信息-45.png "目标库信息-45")

    **表 4**  目标库信息

    <a name="table1353517231365"></a>
    <table><thead align="left"><tr id="row4819321621"><th class="cellrowborder" valign="top" width="23.29%" id="mcps1.2.3.1.1"><p id="p148191426219"><a name="p148191426219"></a><a name="p148191426219"></a><strong id="b14819102625"><a name="b14819102625"></a><a name="b14819102625"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.71%" id="mcps1.2.3.1.2"><p id="p178192021927"><a name="p178192021927"></a><a name="p178192021927"></a><strong id="b178191721220"><a name="b178191721220"></a><a name="b178191721220"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row14819120214"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p48193218211"><a name="p48193218211"></a><a name="p48193218211"></a>IP地址或域名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p6215123031115"><a name="p6215123031115"></a><a name="p6215123031115"></a>源数据库的IP地址或域名，格式为IP地址/域名:端口。其中源数据库服务端口，可输入范围为1~65534间的整数。</p>
    <p id="p897584972711"><a name="p897584972711"></a><a name="p897584972711"></a>该输入框最多支持填写3组源数据库的IP地址或者域名信息，多个值需要使用英文逗号隔开。例如：192.168.0.1:8080,192.168.0.2:8080。同时需要确保所填写的多个IP地址或域名属于同一个实例。</p>
    <div class="note" id="note66221243161214"><a name="note66221243161214"></a><a name="note66221243161214"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p1362214439121"><a name="p1362214439121"></a><a name="p1362214439121"></a>此处若填写的是多组IP地址或者域名信息，在进行测试连接的过程中，只要存在一组IP地址或者域名可以连通，那么测试连接就提示成功。所以需要您保证填写的IP地址或域名的正确性。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row933216286156"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p113331284153"><a name="p113331284153"></a><a name="p113331284153"></a>账号认证数据库</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p63339281150"><a name="p63339281150"></a><a name="p63339281150"></a>填写的数据库账号所属的数据库名称。例如：华为云DDS实例默认的账号认证数据库为admin。</p>
    </td>
    </tr>
    <tr id="row08191623215"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p68191521217"><a name="p68191521217"></a><a name="p68191521217"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p98191821228"><a name="p98191821228"></a><a name="p98191821228"></a>目标数据库的用户名。</p>
    </td>
    </tr>
    <tr id="row98197216211"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p4819523217"><a name="p4819523217"></a><a name="p4819523217"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p16819121724"><a name="p16819121724"></a><a name="p16819121724"></a>目标数据库的用户名所对应的密码。</p>
    </td>
    </tr>
    <tr id="row19827128212"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p1882715215211"><a name="p1882715215211"></a><a name="p1882715215211"></a>SSL安全连接</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p68272021522"><a name="p68272021522"></a><a name="p68272021522"></a>通过该功能，用户可以选择是否开启对迁移链路的加密。如果开启该功能，需要用户上传SSL CA根证书。</p>
    <div class="note" id="note14630114741717"><a name="note14630114741717"></a><a name="note14630114741717"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p8630747181714"><a name="p8630747181714"></a><a name="p8630747181714"></a>最大支持上传500KB的证书文件。</p>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >**目标数据库的IP地址或域名、数据库用户名和密码，会被系统加密暂存，直至删除该迁移任务后自动清除。**  

4.  在“迁移设置“页面，设置迁移对象，单击“下一步“。

    **图 5**  设置迁移对象<a name="zh-cn_topic_0177374171_fig133579181217"></a>  
    ![](figures/设置迁移对象-46.png "设置迁移对象-46")

    **表 5**  迁移对象

    <a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_table165921932111919"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0177374171_zh-cn_topic_0078078071_row165921632141911"><th class="cellrowborder" valign="top" width="16%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p1759233261916"><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p1759233261916"></a><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p1759233261916"></a><strong id="zh-cn_topic_0177374171_zh-cn_topic_0078078071_b1783318515228"><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_b1783318515228"></a><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_b1783318515228"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="84%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p159273271920"><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p159273271920"></a><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p159273271920"></a><strong id="zh-cn_topic_0177374171_zh-cn_topic_0078078071_b10555114922418"><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_b10555114922418"></a><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_b10555114922418"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0177374171_zh-cn_topic_0078078071_row559273214193"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p14592132171916"><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p14592132171916"></a><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p14592132171916"></a>迁移对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p85921932191910"><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p85921932191910"></a><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p85921932191910"></a>对象迁移到目标数据库实例后，对象名将会保持与源数据库实例对象名一致且无法修改。</p>
    <p id="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p1384592151414"><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p1384592151414"></a><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_p1384592151414"></a>您可以根据业务需求，选择全部对象迁移或者自定义迁移对象。</p>
    <a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_ul78601316141810"></a><a name="zh-cn_topic_0177374171_zh-cn_topic_0078078071_ul78601316141810"></a><ul id="zh-cn_topic_0177374171_zh-cn_topic_0078078071_ul78601316141810"><li>全部迁移：将源数据库中的所有对象全部迁移至目标数据库。</li><li>自定义对象：将自定义选择的对象迁移至目标数据库。如果有切换源数据库的操作，请在选择迁移对象前单击右上角的<a name="image12211916210"></a><a name="image12211916210"></a><span><img id="image12211916210" src="figures/drs_icon-2.png"></span>，以确保待选择的对象为最新源数据库对象。</li></ul>
    </td>
    </tr>
    </tbody>
    </table>

5.  在“预检查“页面，进行迁移任务预校验，校验是否可进行迁移。
    -   查看检查结果，如有失败的检查项，需要修复失败项后，单击“重新校验”按钮重新进行迁移任务预校验。

        预检查失败项处理建议请参见《数据复制服务用户指南》中的“[预检查失败项修复方法](https://support.huaweicloud.com/usermanual-drs/drs_precheck.html)”。

    -   预检查完成后，且所有检查项结果均成功时，单击“下一步“。

        **图 6**  预检查<a name="fig14196246164119"></a>  
        ![](figures/预检查-47.png "预检查-47")

        >![](public_sys-resources/icon-note.gif) **说明：**   
        >所有检查项结果均成功时，若存在告警，需要阅读并确认告警详情后才可以继续执行下一步操作。  


6.  在“任务确认“页面，选择迁移任务的启动时间，并确认迁移任务信息无误后，单击“启动任务“，提交迁移任务。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   迁移任务的启动时间可以根据业务需求，设置为“立即启动”或“稍后启动”。  
    >-   预计迁移任务启动后，会对源数据库和目标数据库的性能产生影响，建议选择业务低峰期，合理设置迁移任务的启动时间。  

7.  迁移任务提交后，您可在“在线迁移管理“页面，查看并管理自己的任务。
    -   您可查看任务提交后的状态，状态请参见[任务状态](https://support.huaweicloud.com/qs-drs/drs_03_0001.html)。
    -   在任务列表的右上角，单击![](figures/drs_icon-2.png)刷新列表，可查看到最新的任务状态。



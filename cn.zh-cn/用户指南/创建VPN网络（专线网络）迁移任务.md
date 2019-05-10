# 创建VPN网络（专线网络）迁移任务<a name="drs_02_0021"></a>

本章节将以MySQL到RDS for MySQL的迁移为示例，介绍在VPN（专线）网络场景下，通过数据复制服务管理控制台配置数据迁移任务的流程，其他存储引擎的配置流程类似。

VPN网络（专线网络）适合通过VPN网络（专线网络），实现其他云下自建数据库与云上数据库迁移、或云上跨Region的数据库之间的迁移。

在数据复制服务中，数据库迁移是通过任务的形式完成的，通过创建任务向导，可以完成任务信息配置、任务创建。迁移任务创建成功后，您也可以通过数据复制服务管理控制台，对任务进行管理。

目前数据复制服务支持每个用户最多可创建5个在线迁移任务。

## 前提条件<a name="section196964312381"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   参见[使用限制](https://support.huaweicloud.com/qs-drs/drs_02_0011.html)。
-   参见[申请须知](https://support.huaweicloud.com/qs-drs/drs_online_migration.html)。

## 操作步骤<a name="section1159132373917"></a>

1.  在“在线迁移管理“页面，单击“创建迁移任务“，进入创建迁移任务页面。
2.  在“迁移实例”页面，填选任务名称、通知收件人信息、描述、迁移实例信息，单击“下一步”。

    **图 1**  迁移任务信息<a name="fig1473012110109"></a>  
    ![](figures/迁移任务信息.png "迁移任务信息")

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
    <tr id="row1080215433911"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p158027493912"><a name="p158027493912"></a><a name="p158027493912"></a>通知收件人</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p38891258184013"><a name="p38891258184013"></a><a name="p38891258184013"></a>该项为可选参数，开启之后，需要填写手机号码或者邮箱作为指定收件人。当迁移任务状态异常时，系统将发送通知给指定收件人。</p>
    <div class="note" id="note158461433104913"><a name="note158461433104913"></a><a name="note158461433104913"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p138461333114917"><a name="p138461333114917"></a><a name="p138461333114917"></a>收到确认短信或邮件之后，需要在48小时内处理，否则该功能订阅无效。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row157731032102814"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p1677373232818"><a name="p1677373232818"></a><a name="p1677373232818"></a>时延阈值</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p6681185532914"><a name="p6681185532914"></a><a name="p6681185532914"></a>源数据库和目标数据库之间的同步有时会存在一个时间差，称为时延，单位为秒。</p>
    <p id="p75251915133018"><a name="p75251915133018"></a><a name="p75251915133018"></a>时延阈值设置是指时延超过一定的值后（时间阈值范围为1—3600s），DRS可以发送告警通知给指定收件人。告警通知将在时延稳定超过设定的阈值6min后发送，避免出现由于时延波动反复发送告警通知的情况。</p>
    <div class="note" id="note47298209309"><a name="note47298209309"></a><a name="note47298209309"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul354514492087"></a><a name="ul354514492087"></a><ul id="ul354514492087"><li>首次进入增量迁移阶段，会有较多数据等待同步，存在较大的时延，属于正常情况，不在此功能的监控范围之内。</li><li>设置时间阈值之前，需要填写收件人手机号或邮箱。</li></ul>
    </div></div>
    </td>
    </tr>
    <tr id="row23664659204420"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p37789232204420"><a name="p37789232204420"></a><a name="p37789232204420"></a>描述</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p41028970204420"><a name="p41028970204420"></a><a name="p41028970204420"></a>描述不能超过256位，且不能包含!&lt;&gt;&amp;'\"特殊字符。</p>
    </td>
    </tr>
    </tbody>
    </table>

    **图 2**  迁移实例信息-VPN（专线）<a name="fig6487192516156"></a>  
    ![](figures/迁移实例信息-VPN（专线）.png "迁移实例信息-VPN（专线）")

    **表 2**  迁移实例信息

    <a name="table54580728204436"></a>
    <table><thead align="left"><tr id="row39932329204436"><th class="cellrowborder" valign="top" width="23.87%" id="mcps1.2.3.1.1"><p id="p13293221204436"><a name="p13293221204436"></a><a name="p13293221204436"></a><strong id="b2587841611355"><a name="b2587841611355"></a><a name="b2587841611355"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.13%" id="mcps1.2.3.1.2"><p id="p3009113204436"><a name="p3009113204436"></a><a name="p3009113204436"></a><strong id="b1577696211355"><a name="b1577696211355"></a><a name="b1577696211355"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row129641656121716"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p12964756151713"><a name="p12964756151713"></a><a name="p12964756151713"></a>数据流动方向</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p11514173891212"><a name="p11514173891212"></a><a name="p11514173891212"></a>选择入云。</p>
    <p id="p1983838136"><a name="p1983838136"></a><a name="p1983838136"></a>入云指目标端数据库为华为云关系型数据库。</p>
    </td>
    </tr>
    <tr id="row0414184610580"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1414046115813"><a name="p1414046115813"></a><a name="p1414046115813"></a>源数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p228051952218"><a name="p228051952218"></a><a name="p228051952218"></a>选择MySQL。</p>
    <p id="p04141646165817"><a name="p04141646165817"></a><a name="p04141646165817"></a>目前支持的数据库引擎有：MySQL、Microsoft SQL Server、PostgreSQL、MongoDB、Oracle。</p>
    </td>
    </tr>
    <tr id="row42411630204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p12790028204436"><a name="p12790028204436"></a><a name="p12790028204436"></a>目标数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p11406942102210"><a name="p11406942102210"></a><a name="p11406942102210"></a>选择MySQL。</p>
    <p id="p29359322204436"><a name="p29359322204436"></a><a name="p29359322204436"></a>目前支持的数据库引擎有：MySQL、Microsoft SQL Server、PostgreSQL、MongoDB。</p>
    </td>
    </tr>
    <tr id="row62907306204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p62327044204436"><a name="p62327044204436"></a><a name="p62327044204436"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p87075558433"><a name="p87075558433"></a><a name="p87075558433"></a>选择VPN、专线网络。</p>
    <p id="p10936926102210"><a name="p10936926102210"></a><a name="p10936926102210"></a>默认为公网网络类型，支持VPC网络、VPN网络、专线网络、公网网络。</p>
    <a name="ul1872454917306"></a><a name="ul1872454917306"></a><ul id="ul1872454917306"><li>VPC网络：适合云上数据库之间的迁移。</li><li>公网网络：适合通过公网网络把其他云下或其他平台的数据库迁移到目标数据库，该类型要求目标数据库绑定弹性公网IP（EIP）。</li><li>VPN网络：适合通过VPN网络，实现其他云下自建数据库与云上数据库迁移、或云上跨Region的数据库之间的迁移。</li><li>专线网络：适合通过专线网络，实现其他云下自建数据库与云上数据库迁移、或云上跨Region的数据库之间的迁移。</li></ul>
    </td>
    </tr>
    <tr id="row658644204515"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p53350183204515"><a name="p53350183204515"></a><a name="p53350183204515"></a>目标数据库实例</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p26397538204515"><a name="p26397538204515"></a><a name="p26397538204515"></a>用户所创建的关系型数据库实例。</p>
    </td>
    </tr>
    <tr id="row616054211295"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p18162154202918"><a name="p18162154202918"></a><a name="p18162154202918"></a>目标库读写设置</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><a name="ul441372842315"></a><a name="ul441372842315"></a><ul id="ul441372842315"><li>只读<p id="p161716541232"><a name="p161716541232"></a><a name="p161716541232"></a>若目标数据库设置为只读模式，在迁移过程中，目标数据库将转化为只读、不可写入的状态，迁移任务结束后恢复可读写状态，此选项可有效的确保数据迁移的完整性和成功率。</p>
    </li><li>读写<p id="p63044226243"><a name="p63044226243"></a><a name="p63044226243"></a>若目标数据库设置为读写模式，则在迁移过程中，目标数据库可以进行读写，但需要用户避免操作与更改数据库迁移中的数据，规避数据冲突导致的迁移失败。</p>
    </li></ul>
    <div class="note" id="note1932819586221"><a name="note1932819586221"></a><a name="note1932819586221"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p1328205892213"><a name="p1328205892213"></a><a name="p1328205892213"></a>目前仅MySQL数据库支持目标库读写设置。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row118961082716"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p128192616518"><a name="p128192616518"></a><a name="p128192616518"></a>迁移模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><a name="ul171919713019"></a><a name="ul171919713019"></a><ul id="ul171919713019"><li>全量：该模式为数据库一次性迁移，适用于可中断业务的<span class="keyword" id="keyword8520910122110"><a name="keyword8520910122110"></a><a name="keyword8520910122110"></a>数据库迁移</span>场景，全量迁移将非系统数据库的全部数据库对象和数据一次性迁移至目标端数据库，包括：表、视图、存储过程等。<div class="note" id="note1989394717302"><a name="note1989394717302"></a><a name="note1989394717302"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p12614191914218"><a name="p12614191914218"></a><a name="p12614191914218"></a>如果用户只进行全量迁移时，建议停止对源数据库的操作，否则迁移过程中源数据库产生的新数据不会同步到目标数据库。</p>
    </div></div>
    </li><li>全量+增量：该模式为数据库持续性迁移，适用于对业务中断敏感的场景，通过全量迁移过程中完成的目标端数据库的初始化后，增量迁移阶段通过解析日志等技术，将远端和目标端数据库保持数据持续一致。</li></ul>
    <div class="note" id="note3814342165119"><a name="note3814342165119"></a><a name="note3814342165119"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p118141442205110"><a name="p118141442205110"></a><a name="p118141442205110"></a>选择<span class="uicontrol" id="uicontrol24738122117"><a name="uicontrol24738122117"></a><a name="uicontrol24738122117"></a>“全量+增量”</span>迁移模式，增量迁移可以在全量迁移完成的基础上实现数据的持续同步，无需中断业务，实现迁移过程中源业务和数据库继续对外提供访问。</p>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，迁移实例创建成功后，填选源库信息和目标库信息，建议您单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，勾选协议，单击“下一步“。

    **图 3**  源库信息页面-VPN（专线）<a name="fig136531923115918"></a>  
    ![](figures/源库信息页面-VPN（专线）.png "源库信息页面-VPN（专线）")

    **表 3**  源库信息

    <a name="table1665310232597"></a>
    <table><thead align="left"><tr id="row12653123195919"><th class="cellrowborder" valign="top" width="23.29%" id="mcps1.2.3.1.1"><p id="p156531623165916"><a name="p156531623165916"></a><a name="p156531623165916"></a><strong id="b20653923155913"><a name="b20653923155913"></a><a name="b20653923155913"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.71%" id="mcps1.2.3.1.2"><p id="p1365312365910"><a name="p1365312365910"></a><a name="p1365312365910"></a><strong id="b186531223105910"><a name="b186531223105910"></a><a name="b186531223105910"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1265352355912"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p665313232598"><a name="p665313232598"></a><a name="p665313232598"></a>IP地址或域名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p2653523145918"><a name="p2653523145918"></a><a name="p2653523145918"></a>源数据库的IP地址或域名。</p>
    </td>
    </tr>
    <tr id="row765313235597"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p8653172395914"><a name="p8653172395914"></a><a name="p8653172395914"></a>端口</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p15653192315910"><a name="p15653192315910"></a><a name="p15653192315910"></a>源数据库服务端口，可输入范围为1~65535间的整数。</p>
    </td>
    </tr>
    <tr id="row9653102325913"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p4653162320598"><a name="p4653162320598"></a><a name="p4653162320598"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p8653423135910"><a name="p8653423135910"></a><a name="p8653423135910"></a>源数据库的用户名。</p>
    </td>
    </tr>
    <tr id="row065352315596"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p86531023135911"><a name="p86531023135911"></a><a name="p86531023135911"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p665318234591"><a name="p665318234591"></a><a name="p665318234591"></a>源数据库的用户名所对应的密码。</p>
    </td>
    </tr>
    <tr id="row26531923125912"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p2653112395910"><a name="p2653112395910"></a><a name="p2653112395910"></a>SSL安全连接</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p765310236599"><a name="p765310236599"></a><a name="p765310236599"></a>通过该功能，用户可以选择是否开启对迁移链路的加密，如果开启，需要用户上传SSL CA根证书。</p>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >**源数据库的IP地址或域名、数据库用户名和密码，会被系统加密暂存，直至删除该迁移任务后自动清除。**  

    -   目标库信息配置

        **图 4**  目标库信息-VPN（专线）<a name="fig186534231595"></a>  
        ![](figures/目标库信息-VPN（专线）.png "目标库信息-VPN（专线）")

        **表 4**  目标库信息

        <a name="table157461610185911"></a>
        <table><thead align="left"><tr id="row15746151015912"><th class="cellrowborder" valign="top" width="23%" id="mcps1.2.3.1.1"><p id="p18746101055912"><a name="p18746101055912"></a><a name="p18746101055912"></a><strong id="b074631019593"><a name="b074631019593"></a><a name="b074631019593"></a>参数</strong></p>
        </th>
        <th class="cellrowborder" valign="top" width="77%" id="mcps1.2.3.1.2"><p id="p15746181055920"><a name="p15746181055920"></a><a name="p15746181055920"></a><strong id="b1774613108597"><a name="b1774613108597"></a><a name="b1774613108597"></a>描述</strong></p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row0746151020595"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p1674610102597"><a name="p1674610102597"></a><a name="p1674610102597"></a>数据库实例名称</p>
        </td>
        <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p3746710165918"><a name="p3746710165918"></a><a name="p3746710165918"></a>默认为创建迁移任务时选择的关系型数据库实例，不可进行修改。</p>
        </td>
        </tr>
        <tr id="row2746310155916"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p18746310175911"><a name="p18746310175911"></a><a name="p18746310175911"></a>数据库用户名</p>
        </td>
        <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p874691012591"><a name="p874691012591"></a><a name="p874691012591"></a>目标数据库对应的数据库用户名。</p>
        </td>
        </tr>
        <tr id="row107461010135910"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p47463101599"><a name="p47463101599"></a><a name="p47463101599"></a>数据库密码</p>
        </td>
        <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p47461410155914"><a name="p47461410155914"></a><a name="p47461410155914"></a>数据库用户名和密码将被系统加密暂存，直至该任务删除后清除。</p>
        </td>
        </tr>
        </tbody>
        </table>


4.  在“设定迁移“页面，设置迁移用户和迁移对象，单击“下一步“。

    **图 5**  迁移模式-VPN（专线）<a name="zh-cn_topic_0078078071_fig46205265911"></a>  
    ![](figures/迁移模式-VPN（专线）.png "迁移模式-VPN（专线）")

    **表 5**  迁移模式和迁移对象

    <a name="zh-cn_topic_0078078071_table165921932111919"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0078078071_row165921632141911"><th class="cellrowborder" valign="top" width="16%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0078078071_p1759233261916"><a name="zh-cn_topic_0078078071_p1759233261916"></a><a name="zh-cn_topic_0078078071_p1759233261916"></a><strong id="zh-cn_topic_0078078071_b1783318515228"><a name="zh-cn_topic_0078078071_b1783318515228"></a><a name="zh-cn_topic_0078078071_b1783318515228"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="84%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0078078071_p159273271920"><a name="zh-cn_topic_0078078071_p159273271920"></a><a name="zh-cn_topic_0078078071_p159273271920"></a><strong id="zh-cn_topic_0078078071_b10555114922418"><a name="zh-cn_topic_0078078071_b10555114922418"></a><a name="zh-cn_topic_0078078071_b10555114922418"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0078078071_row2592193212194"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0078078071_p7592232201911"><a name="zh-cn_topic_0078078071_p7592232201911"></a><a name="zh-cn_topic_0078078071_p7592232201911"></a>迁移用户</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0078078071_p11670239171013"><a name="zh-cn_topic_0078078071_p11670239171013"></a><a name="zh-cn_topic_0078078071_p11670239171013"></a>数据库的迁移过程中，迁移用户需要进行单独处理。</p>
    <p id="zh-cn_topic_0078078071_p106411111205412"><a name="zh-cn_topic_0078078071_p106411111205412"></a><a name="zh-cn_topic_0078078071_p106411111205412"></a>常见的迁移用户一般分为三类：可完整迁移的用户、需要降权的用户和不可迁移的用户。您可以根据业务需求选择“迁移”或者“不迁移”。</p>
    <a name="zh-cn_topic_0078078071_ul52489455107"></a><a name="zh-cn_topic_0078078071_ul52489455107"></a><ul id="zh-cn_topic_0078078071_ul52489455107"><li>迁移</li></ul>
    <p id="zh-cn_topic_0078078071_p14479154720361"><a name="zh-cn_topic_0078078071_p14479154720361"></a><a name="zh-cn_topic_0078078071_p14479154720361"></a>迁移用户功能将展示源数据所有用户和对应权限列表，帮助您判断这些用户是否可进行迁移。为了确保迁移过程中数据的安全性，您可对支持迁移的用户（包括可完整迁移的用户和需要降权的用户）设置密码后进行迁移。</p>
    <p id="zh-cn_topic_0078078071_p1164671612111"><a name="zh-cn_topic_0078078071_p1164671612111"></a><a name="zh-cn_topic_0078078071_p1164671612111"></a>设置密码的方式有如下两种：</p>
    <p id="zh-cn_topic_0078078071_p171121820172212"><a name="zh-cn_topic_0078078071_p171121820172212"></a><a name="zh-cn_topic_0078078071_p171121820172212"></a>方法一：选择指定支持迁移的用户，在“设置密码”列可直接输入设置密码。</p>
    <p id="zh-cn_topic_0078078071_p15731334172318"><a name="zh-cn_topic_0078078071_p15731334172318"></a><a name="zh-cn_topic_0078078071_p15731334172318"></a>方法二：为了节省时间，您也可以选择所有支持迁移的用户，单击右下角“统一设置密码”，批量进行密码设置。使用该方法设置的密码，待迁移成功后，可以在目标数据库端通过执行DDL语句，进行密码重置。</p>
    <p id="zh-cn_topic_0078078071_p7266323155716"><a name="zh-cn_topic_0078078071_p7266323155716"></a><a name="zh-cn_topic_0078078071_p7266323155716"></a>对于需要降权处理的用户和不支持迁移的用户，您需要单击对应用户备注列的“查看”，确认详情后才可进行下一步操作。</p>
    <p id="zh-cn_topic_0078078071_p2124163218257"><a name="zh-cn_topic_0078078071_p2124163218257"></a><a name="zh-cn_topic_0078078071_p2124163218257"></a>如果存在多个需要查看备注详情的用户，您也可以单击“确认所有备注”按钮，一键查看备注信息。</p>
    <div class="note" id="zh-cn_topic_0078078071_note441338192113"><a name="zh-cn_topic_0078078071_note441338192113"></a><a name="zh-cn_topic_0078078071_note441338192113"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="zh-cn_topic_0078078071_ul18266139184618"></a><a name="zh-cn_topic_0078078071_ul18266139184618"></a><ul id="zh-cn_topic_0078078071_ul18266139184618"><li>需要降权的用户指具有不满足目标数据库权限要求的部分高权限的用户，比如具有：super、file、shutdown等高权限的用户。该类用户在进行迁移时需要进行降权处理，否则会导致迁移失败。迁移成功后，存储在目标数据库中的对应用户是经过降权处理的用户。</li><li>目前仅MySQL支持迁移用户功能。</li><li>对于不支持迁移的账号，该类帐号将在目标数据库中缺失，请先确保业务不受该类帐号影响。同时，任务启动后，所有针对该类帐号进行的权限密码操作，将会导致增量迁移失败。</li></ul>
    </div></div>
    <a name="zh-cn_topic_0078078071_ul17378301111"></a><a name="zh-cn_topic_0078078071_ul17378301111"></a><ul id="zh-cn_topic_0078078071_ul17378301111"><li>不迁移<p id="zh-cn_topic_0078078071_p794655681211"><a name="zh-cn_topic_0078078071_p794655681211"></a><a name="zh-cn_topic_0078078071_p794655681211"></a>迁移过程中，将不进行用户和权限的迁移。</p>
    </li></ul>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row559273214193"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0078078071_p14592132171916"><a name="zh-cn_topic_0078078071_p14592132171916"></a><a name="zh-cn_topic_0078078071_p14592132171916"></a>迁移对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0078078071_p85921932191910"><a name="zh-cn_topic_0078078071_p85921932191910"></a><a name="zh-cn_topic_0078078071_p85921932191910"></a>迁移对象选择的粒度可以为数据库的全对象，对象迁移到目标数据库实例后，对象名将会保持与源数据库实例对象名一致且无法修改。</p>
    <p id="zh-cn_topic_0078078071_p1384592151414"><a name="zh-cn_topic_0078078071_p1384592151414"></a><a name="zh-cn_topic_0078078071_p1384592151414"></a>您可以根据业务需求，选择全部对象迁移或者自定义迁移对象。</p>
    <a name="zh-cn_topic_0078078071_ul78601316141810"></a><a name="zh-cn_topic_0078078071_ul78601316141810"></a><ul id="zh-cn_topic_0078078071_ul78601316141810"><li>全部迁移：将源数据库中的所有对象全部迁移至目标数据库。</li><li>自定义对象：将自定义选择的对象迁移至目标数据库。</li></ul>
    <div class="note" id="zh-cn_topic_0078078071_note6192135932115"><a name="zh-cn_topic_0078078071_note6192135932115"></a><a name="zh-cn_topic_0078078071_note6192135932115"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="zh-cn_topic_0078078071_p161921759152114"><a name="zh-cn_topic_0078078071_p161921759152114"></a><a name="zh-cn_topic_0078078071_p161921759152114"></a>若选择部分数据库进行迁移时，由于存储过程、视图等对象可能与其他数据库的表存在依赖关系，若所依赖的表未迁移，则会导致迁移失败。建议您在迁移之前进行确认，或选择全部数据库进行迁移。</p>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

5.  在“预检查“页面，进行迁移任务预校验，校验是否可进行迁移。
    -   查看检查结果，如有失败的检查项，需要修复失败项后，单击“重新校验”按钮重新进行迁移任务预校验。

        预检查失败项处理建议请参见《数据复制服务用户指南》中的“[预检查失败项修复方法](https://support.huaweicloud.com/usermanual-drs/drs_precheck.html)”。

        **图 6**  预检查<a name="zh-cn_topic_0078078071_fig237882315489"></a>  
        ![](figures/预检查.png "预检查")


    -   预检查完成后，且预检查通过率为100%时，单击“下一步”。

        >![](public_sys-resources/icon-note.gif) **说明：**   
        >所有检查项结果均成功时，若存在告警，需要阅读并确认告警详情后才可以继续执行下一步操作。  


6.  进入“参数对比“页面，该步骤为可选操作。

    您可以根据业务需求，进行源数据库和目标数据库参数的一致性对比。该操作不影响数据的迁移，主要目的是为了确保迁移成功后业务应用的使用不受影响。

    参数对比功能从常规参数和性能参数两个维度，展示了源数据库和目标数据库的参数值是否一致，而且提供了一键修改的功能。通过一键修改可以将源数据库和目标数据库的参数值自动修改为一致，从而确保迁移后业务的稳定性。

    一般情况下，对于常规参数，如果源库和目标库存在不一致的情况，建议使用一键修复功能将参数值修改为一致。

    对于性能参数，您可以根据业务场景，自定义源数据库和目标库的参数值。

    **图 7**  修改参数<a name="zh-cn_topic_0078078071_fig796212218215"></a>  
    ![](figures/修改参数.png "修改参数")

    通过参数对比功能修改的部分参数值，无法在目标数据库立即生效，需要重启才能生效。建议您在迁移任务启动之前重启目标数据库，或者迁移结束后选择一个计划时间重启。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >如果您选择迁移结束后重启目标数据库，请合理设置重启计划时间，避免参数生效太晚影响业务的正常使用。  

    针对MySQL5.6和MySQL5.7版本，[表6](#zh-cn_topic_0078078071_table117481636102314)和[表7](#zh-cn_topic_0078078071_table122391643123118)分别列举了常见的常规参数及性能参数，方便您在使用参数对比功能时进行参考。

    **表 6**  MySQL5.6参数列表

    <a name="zh-cn_topic_0078078071_table117481636102314"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0078078071_row1474883622318"><th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.1"><p id="zh-cn_topic_0078078071_p67484369233"><a name="zh-cn_topic_0078078071_p67484369233"></a><a name="zh-cn_topic_0078078071_p67484369233"></a><strong id="zh-cn_topic_0078078071_b192122842613"><a name="zh-cn_topic_0078078071_b192122842613"></a><a name="zh-cn_topic_0078078071_b192122842613"></a>参数名称</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.2"><p id="zh-cn_topic_0078078071_p1174911366233"><a name="zh-cn_topic_0078078071_p1174911366233"></a><a name="zh-cn_topic_0078078071_p1174911366233"></a><strong id="zh-cn_topic_0078078071_b2941528192610"><a name="zh-cn_topic_0078078071_b2941528192610"></a><a name="zh-cn_topic_0078078071_b2941528192610"></a>参数类型</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.3"><p id="zh-cn_topic_0078078071_p137497363233"><a name="zh-cn_topic_0078078071_p137497363233"></a><a name="zh-cn_topic_0078078071_p137497363233"></a><strong id="zh-cn_topic_0078078071_b5951928142617"><a name="zh-cn_topic_0078078071_b5951928142617"></a><a name="zh-cn_topic_0078078071_b5951928142617"></a>可选值</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.4"><p id="zh-cn_topic_0078078071_p674923615237"><a name="zh-cn_topic_0078078071_p674923615237"></a><a name="zh-cn_topic_0078078071_p674923615237"></a><strong id="zh-cn_topic_0078078071_b1196528132619"><a name="zh-cn_topic_0078078071_b1196528132619"></a><a name="zh-cn_topic_0078078071_b1196528132619"></a>是否需要重启</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0078078071_row1967520584285"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1068001216297"><a name="zh-cn_topic_0078078071_p1068001216297"></a><a name="zh-cn_topic_0078078071_p1068001216297"></a>connect_timeout</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p66832056102911"><a name="zh-cn_topic_0078078071_p66832056102911"></a><a name="zh-cn_topic_0078078071_p66832056102911"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p26761658122811"><a name="zh-cn_topic_0078078071_p26761658122811"></a><a name="zh-cn_topic_0078078071_p26761658122811"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1867695815283"><a name="zh-cn_topic_0078078071_p1867695815283"></a><a name="zh-cn_topic_0078078071_p1867695815283"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1776895618283"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p12680111212914"><a name="zh-cn_topic_0078078071_p12680111212914"></a><a name="zh-cn_topic_0078078071_p12680111212914"></a>event_scheduler</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p18351057142919"><a name="zh-cn_topic_0078078071_p18351057142919"></a><a name="zh-cn_topic_0078078071_p18351057142919"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p6769165612813"><a name="zh-cn_topic_0078078071_p6769165612813"></a><a name="zh-cn_topic_0078078071_p6769165612813"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p6769195662813"><a name="zh-cn_topic_0078078071_p6769195662813"></a><a name="zh-cn_topic_0078078071_p6769195662813"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row8507125472816"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p750810546288"><a name="zh-cn_topic_0078078071_p750810546288"></a><a name="zh-cn_topic_0078078071_p750810546288"></a>innodb_lock_wait_timeout</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p096416587295"><a name="zh-cn_topic_0078078071_p096416587295"></a><a name="zh-cn_topic_0078078071_p096416587295"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p195088547283"><a name="zh-cn_topic_0078078071_p195088547283"></a><a name="zh-cn_topic_0078078071_p195088547283"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p17508854122815"><a name="zh-cn_topic_0078078071_p17508854122815"></a><a name="zh-cn_topic_0078078071_p17508854122815"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row598875120286"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1698825115284"><a name="zh-cn_topic_0078078071_p1698825115284"></a><a name="zh-cn_topic_0078078071_p1698825115284"></a>max_connections</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p59891459202913"><a name="zh-cn_topic_0078078071_p59891459202913"></a><a name="zh-cn_topic_0078078071_p59891459202913"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p1798812515288"><a name="zh-cn_topic_0078078071_p1798812515288"></a><a name="zh-cn_topic_0078078071_p1798812515288"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p89889511281"><a name="zh-cn_topic_0078078071_p89889511281"></a><a name="zh-cn_topic_0078078071_p89889511281"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1091974972810"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p11110165232917"><a name="zh-cn_topic_0078078071_p11110165232917"></a><a name="zh-cn_topic_0078078071_p11110165232917"></a>net_read_timeout</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p1939617309"><a name="zh-cn_topic_0078078071_p1939617309"></a><a name="zh-cn_topic_0078078071_p1939617309"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p3920149182819"><a name="zh-cn_topic_0078078071_p3920149182819"></a><a name="zh-cn_topic_0078078071_p3920149182819"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p5920124914288"><a name="zh-cn_topic_0078078071_p5920124914288"></a><a name="zh-cn_topic_0078078071_p5920124914288"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row137471447142814"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p211014522290"><a name="zh-cn_topic_0078078071_p211014522290"></a><a name="zh-cn_topic_0078078071_p211014522290"></a>net_write_timeout</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p183429216308"><a name="zh-cn_topic_0078078071_p183429216308"></a><a name="zh-cn_topic_0078078071_p183429216308"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p3747144752814"><a name="zh-cn_topic_0078078071_p3747144752814"></a><a name="zh-cn_topic_0078078071_p3747144752814"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1374744711281"><a name="zh-cn_topic_0078078071_p1374744711281"></a><a name="zh-cn_topic_0078078071_p1374744711281"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row8855469254"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p12749183642315"><a name="zh-cn_topic_0078078071_p12749183642315"></a><a name="zh-cn_topic_0078078071_p12749183642315"></a>explicit_defaults_for_timestamp</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p5749113612316"><a name="zh-cn_topic_0078078071_p5749113612316"></a><a name="zh-cn_topic_0078078071_p5749113612316"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p2749836132316"><a name="zh-cn_topic_0078078071_p2749836132316"></a><a name="zh-cn_topic_0078078071_p2749836132316"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p19749153615231"><a name="zh-cn_topic_0078078071_p19749153615231"></a><a name="zh-cn_topic_0078078071_p19749153615231"></a>是</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row127161843152511"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p11750193672318"><a name="zh-cn_topic_0078078071_p11750193672318"></a><a name="zh-cn_topic_0078078071_p11750193672318"></a>innodb_flush_log_at_trx_commit</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p5178321155914"><a name="zh-cn_topic_0078078071_p5178321155914"></a><a name="zh-cn_topic_0078078071_p5178321155914"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p15750193602313"><a name="zh-cn_topic_0078078071_p15750193602313"></a><a name="zh-cn_topic_0078078071_p15750193602313"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p8750163682311"><a name="zh-cn_topic_0078078071_p8750163682311"></a><a name="zh-cn_topic_0078078071_p8750163682311"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row16540204192511"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p875163611232"><a name="zh-cn_topic_0078078071_p875163611232"></a><a name="zh-cn_topic_0078078071_p875163611232"></a>max_allowed_packet</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p7751133602312"><a name="zh-cn_topic_0078078071_p7751133602312"></a><a name="zh-cn_topic_0078078071_p7751133602312"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p7751236112319"><a name="zh-cn_topic_0078078071_p7751236112319"></a><a name="zh-cn_topic_0078078071_p7751236112319"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p15751133613230"><a name="zh-cn_topic_0078078071_p15751133613230"></a><a name="zh-cn_topic_0078078071_p15751133613230"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row4524203913253"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1275213365236"><a name="zh-cn_topic_0078078071_p1275213365236"></a><a name="zh-cn_topic_0078078071_p1275213365236"></a>tx_isolation</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p275293616239"><a name="zh-cn_topic_0078078071_p275293616239"></a><a name="zh-cn_topic_0078078071_p275293616239"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p167521336172314"><a name="zh-cn_topic_0078078071_p167521336172314"></a><a name="zh-cn_topic_0078078071_p167521336172314"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1575293622310"><a name="zh-cn_topic_0078078071_p1575293622310"></a><a name="zh-cn_topic_0078078071_p1575293622310"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row11397193710255"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p16328185914520"><a name="zh-cn_topic_0078078071_p16328185914520"></a><a name="zh-cn_topic_0078078071_p16328185914520"></a>character_set_client</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p0918143468"><a name="zh-cn_topic_0078078071_p0918143468"></a><a name="zh-cn_topic_0078078071_p0918143468"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p6752163614234"><a name="zh-cn_topic_0078078071_p6752163614234"></a><a name="zh-cn_topic_0078078071_p6752163614234"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p139991115184610"><a name="zh-cn_topic_0078078071_p139991115184610"></a><a name="zh-cn_topic_0078078071_p139991115184610"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row045413352258"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p103282595454"><a name="zh-cn_topic_0078078071_p103282595454"></a><a name="zh-cn_topic_0078078071_p103282595454"></a>character_set_connection</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p31518613466"><a name="zh-cn_topic_0078078071_p31518613466"></a><a name="zh-cn_topic_0078078071_p31518613466"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p7752113611236"><a name="zh-cn_topic_0078078071_p7752113611236"></a><a name="zh-cn_topic_0078078071_p7752113611236"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p4149417194612"><a name="zh-cn_topic_0078078071_p4149417194612"></a><a name="zh-cn_topic_0078078071_p4149417194612"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1438216324254"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1328759114515"><a name="zh-cn_topic_0078078071_p1328759114515"></a><a name="zh-cn_topic_0078078071_p1328759114515"></a>collation_connection</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p12593794610"><a name="zh-cn_topic_0078078071_p12593794610"></a><a name="zh-cn_topic_0078078071_p12593794610"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p8752123682319"><a name="zh-cn_topic_0078078071_p8752123682319"></a><a name="zh-cn_topic_0078078071_p8752123682319"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p12361118174619"><a name="zh-cn_topic_0078078071_p12361118174619"></a><a name="zh-cn_topic_0078078071_p12361118174619"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row15270530102513"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p14328659154512"><a name="zh-cn_topic_0078078071_p14328659154512"></a><a name="zh-cn_topic_0078078071_p14328659154512"></a>character_set_results</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p141159812465"><a name="zh-cn_topic_0078078071_p141159812465"></a><a name="zh-cn_topic_0078078071_p141159812465"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p177531136192312"><a name="zh-cn_topic_0078078071_p177531136192312"></a><a name="zh-cn_topic_0078078071_p177531136192312"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p640611910469"><a name="zh-cn_topic_0078078071_p640611910469"></a><a name="zh-cn_topic_0078078071_p640611910469"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row13272182792511"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p15637132384716"><a name="zh-cn_topic_0078078071_p15637132384716"></a><a name="zh-cn_topic_0078078071_p15637132384716"></a>collation_server</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p975433692316"><a name="zh-cn_topic_0078078071_p975433692316"></a><a name="zh-cn_topic_0078078071_p975433692316"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p19754193632314"><a name="zh-cn_topic_0078078071_p19754193632314"></a><a name="zh-cn_topic_0078078071_p19754193632314"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1875473615232"><a name="zh-cn_topic_0078078071_p1875473615232"></a><a name="zh-cn_topic_0078078071_p1875473615232"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row8749193614239"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p8749133611233"><a name="zh-cn_topic_0078078071_p8749133611233"></a><a name="zh-cn_topic_0078078071_p8749133611233"></a>binlog_cache_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p1874919361238"><a name="zh-cn_topic_0078078071_p1874919361238"></a><a name="zh-cn_topic_0078078071_p1874919361238"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p167491936192312"><a name="zh-cn_topic_0078078071_p167491936192312"></a><a name="zh-cn_topic_0078078071_p167491936192312"></a>4,096～18,446,744,073,709,547,520</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p177493364238"><a name="zh-cn_topic_0078078071_p177493364238"></a><a name="zh-cn_topic_0078078071_p177493364238"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1274943618231"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1858125014294"><a name="zh-cn_topic_0078078071_p1858125014294"></a><a name="zh-cn_topic_0078078071_p1858125014294"></a>binlog_stmt_cache_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p4814153122912"><a name="zh-cn_topic_0078078071_p4814153122912"></a><a name="zh-cn_topic_0078078071_p4814153122912"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p107491336152311"><a name="zh-cn_topic_0078078071_p107491336152311"></a><a name="zh-cn_topic_0078078071_p107491336152311"></a>4,096～18,446,744,073,709,547,520</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1174973611235"><a name="zh-cn_topic_0078078071_p1174973611235"></a><a name="zh-cn_topic_0078078071_p1174973611235"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1274963617232"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p20749123622314"><a name="zh-cn_topic_0078078071_p20749123622314"></a><a name="zh-cn_topic_0078078071_p20749123622314"></a>bulk_insert_buffer_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p216251123111"><a name="zh-cn_topic_0078078071_p216251123111"></a><a name="zh-cn_topic_0078078071_p216251123111"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p0749163610239"><a name="zh-cn_topic_0078078071_p0749163610239"></a><a name="zh-cn_topic_0078078071_p0749163610239"></a>0～18,446,744,073,709,551,615</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p4749193682310"><a name="zh-cn_topic_0078078071_p4749193682310"></a><a name="zh-cn_topic_0078078071_p4749193682310"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1474983602311"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p11750173613233"><a name="zh-cn_topic_0078078071_p11750173613233"></a><a name="zh-cn_topic_0078078071_p11750173613233"></a>innodb_buffer_pool_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p47509365239"><a name="zh-cn_topic_0078078071_p47509365239"></a><a name="zh-cn_topic_0078078071_p47509365239"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p6750163616239"><a name="zh-cn_topic_0078078071_p6750163616239"></a><a name="zh-cn_topic_0078078071_p6750163616239"></a>5,242,880～18,446,744,073,709,551,615</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p7750103692311"><a name="zh-cn_topic_0078078071_p7750103692311"></a><a name="zh-cn_topic_0078078071_p7750103692311"></a>是</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row19750203616236"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p19750143612314"><a name="zh-cn_topic_0078078071_p19750143612314"></a><a name="zh-cn_topic_0078078071_p19750143612314"></a>key_buffer_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p5750153682316"><a name="zh-cn_topic_0078078071_p5750153682316"></a><a name="zh-cn_topic_0078078071_p5750153682316"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p6750103619231"><a name="zh-cn_topic_0078078071_p6750103619231"></a><a name="zh-cn_topic_0078078071_p6750103619231"></a>8～9,223,372,036,854,771,712</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p11750436142317"><a name="zh-cn_topic_0078078071_p11750436142317"></a><a name="zh-cn_topic_0078078071_p11750436142317"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row475020366231"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p16750153622318"><a name="zh-cn_topic_0078078071_p16750153622318"></a><a name="zh-cn_topic_0078078071_p16750153622318"></a>long_query_time</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p11979933103914"><a name="zh-cn_topic_0078078071_p11979933103914"></a><a name="zh-cn_topic_0078078071_p11979933103914"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p207503365239"><a name="zh-cn_topic_0078078071_p207503365239"></a><a name="zh-cn_topic_0078078071_p207503365239"></a>0～3,600</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1720503773911"><a name="zh-cn_topic_0078078071_p1720503773911"></a><a name="zh-cn_topic_0078078071_p1720503773911"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row275133652316"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1275153612312"><a name="zh-cn_topic_0078078071_p1275153612312"></a><a name="zh-cn_topic_0078078071_p1275153612312"></a>query_cache_type</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p47513366230"><a name="zh-cn_topic_0078078071_p47513366230"></a><a name="zh-cn_topic_0078078071_p47513366230"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p875193642311"><a name="zh-cn_topic_0078078071_p875193642311"></a><a name="zh-cn_topic_0078078071_p875193642311"></a>OFF, ON, DEMAND</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p9751436112319"><a name="zh-cn_topic_0078078071_p9751436112319"></a><a name="zh-cn_topic_0078078071_p9751436112319"></a>是</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1175133615232"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p2751163632317"><a name="zh-cn_topic_0078078071_p2751163632317"></a><a name="zh-cn_topic_0078078071_p2751163632317"></a>read_buffer_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p575113362233"><a name="zh-cn_topic_0078078071_p575113362233"></a><a name="zh-cn_topic_0078078071_p575113362233"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p6751636192310"><a name="zh-cn_topic_0078078071_p6751636192310"></a><a name="zh-cn_topic_0078078071_p6751636192310"></a>8,192～2,147,479,552</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p87512036152316"><a name="zh-cn_topic_0078078071_p87512036152316"></a><a name="zh-cn_topic_0078078071_p87512036152316"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row18751153632311"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p5751103692311"><a name="zh-cn_topic_0078078071_p5751103692311"></a><a name="zh-cn_topic_0078078071_p5751103692311"></a>read_rnd_buffer_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p675103682313"><a name="zh-cn_topic_0078078071_p675103682313"></a><a name="zh-cn_topic_0078078071_p675103682313"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p775173614232"><a name="zh-cn_topic_0078078071_p775173614232"></a><a name="zh-cn_topic_0078078071_p775173614232"></a>1～2,147,483,647</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p67513362232"><a name="zh-cn_topic_0078078071_p67513362232"></a><a name="zh-cn_topic_0078078071_p67513362232"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row10751123610232"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1175115364231"><a name="zh-cn_topic_0078078071_p1175115364231"></a><a name="zh-cn_topic_0078078071_p1175115364231"></a>sort_buffer_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p3751836162313"><a name="zh-cn_topic_0078078071_p3751836162313"></a><a name="zh-cn_topic_0078078071_p3751836162313"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p17751193692311"><a name="zh-cn_topic_0078078071_p17751193692311"></a><a name="zh-cn_topic_0078078071_p17751193692311"></a>32,768～18,446,744,073,709,551,615</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p18751123622314"><a name="zh-cn_topic_0078078071_p18751123622314"></a><a name="zh-cn_topic_0078078071_p18751123622314"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1375133632311"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p3752133610238"><a name="zh-cn_topic_0078078071_p3752133610238"></a><a name="zh-cn_topic_0078078071_p3752133610238"></a>sync_binlog</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p47521736102318"><a name="zh-cn_topic_0078078071_p47521736102318"></a><a name="zh-cn_topic_0078078071_p47521736102318"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p1075243602311"><a name="zh-cn_topic_0078078071_p1075243602311"></a><a name="zh-cn_topic_0078078071_p1075243602311"></a>0～4,294,967,295</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p175253612318"><a name="zh-cn_topic_0078078071_p175253612318"></a><a name="zh-cn_topic_0078078071_p175253612318"></a>否</p>
    </td>
    </tr>
    </tbody>
    </table>

    **表 7**  MySQL5.7参数列表

    <a name="zh-cn_topic_0078078071_table122391643123118"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0078078071_row623919434313"><th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.1"><p id="zh-cn_topic_0078078071_p3239144343116"><a name="zh-cn_topic_0078078071_p3239144343116"></a><a name="zh-cn_topic_0078078071_p3239144343116"></a><strong id="zh-cn_topic_0078078071_b3239243133117"><a name="zh-cn_topic_0078078071_b3239243133117"></a><a name="zh-cn_topic_0078078071_b3239243133117"></a>参数名称</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.2"><p id="zh-cn_topic_0078078071_p923914383120"><a name="zh-cn_topic_0078078071_p923914383120"></a><a name="zh-cn_topic_0078078071_p923914383120"></a><strong id="zh-cn_topic_0078078071_b192399434315"><a name="zh-cn_topic_0078078071_b192399434315"></a><a name="zh-cn_topic_0078078071_b192399434315"></a>参数类型</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.3"><p id="zh-cn_topic_0078078071_p182392043113116"><a name="zh-cn_topic_0078078071_p182392043113116"></a><a name="zh-cn_topic_0078078071_p182392043113116"></a><strong id="zh-cn_topic_0078078071_b16240144333114"><a name="zh-cn_topic_0078078071_b16240144333114"></a><a name="zh-cn_topic_0078078071_b16240144333114"></a>可选值</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.4"><p id="zh-cn_topic_0078078071_p2024013438319"><a name="zh-cn_topic_0078078071_p2024013438319"></a><a name="zh-cn_topic_0078078071_p2024013438319"></a><strong id="zh-cn_topic_0078078071_b6240204303110"><a name="zh-cn_topic_0078078071_b6240204303110"></a><a name="zh-cn_topic_0078078071_b6240204303110"></a>是否需要重启</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0078078071_row1124024383118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p92401143203110"><a name="zh-cn_topic_0078078071_p92401143203110"></a><a name="zh-cn_topic_0078078071_p92401143203110"></a>connect_timeout</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p1224012436312"><a name="zh-cn_topic_0078078071_p1224012436312"></a><a name="zh-cn_topic_0078078071_p1224012436312"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p6240843103117"><a name="zh-cn_topic_0078078071_p6240843103117"></a><a name="zh-cn_topic_0078078071_p6240843103117"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p4240943123118"><a name="zh-cn_topic_0078078071_p4240943123118"></a><a name="zh-cn_topic_0078078071_p4240943123118"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1424016433318"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1240204310311"><a name="zh-cn_topic_0078078071_p1240204310311"></a><a name="zh-cn_topic_0078078071_p1240204310311"></a>event_scheduler</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p10240184363116"><a name="zh-cn_topic_0078078071_p10240184363116"></a><a name="zh-cn_topic_0078078071_p10240184363116"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p224011433311"><a name="zh-cn_topic_0078078071_p224011433311"></a><a name="zh-cn_topic_0078078071_p224011433311"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p62405432319"><a name="zh-cn_topic_0078078071_p62405432319"></a><a name="zh-cn_topic_0078078071_p62405432319"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row19240543193115"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p2240164313119"><a name="zh-cn_topic_0078078071_p2240164313119"></a><a name="zh-cn_topic_0078078071_p2240164313119"></a>innodb_lock_wait_timeout</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p1124044363118"><a name="zh-cn_topic_0078078071_p1124044363118"></a><a name="zh-cn_topic_0078078071_p1124044363118"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p12241154383118"><a name="zh-cn_topic_0078078071_p12241154383118"></a><a name="zh-cn_topic_0078078071_p12241154383118"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p162414435313"><a name="zh-cn_topic_0078078071_p162414435313"></a><a name="zh-cn_topic_0078078071_p162414435313"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1324111438316"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p624115431319"><a name="zh-cn_topic_0078078071_p624115431319"></a><a name="zh-cn_topic_0078078071_p624115431319"></a>max_connections</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p22411743183111"><a name="zh-cn_topic_0078078071_p22411743183111"></a><a name="zh-cn_topic_0078078071_p22411743183111"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p124164311312"><a name="zh-cn_topic_0078078071_p124164311312"></a><a name="zh-cn_topic_0078078071_p124164311312"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p13241154317319"><a name="zh-cn_topic_0078078071_p13241154317319"></a><a name="zh-cn_topic_0078078071_p13241154317319"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row13241174353111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p5241204313314"><a name="zh-cn_topic_0078078071_p5241204313314"></a><a name="zh-cn_topic_0078078071_p5241204313314"></a>net_read_timeout</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p12241144343110"><a name="zh-cn_topic_0078078071_p12241144343110"></a><a name="zh-cn_topic_0078078071_p12241144343110"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p202411743133120"><a name="zh-cn_topic_0078078071_p202411743133120"></a><a name="zh-cn_topic_0078078071_p202411743133120"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1824164313312"><a name="zh-cn_topic_0078078071_p1824164313312"></a><a name="zh-cn_topic_0078078071_p1824164313312"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row182410431315"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1024164373117"><a name="zh-cn_topic_0078078071_p1024164373117"></a><a name="zh-cn_topic_0078078071_p1024164373117"></a>net_write_timeout</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p15241443163112"><a name="zh-cn_topic_0078078071_p15241443163112"></a><a name="zh-cn_topic_0078078071_p15241443163112"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p132416434314"><a name="zh-cn_topic_0078078071_p132416434314"></a><a name="zh-cn_topic_0078078071_p132416434314"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1824220432317"><a name="zh-cn_topic_0078078071_p1824220432317"></a><a name="zh-cn_topic_0078078071_p1824220432317"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1624215432310"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p62429433313"><a name="zh-cn_topic_0078078071_p62429433313"></a><a name="zh-cn_topic_0078078071_p62429433313"></a>explicit_defaults_for_timestamp</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p1124294383112"><a name="zh-cn_topic_0078078071_p1124294383112"></a><a name="zh-cn_topic_0078078071_p1124294383112"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p62421043163114"><a name="zh-cn_topic_0078078071_p62421043163114"></a><a name="zh-cn_topic_0078078071_p62421043163114"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p17242114313115"><a name="zh-cn_topic_0078078071_p17242114313115"></a><a name="zh-cn_topic_0078078071_p17242114313115"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row142421643163112"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p182427437318"><a name="zh-cn_topic_0078078071_p182427437318"></a><a name="zh-cn_topic_0078078071_p182427437318"></a>innodb_flush_log_at_trx_commit</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p11242194353112"><a name="zh-cn_topic_0078078071_p11242194353112"></a><a name="zh-cn_topic_0078078071_p11242194353112"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p162421943163114"><a name="zh-cn_topic_0078078071_p162421943163114"></a><a name="zh-cn_topic_0078078071_p162421943163114"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1424234317315"><a name="zh-cn_topic_0078078071_p1424234317315"></a><a name="zh-cn_topic_0078078071_p1424234317315"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row224294313313"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p17243104318317"><a name="zh-cn_topic_0078078071_p17243104318317"></a><a name="zh-cn_topic_0078078071_p17243104318317"></a>max_allowed_packet</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p72432043173118"><a name="zh-cn_topic_0078078071_p72432043173118"></a><a name="zh-cn_topic_0078078071_p72432043173118"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p152431343143111"><a name="zh-cn_topic_0078078071_p152431343143111"></a><a name="zh-cn_topic_0078078071_p152431343143111"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p18243843153115"><a name="zh-cn_topic_0078078071_p18243843153115"></a><a name="zh-cn_topic_0078078071_p18243843153115"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row824312432310"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p82437435311"><a name="zh-cn_topic_0078078071_p82437435311"></a><a name="zh-cn_topic_0078078071_p82437435311"></a>tx_isolation</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p424316434316"><a name="zh-cn_topic_0078078071_p424316434316"></a><a name="zh-cn_topic_0078078071_p424316434316"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p824334313113"><a name="zh-cn_topic_0078078071_p824334313113"></a><a name="zh-cn_topic_0078078071_p824334313113"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1724454318315"><a name="zh-cn_topic_0078078071_p1724454318315"></a><a name="zh-cn_topic_0078078071_p1724454318315"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1924444319319"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p3244104314315"><a name="zh-cn_topic_0078078071_p3244104314315"></a><a name="zh-cn_topic_0078078071_p3244104314315"></a>character_set_client</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p824434373112"><a name="zh-cn_topic_0078078071_p824434373112"></a><a name="zh-cn_topic_0078078071_p824434373112"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p3244194318310"><a name="zh-cn_topic_0078078071_p3244194318310"></a><a name="zh-cn_topic_0078078071_p3244194318310"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1224484383112"><a name="zh-cn_topic_0078078071_p1224484383112"></a><a name="zh-cn_topic_0078078071_p1224484383112"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row92442437313"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p4244343183111"><a name="zh-cn_topic_0078078071_p4244343183111"></a><a name="zh-cn_topic_0078078071_p4244343183111"></a>character_set_connection</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p3244543183119"><a name="zh-cn_topic_0078078071_p3244543183119"></a><a name="zh-cn_topic_0078078071_p3244543183119"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p19245154310318"><a name="zh-cn_topic_0078078071_p19245154310318"></a><a name="zh-cn_topic_0078078071_p19245154310318"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1824574343114"><a name="zh-cn_topic_0078078071_p1824574343114"></a><a name="zh-cn_topic_0078078071_p1824574343114"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row8245124310316"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1124513431311"><a name="zh-cn_topic_0078078071_p1124513431311"></a><a name="zh-cn_topic_0078078071_p1124513431311"></a>collation_connection</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p1224534323112"><a name="zh-cn_topic_0078078071_p1224534323112"></a><a name="zh-cn_topic_0078078071_p1224534323112"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p202451543183111"><a name="zh-cn_topic_0078078071_p202451543183111"></a><a name="zh-cn_topic_0078078071_p202451543183111"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1624514436315"><a name="zh-cn_topic_0078078071_p1624514436315"></a><a name="zh-cn_topic_0078078071_p1624514436315"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row122456430315"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1224612437316"><a name="zh-cn_topic_0078078071_p1224612437316"></a><a name="zh-cn_topic_0078078071_p1224612437316"></a>character_set_results</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p1024620434314"><a name="zh-cn_topic_0078078071_p1024620434314"></a><a name="zh-cn_topic_0078078071_p1024620434314"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p14246943173110"><a name="zh-cn_topic_0078078071_p14246943173110"></a><a name="zh-cn_topic_0078078071_p14246943173110"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p22461443133112"><a name="zh-cn_topic_0078078071_p22461443133112"></a><a name="zh-cn_topic_0078078071_p22461443133112"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row62464436310"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p824674323110"><a name="zh-cn_topic_0078078071_p824674323110"></a><a name="zh-cn_topic_0078078071_p824674323110"></a>collation_server</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p15246184314316"><a name="zh-cn_topic_0078078071_p15246184314316"></a><a name="zh-cn_topic_0078078071_p15246184314316"></a>常规参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p162462043203113"><a name="zh-cn_topic_0078078071_p162462043203113"></a><a name="zh-cn_topic_0078078071_p162462043203113"></a>-</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1424714434315"><a name="zh-cn_topic_0078078071_p1424714434315"></a><a name="zh-cn_topic_0078078071_p1424714434315"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row2024734343116"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p13247194318317"><a name="zh-cn_topic_0078078071_p13247194318317"></a><a name="zh-cn_topic_0078078071_p13247194318317"></a>binlog_cache_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p142479436316"><a name="zh-cn_topic_0078078071_p142479436316"></a><a name="zh-cn_topic_0078078071_p142479436316"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p8247843123117"><a name="zh-cn_topic_0078078071_p8247843123117"></a><a name="zh-cn_topic_0078078071_p8247843123117"></a>4,096～18,446,744,073,709,547,520</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p52481843123115"><a name="zh-cn_topic_0078078071_p52481843123115"></a><a name="zh-cn_topic_0078078071_p52481843123115"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row5248114353114"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p132483434318"><a name="zh-cn_topic_0078078071_p132483434318"></a><a name="zh-cn_topic_0078078071_p132483434318"></a>binlog_stmt_cache_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p324874318315"><a name="zh-cn_topic_0078078071_p324874318315"></a><a name="zh-cn_topic_0078078071_p324874318315"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p42491843143113"><a name="zh-cn_topic_0078078071_p42491843143113"></a><a name="zh-cn_topic_0078078071_p42491843143113"></a>4,096～18,446,744,073,709,547,520</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p11249843193120"><a name="zh-cn_topic_0078078071_p11249843193120"></a><a name="zh-cn_topic_0078078071_p11249843193120"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row182491443123112"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p2249144315318"><a name="zh-cn_topic_0078078071_p2249144315318"></a><a name="zh-cn_topic_0078078071_p2249144315318"></a>bulk_insert_buffer_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p192507436316"><a name="zh-cn_topic_0078078071_p192507436316"></a><a name="zh-cn_topic_0078078071_p192507436316"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p102501643193111"><a name="zh-cn_topic_0078078071_p102501643193111"></a><a name="zh-cn_topic_0078078071_p102501643193111"></a>0～18,446,744,073,709,551,615</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p5250443123111"><a name="zh-cn_topic_0078078071_p5250443123111"></a><a name="zh-cn_topic_0078078071_p5250443123111"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row15250843133113"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p17250543173113"><a name="zh-cn_topic_0078078071_p17250543173113"></a><a name="zh-cn_topic_0078078071_p17250543173113"></a>innodb_buffer_pool_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p4250194303112"><a name="zh-cn_topic_0078078071_p4250194303112"></a><a name="zh-cn_topic_0078078071_p4250194303112"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p39591535331"><a name="zh-cn_topic_0078078071_p39591535331"></a><a name="zh-cn_topic_0078078071_p39591535331"></a>536,870,912～18,446,744,073,709,551,615</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1725112433315"><a name="zh-cn_topic_0078078071_p1725112433315"></a><a name="zh-cn_topic_0078078071_p1725112433315"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1525144383113"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1025114317312"><a name="zh-cn_topic_0078078071_p1025114317312"></a><a name="zh-cn_topic_0078078071_p1025114317312"></a>key_buffer_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p1325184315315"><a name="zh-cn_topic_0078078071_p1325184315315"></a><a name="zh-cn_topic_0078078071_p1325184315315"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p625114433310"><a name="zh-cn_topic_0078078071_p625114433310"></a><a name="zh-cn_topic_0078078071_p625114433310"></a>8～9,223,372,036,854,771,712</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p19251643133117"><a name="zh-cn_topic_0078078071_p19251643133117"></a><a name="zh-cn_topic_0078078071_p19251643133117"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1525134383111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p525118436312"><a name="zh-cn_topic_0078078071_p525118436312"></a><a name="zh-cn_topic_0078078071_p525118436312"></a>long_query_time</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p62511843133112"><a name="zh-cn_topic_0078078071_p62511843133112"></a><a name="zh-cn_topic_0078078071_p62511843133112"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p225114373113"><a name="zh-cn_topic_0078078071_p225114373113"></a><a name="zh-cn_topic_0078078071_p225114373113"></a>0～3,600</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p122523437311"><a name="zh-cn_topic_0078078071_p122523437311"></a><a name="zh-cn_topic_0078078071_p122523437311"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row18252184363117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1925254363111"><a name="zh-cn_topic_0078078071_p1925254363111"></a><a name="zh-cn_topic_0078078071_p1925254363111"></a>query_cache_type</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p20252143183120"><a name="zh-cn_topic_0078078071_p20252143183120"></a><a name="zh-cn_topic_0078078071_p20252143183120"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p72524436310"><a name="zh-cn_topic_0078078071_p72524436310"></a><a name="zh-cn_topic_0078078071_p72524436310"></a>OFF, ON, DEMAND</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p1025217439312"><a name="zh-cn_topic_0078078071_p1025217439312"></a><a name="zh-cn_topic_0078078071_p1025217439312"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row4252194319313"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p1425224319312"><a name="zh-cn_topic_0078078071_p1425224319312"></a><a name="zh-cn_topic_0078078071_p1425224319312"></a>read_buffer_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p1325214432312"><a name="zh-cn_topic_0078078071_p1325214432312"></a><a name="zh-cn_topic_0078078071_p1325214432312"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p172521043133116"><a name="zh-cn_topic_0078078071_p172521043133116"></a><a name="zh-cn_topic_0078078071_p172521043133116"></a>8,192～2,147,479,552</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p0253204313113"><a name="zh-cn_topic_0078078071_p0253204313113"></a><a name="zh-cn_topic_0078078071_p0253204313113"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row9253154320311"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p16253194319315"><a name="zh-cn_topic_0078078071_p16253194319315"></a><a name="zh-cn_topic_0078078071_p16253194319315"></a>read_rnd_buffer_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p132534439317"><a name="zh-cn_topic_0078078071_p132534439317"></a><a name="zh-cn_topic_0078078071_p132534439317"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p20253194310317"><a name="zh-cn_topic_0078078071_p20253194310317"></a><a name="zh-cn_topic_0078078071_p20253194310317"></a>1～2,147,483,647</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p3253543163117"><a name="zh-cn_topic_0078078071_p3253543163117"></a><a name="zh-cn_topic_0078078071_p3253543163117"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row1625384320315"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p2253184313119"><a name="zh-cn_topic_0078078071_p2253184313119"></a><a name="zh-cn_topic_0078078071_p2253184313119"></a>sort_buffer_size</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p11253743143115"><a name="zh-cn_topic_0078078071_p11253743143115"></a><a name="zh-cn_topic_0078078071_p11253743143115"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p112541343203115"><a name="zh-cn_topic_0078078071_p112541343203115"></a><a name="zh-cn_topic_0078078071_p112541343203115"></a>32,768～18,446,744,073,709,551,615</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p152543430316"><a name="zh-cn_topic_0078078071_p152543430316"></a><a name="zh-cn_topic_0078078071_p152543430316"></a>否</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row19254114343120"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="zh-cn_topic_0078078071_p72541943103114"><a name="zh-cn_topic_0078078071_p72541943103114"></a><a name="zh-cn_topic_0078078071_p72541943103114"></a>sync_binlog</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="zh-cn_topic_0078078071_p3254114393116"><a name="zh-cn_topic_0078078071_p3254114393116"></a><a name="zh-cn_topic_0078078071_p3254114393116"></a>性能参数</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="zh-cn_topic_0078078071_p4254184316317"><a name="zh-cn_topic_0078078071_p4254184316317"></a><a name="zh-cn_topic_0078078071_p4254184316317"></a>0～4,294,967,295</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="zh-cn_topic_0078078071_p112547433315"><a name="zh-cn_topic_0078078071_p112547433315"></a><a name="zh-cn_topic_0078078071_p112547433315"></a>否</p>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   目前仅MySQL数据库迁移支持参数对比的功能。  
    >-   对于上述参数“innodb\_buffer\_pool\_size”，参数对比功能对应用到目标数据库的值做了内控，最大不会超过目标数据库总内存的70%。所以有时候是无法完全和源数据库该参数取值一致，这是为了避免目标数据库设置过大，而导致数据库无法启动，如果您觉得上述最大值偏小，可以在数据库中通过执行命令手动设置更大的值。  

    参数对比操作完成后，单击“下一步”。

7.  在“任务确认“页面，设置迁移任务的启动时间，并确认迁移任务信息无误后，勾选协议，单击“启动任务“，提交迁移任务。

    **图 8**  任务确认-VPN（专线）<a name="fig2736101920515"></a>  
    ![](figures/任务确认-VPN（专线）.png "任务确认-VPN（专线）")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >当目标数据库版本为MySQL5.6且进行增量迁移时，在启动任务过程中目标数据库将被重启一次，可能会中断数据库业务的使用。  

8.  迁移任务提交后，您可在“在线迁移管理“页面，查看并管理自己的任务。
    -   您可查看任务提交后的状态，状态请参见[任务状态](zh-cn_topic_0082317249.md)。
    -   在任务列表的右上角，单击![](figures/kwx318612-GAUSS-DBaaS-image-a8fbc7b6-eab2-4798-b522-174e36341a92-0.png)刷新列表，可查看到最新的任务状态。

9.  迁移任务创建成功后，请参见《数据复制服务快速入门》的[使用流程](https://support.huaweicloud.com/qs-drs/drs_02_0001.html)，进行完整的数据业务割接。


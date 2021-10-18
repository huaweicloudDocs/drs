# 分片集群MongoDB数据库迁移至DDS社区版集群<a name="drs_03_0103"></a>

在数据复制服务中，数据库迁移是通过任务的形式完成的，通过创建任务向导，可以完成任务信息配置、任务创建。迁移任务创建成功后，您也可以通过数据复制服务管理控制台，对任务进行管理。

本章节将以MongoDB分片集群为示例，介绍在公网网络场景下，通过数据复制服务管理控制台配置MongoDB数据迁移任务的流程。其中，MongoDB分片集群到DDS增强版集群的迁移与该场景的配置流程类似。

## 前提条件<a name="section148240813206"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   参见[实时迁移](https://support.huaweicloud.com/productdesc-drs/drs_01_0301.html)。
-   参见[使用须知](https://support.huaweicloud.com/qs-drs/drs_online_migration.html)。

## 操作步骤<a name="section382023131718"></a>

1.  在“实时迁移管理“页面，单击“创建迁移任务“，进入创建迁移任务页面。
2.  在“迁移实例”页面，填选区域、任务名称、任务异常通知设置、SMN主题、时延阈值、任务异常自动结束时间、描述、迁移实例信息，单击“下一步”。

    **图 1**  迁移任务信息<a name="fig12135172055911"></a>  
    ![](figures/迁移任务信息.png "迁移任务信息")

    **表 1**  任务和描述

    <a name="table1568151543618"></a>
    <table><thead align="left"><tr id="drs_02_0021_drs_02_0002_row55731924204420"><th class="cellrowborder" valign="top" width="18.42%" id="mcps1.2.3.1.1"><p id="drs_02_0021_drs_02_0002_p17991967204420"><a name="drs_02_0021_drs_02_0002_p17991967204420"></a><a name="drs_02_0021_drs_02_0002_p17991967204420"></a><strong id="drs_02_0021_drs_02_0002_b1611223511352"><a name="drs_02_0021_drs_02_0002_b1611223511352"></a><a name="drs_02_0021_drs_02_0002_b1611223511352"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="81.58%" id="mcps1.2.3.1.2"><p id="drs_02_0021_drs_02_0002_p48063227204420"><a name="drs_02_0021_drs_02_0002_p48063227204420"></a><a name="drs_02_0021_drs_02_0002_p48063227204420"></a><strong id="drs_02_0021_drs_02_0002_b3002268111352"><a name="drs_02_0021_drs_02_0002_b3002268111352"></a><a name="drs_02_0021_drs_02_0002_b3002268111352"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="drs_02_0021_drs_02_0002_row12620182813359"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="drs_02_0021_drs_02_0002_p86211228113513"><a name="drs_02_0021_drs_02_0002_p86211228113513"></a><a name="drs_02_0021_drs_02_0002_p86211228113513"></a>区域</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="drs_02_0021_drs_02_0002_p462118281358"><a name="drs_02_0021_drs_02_0002_p462118281358"></a><a name="drs_02_0021_drs_02_0002_p462118281358"></a>当前所在区域，可进行切换。</p>
    </td>
    </tr>
    <tr id="drs_02_0021_drs_02_0002_row807311204420"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="drs_02_0021_drs_02_0002_p65392260204420"><a name="drs_02_0021_drs_02_0002_p65392260204420"></a><a name="drs_02_0021_drs_02_0002_p65392260204420"></a>任务名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="drs_02_0021_drs_02_0002_p62281730204420"><a name="drs_02_0021_drs_02_0002_p62281730204420"></a><a name="drs_02_0021_drs_02_0002_p62281730204420"></a>任务名称在4-50位之间，必须以字母开头，不区分大小写，可以包含字母、数字、中划线或下划线，不能包含其他的特殊字符。</p>
    </td>
    </tr>
    <tr id="drs_02_0021_drs_02_0002_row36111933161119"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="drs_02_0021_drs_02_0002_p1743564414119"><a name="drs_02_0021_drs_02_0002_p1743564414119"></a><a name="drs_02_0021_drs_02_0002_p1743564414119"></a>描述</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="drs_02_0021_drs_02_0002_p1758045719117"><a name="drs_02_0021_drs_02_0002_p1758045719117"></a><a name="drs_02_0021_drs_02_0002_p1758045719117"></a>描述不能超过256位，且不能包含! = &lt; &gt; &amp; ' " \ 特殊字符。</p>
    </td>
    </tr>
    <tr id="drs_02_0021_drs_02_0002_row1080215433911"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="drs_02_0021_drs_02_0002_p158027493912"><a name="drs_02_0021_drs_02_0002_p158027493912"></a><a name="drs_02_0021_drs_02_0002_p158027493912"></a>任务异常通知设置</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="drs_02_0021_drs_02_0002_p38891258184013"><a name="drs_02_0021_drs_02_0002_p38891258184013"></a><a name="drs_02_0021_drs_02_0002_p38891258184013"></a>该项为可选参数，开启之后，选择对应的SMN主题。当迁移任务状态异常时，系统将发送通知。</p>
    </td>
    </tr>
    <tr id="drs_02_0021_drs_02_0002_row1360111041213"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="drs_02_0021_drs_02_0002_p2036111017129"><a name="drs_02_0021_drs_02_0002_p2036111017129"></a><a name="drs_02_0021_drs_02_0002_p2036111017129"></a>SMN主题</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="drs_02_0021_drs_02_0002_p17361121081210"><a name="drs_02_0021_drs_02_0002_p17361121081210"></a><a name="drs_02_0021_drs_02_0002_p17361121081210"></a><span class="uicontrol" id="drs_02_0021_drs_02_0002_uicontrol83037419162"><a name="drs_02_0021_drs_02_0002_uicontrol83037419162"></a><a name="drs_02_0021_drs_02_0002_uicontrol83037419162"></a>“任务异常通知设置”</span>项开启后可见，需提前在SMN上申请主题并添加订阅。</p>
    <p id="drs_02_0021_drs_02_0002_p127491315171714"><a name="drs_02_0021_drs_02_0002_p127491315171714"></a><a name="drs_02_0021_drs_02_0002_p127491315171714"></a>SMN主题申请和订阅可参考<a href="https://support.huaweicloud.com/qs-smn/smn_ug_0004.html" target="_blank" rel="noopener noreferrer">《消息通知服务用户指南》</a>。</p>
    </td>
    </tr>
    <tr id="drs_02_0021_drs_02_0002_row157731032102814"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="drs_02_0021_drs_02_0002_p1677373232818"><a name="drs_02_0021_drs_02_0002_p1677373232818"></a><a name="drs_02_0021_drs_02_0002_p1677373232818"></a>时延阈值</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="drs_02_0021_drs_02_0002_p6681185532914"><a name="drs_02_0021_drs_02_0002_p6681185532914"></a><a name="drs_02_0021_drs_02_0002_p6681185532914"></a>在增量迁移阶段，源数据库和目标数据库之间的<span id="drs_02_0021_drs_02_0002_text1977624058"><a name="drs_02_0021_drs_02_0002_text1977624058"></a><a name="drs_02_0021_drs_02_0002_text1977624058"></a>实时同步</span>有时会存在一个时间差，称为时延，单位为秒。</p>
    <p id="drs_02_0021_drs_02_0002_p75251915133018"><a name="drs_02_0021_drs_02_0002_p75251915133018"></a><a name="drs_02_0021_drs_02_0002_p75251915133018"></a>时延阈值设置是指时延超过一定的值后（时延阈值范围为1—3600s），DRS可以发送告警通知给指定收件人。告警通知将在时延稳定超过设定的阈值6min后发送，避免出现由于时延波动反复发送告警通知的情况。</p>
    <div class="note" id="drs_02_0021_drs_02_0002_note47298209309"><a name="drs_02_0021_drs_02_0002_note47298209309"></a><a name="drs_02_0021_drs_02_0002_note47298209309"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="drs_02_0021_drs_02_0002_ul167113217818"></a><a name="drs_02_0021_drs_02_0002_ul167113217818"></a><ul id="drs_02_0021_drs_02_0002_ul167113217818"><li>首次进入增量迁移阶段，会有较多数据等待同步，存在较大的时延，属于正常情况，不在此功能的监控范围之内。</li><li>设置时延阈值之前，需要设置任务异常通知。</li></ul>
    </div></div>
    </td>
    </tr>
    <tr id="drs_02_0021_drs_02_0002_row188817390433"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="drs_02_0021_drs_02_0002_p1192225794312"><a name="drs_02_0021_drs_02_0002_p1192225794312"></a><a name="drs_02_0021_drs_02_0002_p1192225794312"></a>任务异常自动结束时间（天）</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="drs_02_0021_drs_02_0002_p1312634214561"><a name="drs_02_0021_drs_02_0002_p1312634214561"></a><a name="drs_02_0021_drs_02_0002_p1312634214561"></a>设置任务异常自动结束天数，输入值必须在14-100之间。</p>
    <div class="note" id="drs_02_0021_drs_02_0002_note115651218193116"><a name="drs_02_0021_drs_02_0002_note115651218193116"></a><a name="drs_02_0021_drs_02_0002_note115651218193116"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="drs_02_0021_drs_02_0002_p1956521816315"><a name="drs_02_0021_drs_02_0002_p1956521816315"></a><a name="drs_02_0021_drs_02_0002_p1956521816315"></a>异常状态下的任务仍然会计费，而长时间异常的任务无法续传和恢复。设置任务异常自动结束天数后，异常且超时的任务将会自动结束，以免产生不必要的费用。</p>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

    **图 2**  MongoDB迁移实例信息<a name="fig6487192516156"></a>  
    ![](figures/MongoDB迁移实例信息.png "MongoDB迁移实例信息")

    **表 2**  迁移实例信息

    <a name="table54580728204436"></a>
    <table><thead align="left"><tr id="row39932329204436"><th class="cellrowborder" valign="top" width="23.87%" id="mcps1.2.3.1.1"><p id="p13293221204436"><a name="p13293221204436"></a><a name="p13293221204436"></a><strong id="b2587841611355"><a name="b2587841611355"></a><a name="b2587841611355"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.13%" id="mcps1.2.3.1.2"><p id="p3009113204436"><a name="p3009113204436"></a><a name="p3009113204436"></a><strong id="b1577696211355"><a name="b1577696211355"></a><a name="b1577696211355"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row695184962111"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p951443871218"><a name="p951443871218"></a><a name="p951443871218"></a>数据流动方向</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p11514173891212"><a name="p11514173891212"></a><a name="p11514173891212"></a>选择入云。</p>
    <p id="p1983838136"><a name="p1983838136"></a><a name="p1983838136"></a>入云指目标端数据库为本云数据库。</p>
    </td>
    </tr>
    <tr id="row0414184610580"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1414046115813"><a name="p1414046115813"></a><a name="p1414046115813"></a>源数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p14557101913243"><a name="p14557101913243"></a><a name="p14557101913243"></a>选择MongoDB。</p>
    </td>
    </tr>
    <tr id="row42411630204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p12790028204436"><a name="p12790028204436"></a><a name="p12790028204436"></a>目标数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p2322512258"><a name="p2322512258"></a><a name="p2322512258"></a>选择DDS。</p>
    </td>
    </tr>
    <tr id="row62907306204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p62327044204436"><a name="p62327044204436"></a><a name="p62327044204436"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p15325794204436"><a name="p15325794204436"></a><a name="p15325794204436"></a>默认为公网网络类型，可按照需求选择VPC网络、VPN网络、专线网络、公网网络。</p>
    <a name="ul1872454917306"></a><a name="ul1872454917306"></a><ul id="ul1872454917306"><li>VPC网络：适合云上数据库之间的迁移。</li><li>公网网络：适合通过公网网络把其他云下或其他平台的数据库迁移到目标数据库，该类型要求目标数据库绑定弹性公网IP（EIP）。</li><li>VPN网络：适合通过VPN网络，实现其他云下自建数据库与云上数据库迁移、或云上跨Region的数据库之间的迁移。</li><li>专线网络：适合通过专线网络，实现其他云下自建数据库与云上数据库迁移、或云上跨Region的数据库之间的迁移。<div class="note" id="note1139512933914"><a name="note1139512933914"></a><a name="note1139512933914"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p1039622910397"><a name="p1039622910397"></a><a name="p1039622910397"></a>分片集群的全量+增量迁移目前不支持选择VPC网络。</p>
    </div></div>
    </li></ul>
    </td>
    </tr>
    <tr id="row658644204515"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p53350183204515"><a name="p53350183204515"></a><a name="p53350183204515"></a>目标数据库实例</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p26397538204515"><a name="p26397538204515"></a><a name="p26397538204515"></a>用户所创建的目标数据库实例。</p>
    </td>
    </tr>
    <tr id="row117172513514"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p01021256155315"><a name="p01021256155315"></a><a name="p01021256155315"></a>迁移实例所在子网</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p18102456175315"><a name="p18102456175315"></a><a name="p18102456175315"></a>选择迁移实例所在的子网。也可以单击“查看子网”，跳转至“网络控制台”查看实例所在子网帮助选择。</p>
    <p id="p151791531292"><a name="p151791531292"></a><a name="p151791531292"></a>默认值为当前所选数据库实例所在子网，请选择有可用IP地址的子网。为确保迁移实例创建成功，仅显示已经开启DHCP的子网。</p>
    </td>
    </tr>
    <tr id="row0850133715295"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p128192616518"><a name="p128192616518"></a><a name="p128192616518"></a>迁移模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><a name="ul171919713019"></a><a name="ul171919713019"></a><ul id="ul171919713019"><li>全量：该模式为数据库一次性迁移，适用于可中断业务的数据库迁移场景，全量迁移将非系统数据库的全部数据库对象和数据一次性迁移至目标端数据库，包括：集合、索引等。<div class="note" id="note1989394717302"><a name="note1989394717302"></a><a name="note1989394717302"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p12614191914218"><a name="p12614191914218"></a><a name="p12614191914218"></a>如果用户只进行全量迁移时，建议停止对源数据库的操作，否则迁移过程中源数据库产生的新数据不会同步到目标数据库。</p>
    </div></div>
    </li><li>全量+增量：该模式为数据库持续性迁移，适用于对业务中断敏感的场景，通过全量迁移过程中完成的目标端数据库的初始化后，增量迁移阶段通过解析日志等技术，将源端和目标端数据库保持数据持续一致。</li></ul>
    <div class="note" id="note3814342165119"><a name="note3814342165119"></a><a name="note3814342165119"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p118141442205110"><a name="p118141442205110"></a><a name="p118141442205110"></a>选择<span class="uicontrol" id="uicontrol24738122117"><a name="uicontrol24738122117"></a><a name="uicontrol24738122117"></a>“全量+增量”</span>迁移模式，增量迁移可以在全量迁移完成的基础上实现数据的持续同步，无需中断业务，实现迁移过程中源业务和数据库继续对外提供访问。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row385355610516"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p98542056105112"><a name="p98542056105112"></a><a name="p98542056105112"></a>源数据库实例类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p7854456195116"><a name="p7854456195116"></a><a name="p7854456195116"></a>需要根据源数据库的具体来源进行设置。</p>
    <a name="ul4879338807"></a><a name="ul4879338807"></a><ul id="ul4879338807"><li>当源库类型属于集群时，该项需要设置为集群</li><li>当源库类型属于副本集或者单节点时，该项需要设置为非集群。</li><li>当源库类型为MongDB集群4.0及以上版本，集群实例无法获取到分片节点的IP时，可选择集群(MongoDB 4.0+)。</li></ul>
    </td>
    </tr>
    <tr id="row208952593510"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p28953594518"><a name="p28953594518"></a><a name="p28953594518"></a>源端分片个数</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p78951459175118"><a name="p78951459175118"></a><a name="p78951459175118"></a>当源端实例类型设置为“集群”时，需要填写源端数据库实例个数。</p>
    <p id="p14946142295819"><a name="p14946142295819"></a><a name="p14946142295819"></a>源端数据库实例个数默认最小值为2，最大值为32，你需要根据源库实际的集群分片个数设置该值大小。</p>
    </td>
    </tr>
    <tr id="row112391118191011"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p5127124111179"><a name="p5127124111179"></a><a name="p5127124111179"></a>企业项目</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p13502591186"><a name="p13502591186"></a><a name="p13502591186"></a>对于已成功关联企业项目的用户，仅需在“企业项目”下拉框中选择目标项目。</p>
    <p id="p1350279131815"><a name="p1350279131815"></a><a name="p1350279131815"></a>如果需要自定义企业项目，请前往项目管理服务进行创建。关于如何创建项目，详见《项目管理用户指南》。</p>
    </td>
    </tr>
    <tr id="row15731813101013"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p14235145217372"><a name="p14235145217372"></a><a name="p14235145217372"></a>标签</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p27631913145915"><a name="p27631913145915"></a><a name="p27631913145915"></a>可选配置，对迁移任务的标识。使用标签可方便管理您的迁移任务。每个任务最多支持10个标签配额。</p>
    <p id="p99775219218"><a name="p99775219218"></a><a name="p99775219218"></a>任务创建成功后，您可以单击实例名称，在<span class="uicontrol" id="uicontrol1433412554316"><a name="uicontrol1433412554316"></a><a name="uicontrol1433412554316"></a>“标签”</span>页签下查看对应标签。关于标签的详细操作，请参见<a href="https://support.huaweicloud.com/usermanual-drs/drs_online_tag.html" target="_blank" rel="noopener noreferrer">标签管理</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，迁移实例创建成功后，填选源库信息和目标库信息，建议您单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，勾选协议，单击“下一步“。

    **图 3**  源库MongoDB信息页面<a name="zh-cn_topic_0135097933_fig136531923115918"></a>  
    ![](figures/源库MongoDB信息页面.png "源库MongoDB信息页面")

    **表 3**  源库信息

    <a name="zh-cn_topic_0135097933_table1665310232597"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0135097933_row12653123195919"><th class="cellrowborder" valign="top" width="23.29%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0135097933_p156531623165916"><a name="zh-cn_topic_0135097933_p156531623165916"></a><a name="zh-cn_topic_0135097933_p156531623165916"></a><strong id="zh-cn_topic_0135097933_b20653923155913"><a name="zh-cn_topic_0135097933_b20653923155913"></a><a name="zh-cn_topic_0135097933_b20653923155913"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.71%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0135097933_p1365312365910"><a name="zh-cn_topic_0135097933_p1365312365910"></a><a name="zh-cn_topic_0135097933_p1365312365910"></a><strong id="zh-cn_topic_0135097933_b186531223105910"><a name="zh-cn_topic_0135097933_b186531223105910"></a><a name="zh-cn_topic_0135097933_b186531223105910"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0135097933_row1265352355912"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p1267813415714"><a name="p1267813415714"></a><a name="p1267813415714"></a>mongosIP地址或域名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p6215123031115"><a name="p6215123031115"></a><a name="p6215123031115"></a>源数据库的IP地址或域名，格式为IP地址/域名:端口。其中源数据库服务端口，可输入范围为1~65534间的整数。</p>
    <p id="zh-cn_topic_0135097933_p2653523145918"><a name="zh-cn_topic_0135097933_p2653523145918"></a><a name="zh-cn_topic_0135097933_p2653523145918"></a>该输入框最多支持填写3组源数据库的IP地址或者域名信息，多个值需要使用英文逗号隔开。例如：192.168.0.1:8080,192.168.0.2:8080。同时需要确保所填写的多个IP地址或域名属于同一个分片集群。</p>
    <div class="note" id="note66221243161214"><a name="note66221243161214"></a><a name="note66221243161214"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p1362214439121"><a name="p1362214439121"></a><a name="p1362214439121"></a>此处若填写的是多组IP地址或者域名信息，在进行测试连接的过程中，只要存在一组IP地址或者域名可以连通，那么测试连接就提示成功。所以需要您保证填写的IP地址或域名的正确性。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row104567257713"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p24576251077"><a name="p24576251077"></a><a name="p24576251077"></a>账号认证数据库</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p1645772510718"><a name="p1645772510718"></a><a name="p1645772510718"></a>填写的数据库账号所属的数据库名称。例如：华为云DDS实例默认的账号认证数据库为admin。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row9653102325913"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p4653162320598"><a name="zh-cn_topic_0135097933_p4653162320598"></a><a name="zh-cn_topic_0135097933_p4653162320598"></a>mongos用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p8653423135910"><a name="zh-cn_topic_0135097933_p8653423135910"></a><a name="zh-cn_topic_0135097933_p8653423135910"></a>源数据库的用户名。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row065352315596"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p86531023135911"><a name="zh-cn_topic_0135097933_p86531023135911"></a><a name="zh-cn_topic_0135097933_p86531023135911"></a>mongos密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p665318234591"><a name="zh-cn_topic_0135097933_p665318234591"></a><a name="zh-cn_topic_0135097933_p665318234591"></a>源数据库的用户名所对应的密码。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row26531923125912"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p2653112395910"><a name="zh-cn_topic_0135097933_p2653112395910"></a><a name="zh-cn_topic_0135097933_p2653112395910"></a>SSL安全连接</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p765310236599"><a name="zh-cn_topic_0135097933_p765310236599"></a><a name="zh-cn_topic_0135097933_p765310236599"></a>通过该功能，用户可以选择是否开启对迁移链路的加密。如果开启该功能，需要用户上传SSL CA根证书。</p>
    <div class="note" id="note174414299197"><a name="note174414299197"></a><a name="note174414299197"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul02071510191312"></a><a name="ul02071510191312"></a><ul id="ul02071510191312"><li>最大支持上传500KB的证书文件。</li><li>如果不使用SSL证书，请自行承担数据安全风险。</li></ul>
    </div></div>
    </td>
    </tr>
    <tr id="row3204554770"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p172044541177"><a name="p172044541177"></a><a name="p172044541177"></a>分片数据库</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p12044542711"><a name="p12044542711"></a><a name="p12044542711"></a>根据源库实际的集群分片个数，填写对应的分片数据库信息。</p>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >**源数据库的IP地址或域名、数据库用户名和密码，会被系统加密暂存，直至删除该迁移任务后自动清除。**

    -   目标库信息配置

        **图 4**  目标库DDS信息<a name="zh-cn_topic_0135097933_fig186534231595"></a>  
        ![](figures/目标库DDS信息.png "目标库DDS信息")

        **表 4**  目标库信息

        <a name="zh-cn_topic_0135097933_table157461610185911"></a>
        <table><thead align="left"><tr id="zh-cn_topic_0135097933_row15746151015912"><th class="cellrowborder" valign="top" width="23.02%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0135097933_p18746101055912"><a name="zh-cn_topic_0135097933_p18746101055912"></a><a name="zh-cn_topic_0135097933_p18746101055912"></a><strong id="zh-cn_topic_0135097933_b074631019593"><a name="zh-cn_topic_0135097933_b074631019593"></a><a name="zh-cn_topic_0135097933_b074631019593"></a>参数</strong></p>
        </th>
        <th class="cellrowborder" valign="top" width="76.98%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0135097933_p15746181055920"><a name="zh-cn_topic_0135097933_p15746181055920"></a><a name="zh-cn_topic_0135097933_p15746181055920"></a><strong id="zh-cn_topic_0135097933_b1774613108597"><a name="zh-cn_topic_0135097933_b1774613108597"></a><a name="zh-cn_topic_0135097933_b1774613108597"></a>描述</strong></p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="zh-cn_topic_0135097933_row0746151020595"><td class="cellrowborder" valign="top" width="23.02%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p1674610102597"><a name="zh-cn_topic_0135097933_p1674610102597"></a><a name="zh-cn_topic_0135097933_p1674610102597"></a>数据库实例名称</p>
        </td>
        <td class="cellrowborder" valign="top" width="76.98%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p3746710165918"><a name="zh-cn_topic_0135097933_p3746710165918"></a><a name="zh-cn_topic_0135097933_p3746710165918"></a>默认为创建迁移任务时选择的数据库实例，不可进行修改。</p>
        </td>
        </tr>
        <tr id="zh-cn_topic_0135097933_row2746310155916"><td class="cellrowborder" valign="top" width="23.02%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p18746310175911"><a name="zh-cn_topic_0135097933_p18746310175911"></a><a name="zh-cn_topic_0135097933_p18746310175911"></a>数据库用户名</p>
        </td>
        <td class="cellrowborder" valign="top" width="76.98%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p874691012591"><a name="zh-cn_topic_0135097933_p874691012591"></a><a name="zh-cn_topic_0135097933_p874691012591"></a>目标数据库对应的数据库用户名。</p>
        </td>
        </tr>
        <tr id="zh-cn_topic_0135097933_row107461010135910"><td class="cellrowborder" valign="top" width="23.02%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p47463101599"><a name="zh-cn_topic_0135097933_p47463101599"></a><a name="zh-cn_topic_0135097933_p47463101599"></a>数据库密码</p>
        </td>
        <td class="cellrowborder" valign="top" width="76.98%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p47461410155914"><a name="zh-cn_topic_0135097933_p47461410155914"></a><a name="zh-cn_topic_0135097933_p47461410155914"></a>目标数据库的登录密码。</p>
        </td>
        </tr>
        </tbody>
        </table>

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >**目标数据库的用户名和密码将在迁移过程中被加密暂存到数据库和迁移实例主机上，待该任务删除后会永久清除。**


4.  在“迁移设置“页面，设置迁移对象，单击“下一步“。

    **图 5**  设置迁移对象<a name="fig133579181217"></a>  
    ![](figures/设置迁移对象.png "设置迁移对象")

    **表 5**  迁移对象

    <a name="zh-cn_topic_0078078071_table165921932111919"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0078078071_row165921632141911"><th class="cellrowborder" valign="top" width="16.73%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0078078071_p1759233261916"><a name="zh-cn_topic_0078078071_p1759233261916"></a><a name="zh-cn_topic_0078078071_p1759233261916"></a><strong id="zh-cn_topic_0078078071_b1783318515228"><a name="zh-cn_topic_0078078071_b1783318515228"></a><a name="zh-cn_topic_0078078071_b1783318515228"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="83.27%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0078078071_p159273271920"><a name="zh-cn_topic_0078078071_p159273271920"></a><a name="zh-cn_topic_0078078071_p159273271920"></a><strong id="zh-cn_topic_0078078071_b10555114922418"><a name="zh-cn_topic_0078078071_b10555114922418"></a><a name="zh-cn_topic_0078078071_b10555114922418"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row9827431163111"><td class="cellrowborder" valign="top" width="16.73%" headers="mcps1.2.3.1.1 "><p id="p5828931103117"><a name="p5828931103117"></a><a name="p5828931103117"></a>迁移用户</p>
    </td>
    <td class="cellrowborder" valign="top" width="83.27%" headers="mcps1.2.3.1.2 "><div class="p" id="zh-cn_topic_0078078071_p106411111205412"><a name="zh-cn_topic_0078078071_p106411111205412"></a><a name="zh-cn_topic_0078078071_p106411111205412"></a>常见的迁移用户一般分为两类：支持迁移的用户和不支持迁移的用户。您可以根据业务需求选择“迁移”或者“不迁移”，其中，不支持迁移的账号或者未选择迁移的账号将在目标数据库中缺失，需要先确保业务不受影响。<a name="zh-cn_topic_0078078071_ul52489455107"></a><a name="zh-cn_topic_0078078071_ul52489455107"></a><ul id="zh-cn_topic_0078078071_ul52489455107"><li>迁移<p id="zh-cn_topic_0078078071_p385413556115"><a name="zh-cn_topic_0078078071_p385413556115"></a><a name="zh-cn_topic_0078078071_p385413556115"></a>当您选择迁移用户时，请参见《数据复制服务用户指南》中“<a href="https://support.huaweicloud.com/usermanual-drs/drs_09_0017.html" target="_blank" rel="noopener noreferrer">迁移用户</a>”章节进行数据库用户及角色的处理。</p>
    </li></ul>
    <a name="zh-cn_topic_0078078071_ul17378301111"></a><a name="zh-cn_topic_0078078071_ul17378301111"></a><ul id="zh-cn_topic_0078078071_ul17378301111"><li>不迁移<p id="zh-cn_topic_0078078071_p794655681211"><a name="zh-cn_topic_0078078071_p794655681211"></a><a name="zh-cn_topic_0078078071_p794655681211"></a>迁移过程中，将不进行数据库用户及角色的迁移。</p>
    </li></ul>
    </div>
    </td>
    </tr>
    <tr id="row18272163662119"><td class="cellrowborder" valign="top" width="16.73%" headers="mcps1.2.3.1.1 "><p id="p202731936182120"><a name="p202731936182120"></a><a name="p202731936182120"></a>其他迁移选项</p>
    </td>
    <td class="cellrowborder" valign="top" width="83.27%" headers="mcps1.2.3.1.2 "><p id="p102731736172117"><a name="p102731736172117"></a><a name="p102731736172117"></a>根据业务需求，选择全量迁移是否迁移用户自行创建的索引，基于_id的默认索引目标端会自动创建。如果不迁移索引，索引不参与对比。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0078078071_row559273214193"><td class="cellrowborder" valign="top" width="16.73%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0078078071_p14592132171916"><a name="zh-cn_topic_0078078071_p14592132171916"></a><a name="zh-cn_topic_0078078071_p14592132171916"></a>迁移对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="83.27%" headers="mcps1.2.3.1.2 "><p id="p189288361457"><a name="p189288361457"></a><a name="p189288361457"></a>您可以根据业务需求，选择全部对象迁移、表级迁移或者库级迁移。</p>
    <a name="ul692812368518"></a><a name="ul692812368518"></a><ul id="ul692812368518"><li>全部迁移：将源数据库中的所有对象全部迁移至目标数据库，对象迁移到目标数据库实例后，对象名将会保持与源数据库实例对象名一致且无法修改。</li><li>表级迁移：将选择的表级对象迁移至目标数据库。</li><li>库级迁移：将选择的库级对象迁移至目标数据库。</li></ul>
    <p id="p759715540459"><a name="p759715540459"></a><a name="p759715540459"></a>如果有切换源数据库的操作或源库迁移对象变化的情况，请务必在选择迁移对象前单击右上角的<a name="image959917843110"></a><a name="image959917843110"></a><span><img id="image959917843110" src="figures/icon-刷新.png"></span>，以确保待选择的对象为最新源数据库对象。</p>
    <div class="note" id="zh-cn_topic_0078078071_note6192135932115"><a name="zh-cn_topic_0078078071_note6192135932115"></a><a name="zh-cn_topic_0078078071_note6192135932115"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul19601624657"></a><a name="ul19601624657"></a><ul id="ul19601624657"><li>若选择部分数据库进行迁移时，由于存储过程、视图等对象可能与其他数据库的表存在依赖关系，若所依赖的表未迁移，则会导致迁移失败。建议您在迁移之前进行确认，或选择全部数据库进行迁移。</li><li>选择对象的时候，对象名称的前后空格不显示，中间如有多个空格只显示一个空格。</li><li>选择对象的时候支持搜索，以便您快速选择需要的数据库对象。</li></ul>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

5.  在“预检查“页面，进行迁移任务预校验，校验是否可进行迁移。
    -   查看检查结果，如有不通过的检查项，需要修复不通过项后，单击“重新校验”按钮重新进行迁移任务预校验。

        预检查不通过项处理建议请参见《数据复制服务用户指南》中的“[预检查不通过项修复方法](https://support.huaweicloud.com/usermanual-drs/drs_precheck.html)”。

        **图 6**  MongoDB预检查<a name="fig1873582121618"></a>  
        ![](figures/MongoDB预检查.png "MongoDB预检查")

    -   预检查完成后，且预检查通过率为100%时，单击“下一步”。

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >所有检查项结果均通过时，若存在请确认项，需要阅读并确认详情后才可以继续执行下一步操作。


6.  在“任务确认“页面，设置迁移任务的启动时间，并确认迁移任务信息无误后，单击“启动任务“，提交迁移任务。
7.  迁移任务提交后，您可在“实时迁移管理“页面，查看并管理自己的任务。
    -   您可查看任务提交后的状态，状态请参见[任务状态](https://support.huaweicloud.com/qs-drs/drs_03_0001.html)。
    -   在任务列表的右上角，单击![](figures/drs_icon-2.png)刷新列表，可查看到最新的任务状态。

8.  迁移任务创建成功后，请参见《数据复制服务快速入门》的[使用流程](https://support.huaweicloud.com/qs-drs/drs_02_0001.html)，进行完整的数据业务割接。


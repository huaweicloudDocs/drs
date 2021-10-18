# 创建VPC网络迁移任务<a name="drs_02_0022"></a>

VPC网络适合云上数据库之间的迁移。

在数据复制服务中，数据库迁移是通过任务的形式完成的，通过创建任务向导，可以完成任务信息配置、任务创建。迁移任务创建成功后，您也可以通过数据复制服务管理控制台，对任务进行管理。

本章节将以MySQL到RDS for MySQL的迁移为示例，介绍在VPC网络场景下，通过数据复制服务管理控制台配置数据迁移任务的流程，其他存储引擎的配置流程类似。

## 前提条件<a name="section148240813206"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   参见[实时迁移](https://support.huaweicloud.com/productdesc-drs/drs_01_0301.html)。
-   参见[使用须知](https://support.huaweicloud.com/qs-drs/drs_online_migration.html)。

## 操作步骤<a name="section157871952102012"></a>

1.  在“实时迁移管理“页面，单击“创建迁移任务“，进入创建迁移任务页面。
2.  在“迁移实例”页面，填选区域、任务名称、任务异常通知设置、SMN主题、时延阈值、任务异常自动结束时间、描述、迁移实例信息，单击“下一步”。

    **图 1**  迁移任务信息<a name="fig46277379581"></a>  
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

    **图 2**  VPC网络迁移实例信息<a name="fig6487192516156"></a>  
    ![](figures/VPC网络迁移实例信息.png "VPC网络迁移实例信息")

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
    <p id="p1983838136"><a name="p1983838136"></a><a name="p1983838136"></a>入云指目标端数据库为本云关系型数据库。</p>
    </td>
    </tr>
    <tr id="row0414184610580"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1414046115813"><a name="p1414046115813"></a><a name="p1414046115813"></a>源数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p14557101913243"><a name="p14557101913243"></a><a name="p14557101913243"></a>选择MySQL。</p>
    </td>
    </tr>
    <tr id="row42411630204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p12790028204436"><a name="p12790028204436"></a><a name="p12790028204436"></a>目标数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p2322512258"><a name="p2322512258"></a><a name="p2322512258"></a>选择MySQL。</p>
    </td>
    </tr>
    <tr id="row62907306204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p62327044204436"><a name="p62327044204436"></a><a name="p62327044204436"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p15598018543"><a name="p15598018543"></a><a name="p15598018543"></a>此处选择VPC网络。</p>
    <p id="p15325794204436"><a name="p15325794204436"></a><a name="p15325794204436"></a>默认为公网网络类型，可按照需求选择VPC网络、VPN网络、专线网络、公网网络。</p>
    <a name="ul1872454917306"></a><a name="ul1872454917306"></a><ul id="ul1872454917306"><li>VPC网络：适合云上数据库之间的迁移。</li><li>公网网络：适合通过公网网络把其他云下或其他平台的数据库迁移到目标数据库，该类型要求目标数据库绑定弹性公网IP（EIP）。</li><li>VPN网络：适合通过VPN网络，实现其他云下自建数据库与云上数据库迁移、或云上跨Region的数据库之间的迁移。</li><li>专线网络：适合通过专线网络，实现其他云下自建数据库与云上数据库迁移、或云上跨Region的数据库之间的迁移。</li></ul>
    </td>
    </tr>
    <tr id="row658644204515"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p53350183204515"><a name="p53350183204515"></a><a name="p53350183204515"></a>目标数据库实例</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p26397538204515"><a name="p26397538204515"></a><a name="p26397538204515"></a>用户所创建的目标数据库实例。</p>
    </td>
    </tr>
    <tr id="row113155141514"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p01021256155315"><a name="p01021256155315"></a><a name="p01021256155315"></a>迁移实例所在子网</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p18102456175315"><a name="p18102456175315"></a><a name="p18102456175315"></a>选择迁移实例所在的子网。也可以单击“查看子网”，跳转至“网络控制台”查看实例所在子网帮助选择。</p>
    <p id="p151791531292"><a name="p151791531292"></a><a name="p151791531292"></a>默认值为当前所选数据库实例所在子网，请选择有可用IP地址的子网。为确保迁移实例创建成功，仅显示已经开启DHCP的子网。</p>
    </td>
    </tr>
    <tr id="row4486429193216"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p20565125818284"><a name="p20565125818284"></a><a name="p20565125818284"></a>目标库读写设置</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><a name="ul1995631116555"></a><a name="ul1995631116555"></a><ul id="ul1995631116555"><li>只读<p id="p161716541232"><a name="p161716541232"></a><a name="p161716541232"></a>迁移中，目标数据库将转化为只读、不可写入的状态，迁移任务结束后恢复可读写状态，此选项可有效的确保数据迁移的完整性和成功率，推荐此选项。</p>
    </li></ul>
    <a name="ul117133599542"></a><a name="ul117133599542"></a><ul id="ul117133599542"><li>读写<p id="p12714659185417"><a name="p12714659185417"></a><a name="p12714659185417"></a>迁移中，目标数据库可以读写，但需要避免操作或接入应用后会更改迁移中的数据（注意：无业务的程序常常也有微量的数据操作），进而形成数据冲突、任务故障、且无法修复续传，充分了解要点后可选择此选项。</p>
    </li></ul>
    </td>
    </tr>
    <tr id="row0850133715295"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p128192616518"><a name="p128192616518"></a><a name="p128192616518"></a>迁移模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><a name="ul171919713019"></a><a name="ul171919713019"></a><ul id="ul171919713019"><li>全量：该模式为数据库一次性迁移，适用于可中断业务的<span class="keyword" id="keyword8520910122110"><a name="keyword8520910122110"></a><a name="keyword8520910122110"></a>数据库迁移</span>场景，全量迁移将非系统数据库的全部数据库对象和数据一次性迁移至目标端数据库，包括：表、视图、存储过程等。<div class="note" id="note1989394717302"><a name="note1989394717302"></a><a name="note1989394717302"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p12614191914218"><a name="p12614191914218"></a><a name="p12614191914218"></a>如果用户只进行全量迁移时，建议停止对源数据库的操作，否则迁移过程中源数据库产生的新数据不会同步到目标数据库。</p>
    </div></div>
    </li><li>全量+增量：该模式为数据库持续性迁移，适用于对业务中断敏感的场景，通过全量迁移过程中完成的目标端数据库的初始化后，增量迁移阶段通过解析日志等技术，将源端和目标端数据库保持数据持续一致。</li></ul>
    <div class="note" id="note3814342165119"><a name="note3814342165119"></a><a name="note3814342165119"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p118141442205110"><a name="p118141442205110"></a><a name="p118141442205110"></a>选择<span class="uicontrol" id="uicontrol24738122117"><a name="uicontrol24738122117"></a><a name="uicontrol24738122117"></a>“全量+增量”</span>迁移模式，增量迁移可以在全量迁移完成的基础上实现数据的持续同步，无需中断业务，实现迁移过程中源业务和数据库继续对外提供访问。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row29252034154016"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p20903194151816"><a name="p20903194151816"></a><a name="p20903194151816"></a>企业项目</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p102403918544"><a name="p102403918544"></a><a name="p102403918544"></a>对于已成功关联企业项目的用户，仅需在“企业项目”下拉框中选择目标项目。</p>
    <p id="p9102145320116"><a name="p9102145320116"></a><a name="p9102145320116"></a>如果需要自定义企业项目，请前往项目管理服务进行创建。关于如何创建项目，详见《项目管理用户指南》。</p>
    </td>
    </tr>
    <tr id="row174147413401"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p14235145217372"><a name="p14235145217372"></a><a name="p14235145217372"></a>标签</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p27631913145915"><a name="p27631913145915"></a><a name="p27631913145915"></a>可选配置，对迁移任务的标识。使用标签可方便管理您的迁移任务。每个任务最多支持10个标签配额。</p>
    <p id="p1060912514273"><a name="p1060912514273"></a><a name="p1060912514273"></a>任务创建成功后，您可以单击实例名称，在<span class="uicontrol" id="uicontrol8609155132714"><a name="uicontrol8609155132714"></a><a name="uicontrol8609155132714"></a>“标签”</span>页签下查看对应标签。关于标签的详细操作，请参见<a href="https://support.huaweicloud.com/usermanual-drs/drs_online_tag.html" target="_blank" rel="noopener noreferrer">标签管理</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，迁移实例创建成功后，填选源库信息和目标库信息，建议您单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，勾选协议，单击“下一步“。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >此处源库类型分为ECS自建库和RDS实例，需要根据源数据库的实际来源选择相应的分类。两种场景下的参数配置不一样，需要根据具体场景进行配置。

    -   场景一：ECS自建库源库信息配置

        **图 3**  ECS自建库场景源库信息<a name="fig4819182126"></a>  
        ![](figures/ECS自建库场景源库信息.png "ECS自建库场景源库信息")

        **表 3**  ECS自建库场景源库信息

        <a name="table108271821215"></a>
        <table><thead align="left"><tr id="row4819321621"><th class="cellrowborder" valign="top" width="23.29%" id="mcps1.2.3.1.1"><p id="p148191426219"><a name="p148191426219"></a><a name="p148191426219"></a><strong id="b14819102625"><a name="b14819102625"></a><a name="b14819102625"></a>参数</strong></p>
        </th>
        <th class="cellrowborder" valign="top" width="76.71%" id="mcps1.2.3.1.2"><p id="p178192021927"><a name="p178192021927"></a><a name="p178192021927"></a><strong id="b178191721220"><a name="b178191721220"></a><a name="b178191721220"></a>描述</strong></p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row11819925214"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p28196214219"><a name="p28196214219"></a><a name="p28196214219"></a>源库类型</p>
        </td>
        <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p2819421021"><a name="p2819421021"></a><a name="p2819421021"></a>选择ECS自建库。</p>
        </td>
        </tr>
        <tr id="row98192216219"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p08191218217"><a name="p08191218217"></a><a name="p08191218217"></a>VPC</p>
        </td>
        <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p1981992728"><a name="p1981992728"></a><a name="p1981992728"></a>源数据库实例所在的虚拟专用网络，可以对不同业务进行网络隔离。您需要创建或选择所需的虚拟私有云。如何创建虚拟私有云，请参见《虚拟私有云用户指南》中的“<a href="https://support.huaweicloud.com/usermanual-vpc/zh-cn_topic_0013935842.html" target="_blank" rel="noopener noreferrer">创建虚拟私有云基本信息及默认子网</a>”。</p>
        </td>
        </tr>
        <tr id="row198191427220"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p7819320212"><a name="p7819320212"></a><a name="p7819320212"></a>子网</p>
        </td>
        <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p18819172626"><a name="p18819172626"></a><a name="p18819172626"></a>通过子网提供与其他网络隔离的、可以独享的网络资源，以提高网络安全。子网在可用分区内才会有效，创建源数据库实例的子网需要开启DHCP功能，在创建过程中也不能关闭已选子网的DHCP功能。</p>
        </td>
        </tr>
        <tr id="row14819120214"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p48193218211"><a name="p48193218211"></a><a name="p48193218211"></a>IP地址或域名</p>
        </td>
        <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p1481919210215"><a name="p1481919210215"></a><a name="p1481919210215"></a>源数据库的IP地址或域名。</p>
        </td>
        </tr>
        <tr id="row281992628"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p1881913215211"><a name="p1881913215211"></a><a name="p1881913215211"></a>端口</p>
        </td>
        <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p18192218212"><a name="p18192218212"></a><a name="p18192218212"></a>源数据库服务端口，可输入范围为1~65535间的整数。</p>
        </td>
        </tr>
        <tr id="row08191623215"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p68191521217"><a name="p68191521217"></a><a name="p68191521217"></a>数据库用户名</p>
        </td>
        <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p98191821228"><a name="p98191821228"></a><a name="p98191821228"></a>源数据库的用户名。</p>
        </td>
        </tr>
        <tr id="row98197216211"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p4819523217"><a name="p4819523217"></a><a name="p4819523217"></a>数据库密码</p>
        </td>
        <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p16819121724"><a name="p16819121724"></a><a name="p16819121724"></a>源数据库的用户名所对应的密码。</p>
        </td>
        </tr>
        <tr id="row19827128212"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p1882715215211"><a name="p1882715215211"></a><a name="p1882715215211"></a>SSL安全连接</p>
        </td>
        <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p68272021522"><a name="p68272021522"></a><a name="p68272021522"></a>通过该功能，用户可以选择是否开启对迁移链路的加密。如果开启该功能，需要用户上传SSL CA根证书。</p>
        <div class="note" id="note118041213163"><a name="note118041213163"></a><a name="note118041213163"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul266710518121"></a><a name="ul266710518121"></a><ul id="ul266710518121"><li>最大支持上传500KB的证书文件。</li><li>如果不使用SSL证书，请自行承担数据安全风险。</li></ul>
        </div></div>
        </td>
        </tr>
        </tbody>
        </table>

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >**源数据库的IP地址或域名、数据库用户名和密码，会被系统加密暂存，直至删除该迁移任务后自动清除。**

    -   场景二：RDS实例源库信息配置

        **图 4**  RDS实例场景源库信息<a name="fig982712210213"></a>  
        ![](figures/RDS实例场景源库信息.png "RDS实例场景源库信息")

        **表 4**  RDS实例场景源库信息

        <a name="table5827152923"></a>
        <table><thead align="left"><tr id="row48273219210"><th class="cellrowborder" valign="top" width="22.869999999999997%" id="mcps1.2.3.1.1"><p id="p198276214213"><a name="p198276214213"></a><a name="p198276214213"></a><strong id="b98275220212"><a name="b98275220212"></a><a name="b98275220212"></a>参数</strong></p>
        </th>
        <th class="cellrowborder" valign="top" width="77.13%" id="mcps1.2.3.1.2"><p id="p1282713218211"><a name="p1282713218211"></a><a name="p1282713218211"></a><strong id="b168271421523"><a name="b168271421523"></a><a name="b168271421523"></a>描述</strong></p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row198277210215"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p68272021227"><a name="p68272021227"></a><a name="p68272021227"></a>源库类型</p>
        </td>
        <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p158276215212"><a name="p158276215212"></a><a name="p158276215212"></a>选择RDS实例。</p>
        </td>
        </tr>
        <tr id="row1982742821"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p3827162426"><a name="p3827162426"></a><a name="p3827162426"></a>数据库实例名称</p>
        </td>
        <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p1082792823"><a name="p1082792823"></a><a name="p1082792823"></a>选择待迁移的关系型数据库实例作为源数据库实例。</p>
        </td>
        </tr>
        <tr id="row188271221621"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p16827121429"><a name="p16827121429"></a><a name="p16827121429"></a>数据库用户名</p>
        </td>
        <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p1282702525"><a name="p1282702525"></a><a name="p1282702525"></a>源数据库实例的用户名。</p>
        </td>
        </tr>
        <tr id="row16827162722"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p128271529210"><a name="p128271529210"></a><a name="p128271529210"></a>数据库密码</p>
        </td>
        <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p5827121227"><a name="p5827121227"></a><a name="p5827121227"></a>源数据库的用户名所对应的密码。</p>
        </td>
        </tr>
        </tbody>
        </table>

    -   目标库信息配置

        **图 5**  目标库信息<a name="fig1482718216219"></a>  
        ![](figures/目标库信息.png "目标库信息")

        **表 5**  目标库信息

        <a name="table12827621220"></a>
        <table><thead align="left"><tr id="row28279213213"><th class="cellrowborder" valign="top" width="23%" id="mcps1.2.3.1.1"><p id="p10827621127"><a name="p10827621127"></a><a name="p10827621127"></a><strong id="b18277211214"><a name="b18277211214"></a><a name="b18277211214"></a>参数</strong></p>
        </th>
        <th class="cellrowborder" valign="top" width="77%" id="mcps1.2.3.1.2"><p id="p118271621920"><a name="p118271621920"></a><a name="p118271621920"></a><strong id="b48274219213"><a name="b48274219213"></a><a name="b48274219213"></a>描述</strong></p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row198271021525"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p11827172021"><a name="p11827172021"></a><a name="p11827172021"></a>数据库实例名称</p>
        </td>
        <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p382752323"><a name="p382752323"></a><a name="p382752323"></a>默认为创建迁移任务时选择的关系型数据库实例，不可进行修改。</p>
        </td>
        </tr>
        <tr id="row19827021723"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p138271521229"><a name="p138271521229"></a><a name="p138271521229"></a>数据库用户名</p>
        </td>
        <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p38271228213"><a name="p38271228213"></a><a name="p38271228213"></a>目标数据库对应的数据库用户名。</p>
        </td>
        </tr>
        <tr id="row17769362594"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p47463101599"><a name="p47463101599"></a><a name="p47463101599"></a>数据库密码</p>
        </td>
        <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p174383382711"><a name="p174383382711"></a><a name="p174383382711"></a>目标数据库的登录密码。</p>
        </td>
        </tr>
        <tr id="row3765147906"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p1629818288017"><a name="p1629818288017"></a><a name="p1629818288017"></a>所有Definer迁移到该用户下</p>
        </td>
        <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><a name="ul398013671012"></a><a name="ul398013671012"></a><ul id="ul398013671012"><li>是<p id="p1464371118108"><a name="p1464371118108"></a><a name="p1464371118108"></a>迁移后，所有源数据库对象的Definer都会迁移至该用户下，其他用户需要授权后才具有数据库对象权限，如何授权请参考<a href="https://support.huaweicloud.com/drs_faq/drs_16_0003.html" target="_blank" rel="noopener noreferrer">MySQL迁移中Definer强制转化后如何维持原业务用户权限体系</a></p>
        </li><li>否<p id="p217461817104"><a name="p217461817104"></a><a name="p217461817104"></a>迁移后，将保持源数据库对象Definer定义不变，选择此选项，需要配合下一步用户权限迁移功能，将源数据库的用户全部迁移，这样才能保持源数据库的权限体系完全不变。</p>
        </li></ul>
        </td>
        </tr>
        </tbody>
        </table>

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >数据库用户名和密码将被系统加密暂存，直至该任务删除后清除。


4.  在“迁移设置“页面，设置迁移用户和迁移对象，单击“下一步“。

    **图 6**  迁移模式<a name="drs_02_0021_zh-cn_topic_0078078071_fig46205265911"></a>  
    ![](figures/迁移模式.png "迁移模式")

    **表 6**  迁移模式和迁移对象

    <a name="drs_02_0021_zh-cn_topic_0078078071_table165921932111919"></a>
    <table><thead align="left"><tr id="drs_02_0021_zh-cn_topic_0078078071_row165921632141911"><th class="cellrowborder" valign="top" width="16%" id="mcps1.2.3.1.1"><p id="drs_02_0021_zh-cn_topic_0078078071_p1759233261916"><a name="drs_02_0021_zh-cn_topic_0078078071_p1759233261916"></a><a name="drs_02_0021_zh-cn_topic_0078078071_p1759233261916"></a><strong id="drs_02_0021_zh-cn_topic_0078078071_b1783318515228"><a name="drs_02_0021_zh-cn_topic_0078078071_b1783318515228"></a><a name="drs_02_0021_zh-cn_topic_0078078071_b1783318515228"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="84%" id="mcps1.2.3.1.2"><p id="drs_02_0021_zh-cn_topic_0078078071_p159273271920"><a name="drs_02_0021_zh-cn_topic_0078078071_p159273271920"></a><a name="drs_02_0021_zh-cn_topic_0078078071_p159273271920"></a><strong id="drs_02_0021_zh-cn_topic_0078078071_b10555114922418"><a name="drs_02_0021_zh-cn_topic_0078078071_b10555114922418"></a><a name="drs_02_0021_zh-cn_topic_0078078071_b10555114922418"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="drs_02_0021_row56641922154310"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="drs_02_0021_p628792914310"><a name="drs_02_0021_p628792914310"></a><a name="drs_02_0021_p628792914310"></a>流速模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="drs_02_0021_p122871029184320"><a name="drs_02_0021_p122871029184320"></a><a name="drs_02_0021_p122871029184320"></a>流速模式支持限速和不限速，默认为不限速。</p>
    <a name="drs_02_0021_ul328718292432"></a><a name="drs_02_0021_ul328718292432"></a><ul id="drs_02_0021_ul328718292432"><li>限速<p id="drs_02_0021_p162871429154317"><a name="drs_02_0021_p162871429154317"></a><a name="drs_02_0021_p162871429154317"></a>自定义的最大迁移速度，迁移过程中的迁移速度将不会超过该速度。</p>
    <p id="drs_02_0021_p182874295439"><a name="drs_02_0021_p182874295439"></a><a name="drs_02_0021_p182874295439"></a>当流速模式选择了“限速”时，你需要通过流速设置来定时控制迁移速度。流速设置通常包括限速时间段和流速大小的设置。默认的限速时间段为全天限流，您也可以根据业务需求自定义时段限流。自定义的时段限流支持最多设置3个定时任务，每个定时任务之间不能存在交叉的时间段，未设定在限速时间段的时间默认为不限速。</p>
    <p id="drs_02_0021_p528762914435"><a name="drs_02_0021_p528762914435"></a><a name="drs_02_0021_p528762914435"></a>流速的大小需要根据业务场景来设置，不能超过9999MB/s。</p>
    <div class="fignone" id="drs_02_0021_fig228702964316"><a name="drs_02_0021_fig228702964316"></a><a name="drs_02_0021_fig228702964316"></a><span class="figcap"><b>图1 </b>设置流速模式</span><br><a name="drs_02_0021_drs_02_0002_image1266125119393"></a><a name="drs_02_0021_drs_02_0002_image1266125119393"></a><span><img id="drs_02_0021_drs_02_0002_image1266125119393" src="figures/设置流速模式.png" height="159.61197" width="352.1175"></span></div>
    </li><li>不限速<div class="p" id="drs_02_0021_p182881429184310"><a name="drs_02_0021_p182881429184310"></a><a name="drs_02_0021_p182881429184310"></a>对迁移速度不进行限制，通常会最大化使用源数据库的出口带宽。该流速模式同时会对源数据库造成读消耗，消耗取决于源数据库的出口带宽。比如源数据库的出口带宽为100MB/s，假设高速模式使用了80%带宽，则迁移对源数据库将造成80MB/s的读操作IO消耗。<div class="note" id="drs_02_0021_note0288112910438"><a name="drs_02_0021_note0288112910438"></a><a name="drs_02_0021_note0288112910438"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="drs_02_0021_ul1528802934318"></a><a name="drs_02_0021_ul1528802934318"></a><ul id="drs_02_0021_ul1528802934318"><li>限速模式只对全量迁移阶段生效，增量迁移阶段不生效。</li><li>您也可以在创建任务后修改流速模式。具体方法请参见<a href="https://support.huaweicloud.com/usermanual-drs/drs_03_0046.html" target="_blank" rel="noopener noreferrer">修改流速模式</a>。</li></ul>
    </div></div>
    </div>
    </li></ul>
    </td>
    </tr>
    <tr id="drs_02_0021_zh-cn_topic_0078078071_row844211210119"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="drs_02_0021_zh-cn_topic_0078078071_p66491951191519"><a name="drs_02_0021_zh-cn_topic_0078078071_p66491951191519"></a><a name="drs_02_0021_zh-cn_topic_0078078071_p66491951191519"></a>快照模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="drs_02_0021_zh-cn_topic_0078078071_p96491051201513"><a name="drs_02_0021_zh-cn_topic_0078078071_p96491051201513"></a><a name="drs_02_0021_zh-cn_topic_0078078071_p96491051201513"></a>如果您选择的是全量迁移模式的任务，数据复制服务支持设置快照模式。</p>
    <a name="drs_02_0021_zh-cn_topic_0078078071_ul520619298172"></a><a name="drs_02_0021_zh-cn_topic_0078078071_ul520619298172"></a><ul id="drs_02_0021_zh-cn_topic_0078078071_ul520619298172"><li>非快照式<p id="drs_02_0021_zh-cn_topic_0078078071_p14673532201812"><a name="drs_02_0021_zh-cn_topic_0078078071_p14673532201812"></a><a name="drs_02_0021_zh-cn_topic_0078078071_p14673532201812"></a>适用于停止业务数据写入的导出，如果全量迁移中仍然有业务数据的修改，则导出数据为时间点非水平一致。稳定性和性能要优于快照式全量迁移。</p>
    </li><li>快照式<p id="drs_02_0021_zh-cn_topic_0078078071_p15193122742117"><a name="drs_02_0021_zh-cn_topic_0078078071_p15193122742117"></a><a name="drs_02_0021_zh-cn_topic_0078078071_p15193122742117"></a>可以在业务运行时产生一份时间水平一致的快照数据，具有业务数据分析价值，过程中的数据变化不会体现在导出数据中。</p>
    <div class="note" id="drs_02_0021_zh-cn_topic_0078078071_note16336123112117"><a name="drs_02_0021_zh-cn_topic_0078078071_note16336123112117"></a><a name="drs_02_0021_zh-cn_topic_0078078071_note16336123112117"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="drs_02_0021_zh-cn_topic_0078078071_ul58981133103"></a><a name="drs_02_0021_zh-cn_topic_0078078071_ul58981133103"></a><ul id="drs_02_0021_zh-cn_topic_0078078071_ul58981133103"><li>快照读会使用MySQL备份锁进行全局锁表，在开启一致性读后自动解锁（加锁时间在3s以内），备份锁会对此期间的DML或者DDL操作造成阻塞，建议用户选择源库空闲的时间段使用快照备份功能。</li><li>目前仅MySQL全量模式的迁移任务支持快照模式设置。</li><li>在快照迁移时不允许执行DDL操作，否则会导致全量迁移失败。</li></ul>
    </div></div>
    </li></ul>
    </td>
    </tr>
    <tr id="drs_02_0021_zh-cn_topic_0078078071_row2592193212194"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="drs_02_0021_zh-cn_topic_0078078071_p7592232201911"><a name="drs_02_0021_zh-cn_topic_0078078071_p7592232201911"></a><a name="drs_02_0021_zh-cn_topic_0078078071_p7592232201911"></a>迁移用户</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="drs_02_0021_zh-cn_topic_0078078071_p11670239171013"><a name="drs_02_0021_zh-cn_topic_0078078071_p11670239171013"></a><a name="drs_02_0021_zh-cn_topic_0078078071_p11670239171013"></a>数据库的迁移过程中，迁移用户需要进行单独处理。</p>
    <div class="p" id="drs_02_0021_zh-cn_topic_0078078071_p106411111205412"><a name="drs_02_0021_zh-cn_topic_0078078071_p106411111205412"></a><a name="drs_02_0021_zh-cn_topic_0078078071_p106411111205412"></a>常见的迁移用户一般分为三类：可完整迁移的用户、需要降权的用户和不可迁移的用户。您可以根据业务需求选择“迁移”或者“不迁移”，选择<span class="uicontrol" id="drs_02_0021_uicontrol1845534122119"><a name="drs_02_0021_uicontrol1845534122119"></a><a name="drs_02_0021_uicontrol1845534122119"></a>“迁移”</span>后，可根据需要选择迁移用户。 <a name="drs_02_0021_zh-cn_topic_0078078071_ul52489455107"></a><a name="drs_02_0021_zh-cn_topic_0078078071_ul52489455107"></a><ul id="drs_02_0021_zh-cn_topic_0078078071_ul52489455107"><li>迁移<p id="drs_02_0021_zh-cn_topic_0078078071_p385413556115"><a name="drs_02_0021_zh-cn_topic_0078078071_p385413556115"></a><a name="drs_02_0021_zh-cn_topic_0078078071_p385413556115"></a>当您选择迁移用户时，请参见《数据复制服务用户指南》中“<a href="https://support.huaweicloud.com/usermanual-drs/drs_09_0017.html" target="_blank" rel="noopener noreferrer">迁移用户</a>”章节进行数据库用户、权限及密码的处理。</p>
    </li></ul>
    </div>
    <a name="drs_02_0021_zh-cn_topic_0078078071_ul17378301111"></a><a name="drs_02_0021_zh-cn_topic_0078078071_ul17378301111"></a><ul id="drs_02_0021_zh-cn_topic_0078078071_ul17378301111"><li>不迁移<p id="drs_02_0021_zh-cn_topic_0078078071_p794655681211"><a name="drs_02_0021_zh-cn_topic_0078078071_p794655681211"></a><a name="drs_02_0021_zh-cn_topic_0078078071_p794655681211"></a>迁移过程中，将不进行数据库用户、权限和密码的迁移。</p>
    </li></ul>
    </td>
    </tr>
    <tr id="drs_02_0021_zh-cn_topic_0078078071_row559273214193"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="drs_02_0021_zh-cn_topic_0078078071_p14592132171916"><a name="drs_02_0021_zh-cn_topic_0078078071_p14592132171916"></a><a name="drs_02_0021_zh-cn_topic_0078078071_p14592132171916"></a>迁移对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="drs_02_0021_zh-cn_topic_0078078071_p1384592151414"><a name="drs_02_0021_zh-cn_topic_0078078071_p1384592151414"></a><a name="drs_02_0021_zh-cn_topic_0078078071_p1384592151414"></a>您可以根据业务需求，选择全部对象迁移、表级迁移或者库级迁移。</p>
    <a name="drs_02_0021_zh-cn_topic_0078078071_ul78601316141810"></a><a name="drs_02_0021_zh-cn_topic_0078078071_ul78601316141810"></a><ul id="drs_02_0021_zh-cn_topic_0078078071_ul78601316141810"><li>全部迁移：将源数据库中的所有对象全部迁移至目标数据库，对象迁移到目标数据库实例后，对象名将会保持与源数据库实例对象名一致且无法修改。</li><li>表级迁移：将选择的表级对象迁移至目标数据库。</li><li>库级迁移：将选择的库级对象迁移至目标数据库。</li></ul>
    <p id="drs_02_0021_p759715540459"><a name="drs_02_0021_p759715540459"></a><a name="drs_02_0021_p759715540459"></a>如果有切换源数据库的操作或源库迁移对象变化的情况，请务必在选择迁移对象前单击右上角的<a name="drs_02_0021_image959917843110"></a><a name="drs_02_0021_image959917843110"></a><span><img id="drs_02_0021_image959917843110" src="figures/drs_icon-2.png"></span>，以确保待选择的对象为最新源数据库对象。</p>
    <div class="note" id="drs_02_0021_zh-cn_topic_0078078071_note6192135932115"><a name="drs_02_0021_zh-cn_topic_0078078071_note6192135932115"></a><a name="drs_02_0021_zh-cn_topic_0078078071_note6192135932115"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="drs_02_0021_ul19601624657"></a><a name="drs_02_0021_ul19601624657"></a><ul id="drs_02_0021_ul19601624657"><li>若选择部分数据库进行迁移时，由于存储过程、视图等对象可能与其他数据库的表存在依赖关系，若所依赖的表未迁移，则会导致迁移失败。建议您在迁移之前进行确认，或选择全部数据库进行迁移。</li><li>选择对象的时候，对象名称的前后空格不显示，中间如有多个空格只显示一个空格。</li><li>选择对象的时候支持搜索，以便您快速选择需要的数据库对象。</li></ul>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

5.  在“预检查“页面，进行迁移任务预校验，校验是否可进行迁移。
    -   查看检查结果，如有不通过的检查项，需要修复不通过项后，单击“重新校验”按钮重新进行迁移任务预校验。

        预检查不通过项处理建议请参见《数据复制服务用户指南》中的“[预检查不通过项修复方法](https://support.huaweicloud.com/usermanual-drs/drs_precheck.html)”。

        **图 8**  预检查<a name="drs_02_0021_drs_02_0002_fig5147165311461"></a>  
        ![](figures/预检查.png "预检查")

    -   预检查完成后，且预检查通过率为100%时，单击“下一步”。

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >所有检查项结果均通过时，若存在待确认项，需要阅读并确认详情后才可以继续执行下一步操作。


6.  进入“参数对比“页面，进行参数对比。

    参数对比功能从常规参数和性能参数两个维度，展示了源数据库和目标数据库的参数值是否一致。您可以根据业务需求，决定是否选用该功能。该操作不影响数据的迁移，主要目的是为了确保迁移成功后业务应用的使用不受影响。

    -   若您选择不进行参数对比，可跳过该步骤，单击页面右下角“下一步“按钮，继续执行后续操作。
    -   若您选择进行参数对比，请参照如下的步骤操作。

        一般情况下，对于常规参数，如果源库和目标库存在不一致的情况，建议将目标数据库的参数值通过“一键修改“按钮修改为和源库对应参数相同的值。

        **图 9**  修改常规参数<a name="drs_02_0021_drs_02_0002_fig771445810191"></a>  
        ![](figures/修改常规参数.png "修改常规参数")

        对于性能参数，您可以根据业务场景，自定义源数据库和目标库的参数值，二者结果可以一致也可以不一致。

        -   若您需要将对比结果一致的性能参数修改为不一致，需要在“目标库值调整为“一列手动输入结果，单击左上角“一键修改“按钮，即可将源数据库和目标数据库对应的性能参数值改为不一致。
        -   若您想将对比结果不一致的参数改为一致结果，请参考如下流程进行修改：
            1.  对齐源库和目标库的参数值。

                当源库和目标库对应的参数值出现不一致时，选择需要修改的参数，单击“一键对齐“按钮，系统将帮您自动填充目标数据库的参数值，使其和源库对应的参数值保持一致。

                **图 10**  一键对齐参数<a name="drs_02_0021_drs_02_0002_fig5154113452214"></a>  
                ![](figures/一键对齐参数.png "一键对齐参数")

                >![](public_sys-resources/icon-note.gif) **说明：** 
                >对齐参数值的操作，您也可以通过手动输入结果。

            2.  修改参数值。

                源库和目标库的不一致参数值对齐后，单击“一键修改“按钮，系统将按照您当前设置的目标库参数值进行修改。修改完成后，目标库的参数值和对比结果会自动进行更新。

                **图 11**  修改性能参数<a name="drs_02_0021_drs_02_0002_fig2890155692418"></a>  
                ![](figures/修改性能参数.png "修改性能参数")

                部分参数修改后无法在目标数据库立即生效，需要重启才能生效，此时的对比结果显示为“待重启，不一致”。建议您在迁移任务启动之前重启目标数据库，或者迁移结束后选择一个计划时间重启。如果您选择迁移结束后重启目标数据库，请合理设置重启计划时间，避免参数生效太晚影响业务的正常使用。

                在进行参数对比功能时，您可以参见《数据复制服务用户指南》中“[参数对比列表](https://support.huaweicloud.com/usermanual-drs/drs_08_0001.html)”进行参数设置。

            3.  参数对比操作完成后，单击“下一步”。


7.  在“任务确认“页面，设置迁移任务的启动时间，并确认迁移任务信息无误后，单击“启动任务“，提交迁移任务。

    迁移任务的启动时间可以根据业务需求，设置为“立即启动”或“稍后启动”。

    预计迁移任务启动后，会对源数据库和目标数据库的性能产生影响，建议选择业务低峰期，合理设置迁移任务的启动时间。

8.  迁移任务提交后，您可在“实时迁移管理“页面，查看并管理自己的任务。
    -   您可查看任务提交后的状态，状态请参见[任务状态](https://support.huaweicloud.com/qs-drs/drs_03_0001.html)。
    -   在任务列表的右上角，单击![](figures/drs_icon-2.png)刷新列表，可查看到最新的任务状态。



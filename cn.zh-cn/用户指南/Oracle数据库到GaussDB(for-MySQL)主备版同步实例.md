# Oracle数据库到GaussDB\(for MySQL\)主备版同步实例<a name="drs_03_1114"></a>

本小节以Oracle-\>GaussDB\(for MySQL\)主备版的实时同步为示例，介绍如何使用数据复制服务配置实时同步任务。

## 前提条件<a name="section2097363117427"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   参见[实时同步](https://support.huaweicloud.com/productdesc-drs/drs_01_0302.html)。
-   参见[使用须知](https://support.huaweicloud.com/qs-drs/drs_06_0003.html)。

## 操作步骤<a name="section15233183613210"></a>

1.  在“实时同步管理”页面，单击“创建同步任务”。
2.  在“同步实例”页面，填选区域、任务名称、任务异常通知信息、SMN主题、时延阈值、任务异常自动结束时间、描述、同步实例信息，单击“下一步”。

    **图 1**  同步任务信息<a name="fig078405211374"></a>  
    ![](figures/同步任务信息.png "同步任务信息")

    **表 1**  任务和描述

    <a name="table27686220467"></a>
    <table><thead align="left"><tr id="drs_06_0005_row55731924204420"><th class="cellrowborder" valign="top" width="18.43%" id="mcps1.2.3.1.1"><p id="drs_06_0005_p17991967204420"><a name="drs_06_0005_p17991967204420"></a><a name="drs_06_0005_p17991967204420"></a><strong id="drs_06_0005_b1611223511352"><a name="drs_06_0005_b1611223511352"></a><a name="drs_06_0005_b1611223511352"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="81.57%" id="mcps1.2.3.1.2"><p id="drs_06_0005_p48063227204420"><a name="drs_06_0005_p48063227204420"></a><a name="drs_06_0005_p48063227204420"></a><strong id="drs_06_0005_b3002268111352"><a name="drs_06_0005_b3002268111352"></a><a name="drs_06_0005_b3002268111352"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="drs_06_0005_row1459143619148"><td class="cellrowborder" valign="top" width="18.43%" headers="mcps1.2.3.1.1 "><p id="drs_06_0005_p28681745141416"><a name="drs_06_0005_p28681745141416"></a><a name="drs_06_0005_p28681745141416"></a>区域</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.57%" headers="mcps1.2.3.1.2 "><p id="drs_06_0005_p1895134514149"><a name="drs_06_0005_p1895134514149"></a><a name="drs_06_0005_p1895134514149"></a>当前所在区域，可进行切换。</p>
    </td>
    </tr>
    <tr id="drs_06_0005_row807311204420"><td class="cellrowborder" valign="top" width="18.43%" headers="mcps1.2.3.1.1 "><p id="drs_06_0005_p65392260204420"><a name="drs_06_0005_p65392260204420"></a><a name="drs_06_0005_p65392260204420"></a>任务名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.57%" headers="mcps1.2.3.1.2 "><p id="drs_06_0005_p62281730204420"><a name="drs_06_0005_p62281730204420"></a><a name="drs_06_0005_p62281730204420"></a>任务名称在4-50位之间，必须以字母开头，不区分大小写，可以包含字母、数字、中划线或下划线，不能包含其他的特殊字符。</p>
    </td>
    </tr>
    <tr id="drs_06_0005_row18223175312283"><td class="cellrowborder" valign="top" width="18.43%" headers="mcps1.2.3.1.1 "><p id="drs_06_0005_p189819291"><a name="drs_06_0005_p189819291"></a><a name="drs_06_0005_p189819291"></a>描述</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.57%" headers="mcps1.2.3.1.2 "><p id="drs_06_0005_p129151192917"><a name="drs_06_0005_p129151192917"></a><a name="drs_06_0005_p129151192917"></a>描述不能超过256位，且不能包含! = &lt; &gt; &amp; ' " \ 特殊字符。</p>
    </td>
    </tr>
    <tr id="drs_06_0005_row1080215433911"><td class="cellrowborder" valign="top" width="18.43%" headers="mcps1.2.3.1.1 "><p id="drs_06_0005_p158027493912"><a name="drs_06_0005_p158027493912"></a><a name="drs_06_0005_p158027493912"></a>任务异常通知设置</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.57%" headers="mcps1.2.3.1.2 "><p id="drs_06_0005_p38891258184013"><a name="drs_06_0005_p38891258184013"></a><a name="drs_06_0005_p38891258184013"></a>该项为可选参数，开启之后，选择对应的SMN主题，。当同步任务状态异常时，系统将发送通知。</p>
    </td>
    </tr>
    <tr id="drs_06_0005_row1238083594114"><td class="cellrowborder" valign="top" width="18.43%" headers="mcps1.2.3.1.1 "><p id="drs_06_0005_p5381193584119"><a name="drs_06_0005_p5381193584119"></a><a name="drs_06_0005_p5381193584119"></a>SMN主题</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.57%" headers="mcps1.2.3.1.2 "><p id="drs_06_0005_p17361121081210"><a name="drs_06_0005_p17361121081210"></a><a name="drs_06_0005_p17361121081210"></a><span class="uicontrol" id="drs_06_0005_uicontrol83037419162"><a name="drs_06_0005_uicontrol83037419162"></a><a name="drs_06_0005_uicontrol83037419162"></a>“任务异常通知设置”</span>项开启后可见，需提前在SMN上申请主题并添加订阅。</p>
    <p id="drs_06_0005_p127491315171714"><a name="drs_06_0005_p127491315171714"></a><a name="drs_06_0005_p127491315171714"></a>SMN主题申请和订阅可参考<a href="https://support.huaweicloud.com/qs-smn/smn_ug_0004.html" target="_blank" rel="noopener noreferrer">《消息通知服务用户指南》</a>。</p>
    </td>
    </tr>
    <tr id="drs_06_0005_row49611652175115"><td class="cellrowborder" valign="top" width="18.43%" headers="mcps1.2.3.1.1 "><p id="drs_06_0005_p183714599519"><a name="drs_06_0005_p183714599519"></a><a name="drs_06_0005_p183714599519"></a>时延阈值</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.57%" headers="mcps1.2.3.1.2 "><p id="drs_06_0005_p1737125935111"><a name="drs_06_0005_p1737125935111"></a><a name="drs_06_0005_p1737125935111"></a>在增量同步阶段，源数据库和目标数据库之间的同步有时会存在一个时间差，称为时延，单位为秒。</p>
    <p id="drs_06_0005_p14371596516"><a name="drs_06_0005_p14371596516"></a><a name="drs_06_0005_p14371596516"></a>时延阈值设置是指时延超过一定的值后（时延阈值范围为1—3600s），DRS可以发送告警通知给指定收件人。告警通知将在时延稳定超过设定的阈值6min后发送，避免出现由于时延波动反复发送告警通知的情况。</p>
    <div class="note" id="drs_06_0005_note14371459105118"><a name="drs_06_0005_note14371459105118"></a><a name="drs_06_0005_note14371459105118"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="drs_06_0005_ul163805916512"></a><a name="drs_06_0005_ul163805916512"></a><ul id="drs_06_0005_ul163805916512"><li>首次进入增量同步阶段，会有较多数据等待同步，存在较大的时延，属于正常情况，不在此功能的监控范围之内。</li><li>设置时延阈值之前，需要设置任务异常通知。</li></ul>
    </div></div>
    </td>
    </tr>
    <tr id="drs_06_0005_row157731032102814"><td class="cellrowborder" valign="top" width="18.43%" headers="mcps1.2.3.1.1 "><p id="drs_06_0005_p1677373232818"><a name="drs_06_0005_p1677373232818"></a><a name="drs_06_0005_p1677373232818"></a>任务异常自动结束时间（天）</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.57%" headers="mcps1.2.3.1.2 "><p id="drs_06_0005_p10335124785914"><a name="drs_06_0005_p10335124785914"></a><a name="drs_06_0005_p10335124785914"></a>设置任务异常自动结束天数，输入值必须在14-100之间。</p>
    <div class="note" id="drs_06_0005_note115651218193116"><a name="drs_06_0005_note115651218193116"></a><a name="drs_06_0005_note115651218193116"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="drs_06_0005_p1956521816315"><a name="drs_06_0005_p1956521816315"></a><a name="drs_06_0005_p1956521816315"></a>异常状态下的任务仍然会计费，而长时间异常的任务无法续传和恢复。设置任务异常自动结束天数后，异常且超时的任务将会自动结束，以免产生不必要的费用。</p>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

    **图 2**  Oracle到GaussDB\(for MySQL\)主备版同步实例信息<a name="fig123764616489"></a>  
    ![](figures/Oracle到GaussDB(for-MySQL)主备版同步实例信息.png "Oracle到GaussDB(for-MySQL)主备版同步实例信息")

    **表 2**  同步实例信息

    <a name="table476811227463"></a>
    <table><thead align="left"><tr id="row39932329204436"><th class="cellrowborder" valign="top" width="23.87%" id="mcps1.2.3.1.1"><p id="p13293221204436"><a name="p13293221204436"></a><a name="p13293221204436"></a><strong id="b2587841611355"><a name="b2587841611355"></a><a name="b2587841611355"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.13%" id="mcps1.2.3.1.2"><p id="p3009113204436"><a name="p3009113204436"></a><a name="p3009113204436"></a><strong id="b1577696211355"><a name="b1577696211355"></a><a name="b1577696211355"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row05147381129"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p951443871218"><a name="p951443871218"></a><a name="p951443871218"></a>数据流动方向</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p10323458361"><a name="p10323458361"></a><a name="p10323458361"></a>选择<span class="uicontrol" id="uicontrol1422913280188"><a name="uicontrol1422913280188"></a><a name="uicontrol1422913280188"></a>“入云”</span>。</p>
    </td>
    </tr>
    <tr id="row0414184610580"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1414046115813"><a name="p1414046115813"></a><a name="p1414046115813"></a>源数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p168249357197"><a name="p168249357197"></a><a name="p168249357197"></a>选择<span class="uicontrol" id="uicontrol051853118180"><a name="uicontrol051853118180"></a><a name="uicontrol051853118180"></a>“Oracle”</span>。</p>
    </td>
    </tr>
    <tr id="row42411630204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p12790028204436"><a name="p12790028204436"></a><a name="p12790028204436"></a>目标数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1969552512018"><a name="p1969552512018"></a><a name="p1969552512018"></a>选择<span class="uicontrol" id="uicontrol154014364188"><a name="uicontrol154014364188"></a><a name="uicontrol154014364188"></a>“GaussDB(for MySQL)主备版”</span>。</p>
    </td>
    </tr>
    <tr id="row62907306204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p62327044204436"><a name="p62327044204436"></a><a name="p62327044204436"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p87075558433"><a name="p87075558433"></a><a name="p87075558433"></a>此处以<span class="uicontrol" id="uicontrol12676440161816"><a name="uicontrol12676440161816"></a><a name="uicontrol12676440161816"></a>“公网网络”</span>为示例。目前支持可选公网网络、VPN网络和专线网络。</p>
    </td>
    </tr>
    <tr id="row658644204515"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p53350183204515"><a name="p53350183204515"></a><a name="p53350183204515"></a>目标数据库实例</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p26397538204515"><a name="p26397538204515"></a><a name="p26397538204515"></a>创建好的GaussDB(for MySQL)主备版实例。</p>
    </td>
    </tr>
    <tr id="row1626018434720"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p01021256155315"><a name="p01021256155315"></a><a name="p01021256155315"></a>同步实例所在子网</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p18102456175315"><a name="p18102456175315"></a><a name="p18102456175315"></a>请选择同步实例所在的子网。也可以单击“查看子网”，跳转至“网络控制台”查看实例所在子网帮助选择。</p>
    <p id="p47671146133910"><a name="p47671146133910"></a><a name="p47671146133910"></a>默认值为当前所选数据库实例所在子网，请选择有可用IP地址的子网。为确保同步实例创建成功，仅显示已经开启DHCP的子网。</p>
    </td>
    </tr>
    <tr id="row1169913195320"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p06786155538"><a name="p06786155538"></a><a name="p06786155538"></a>同步类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p16673526288"><a name="p16673526288"></a><a name="p16673526288"></a>全量+增量</p>
    <p id="p766716522283"><a name="p766716522283"></a><a name="p766716522283"></a>该模式为数据持续性实时同步，通过全量过程完成目标端数据库的初始化后，增量同步阶段通过解析日志等技术，将源端和目标端数据保持数据持续一致。</p>
    <div class="note" id="note3678415155319"><a name="note3678415155319"></a><a name="note3678415155319"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p16678121514537"><a name="p16678121514537"></a><a name="p16678121514537"></a>选择<span class="uicontrol" id="uicontrol18678615205315"><a name="uicontrol18678615205315"></a><a name="uicontrol18678615205315"></a>“全量+增量”</span>同步模式，增量同步可以在全量同步完成的基础上实现数据的持续同步，无需中断业务，实现同步过程中源业务和数据库继续对外提供访问。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row456045155616"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1017716536718"><a name="p1017716536718"></a><a name="p1017716536718"></a>企业项目</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p795282881017"><a name="p795282881017"></a><a name="p795282881017"></a>对于已成功关联企业项目的用户，仅需在“企业项目”下拉框中选择目标项目。</p>
    <p id="p8952152819109"><a name="p8952152819109"></a><a name="p8952152819109"></a>如果需要自定义企业项目，请前往项目管理服务进行创建。关于如何创建项目，详见《项目管理用户指南》。</p>
    </td>
    </tr>
    <tr id="row1318710585563"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1276314133599"><a name="p1276314133599"></a><a name="p1276314133599"></a>标签</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p492718308322"><a name="p492718308322"></a><a name="p492718308322"></a>可选配置，对同步任务的标识。使用标签可方便管理您的<span id="drs_06_0005_text947798304"><a name="drs_06_0005_text947798304"></a><a name="drs_06_0005_text947798304"></a>实时同步</span>任务。每个任务最多支持10个标签配额。</p>
    <p id="p8307101212113"><a name="p8307101212113"></a><a name="p8307101212113"></a>任务创建成功后，您可以单击实例名称，在<span class="uicontrol" id="zh-cn_topic_0078078071_uicontrol1433412554316"><a name="zh-cn_topic_0078078071_uicontrol1433412554316"></a><a name="zh-cn_topic_0078078071_uicontrol1433412554316"></a>“标签”</span>页签下查看对应标签。关于标签的详细操作，请参见<a href="https://support.huaweicloud.com/usermanual-drs/drs_synchronization_tag.html" target="_blank" rel="noopener noreferrer">标签管理</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，同步实例创建成功后，填选源库信息和目标库信息，单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，勾选协议，单击“下一步“。

    **图 3**  Oracle 源库信息<a name="zh-cn_topic_0288918853_fig20498162055215"></a>  
    ![](figures/Oracle-源库信息.png "Oracle-源库信息")

    **表 3**  源库信息

    <a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_table1665310232597"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_row12653123195919"><th class="cellrowborder" valign="top" width="23.27%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p156531623165916"><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p156531623165916"></a><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p156531623165916"></a><strong id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_b20653923155913"><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_b20653923155913"></a><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_b20653923155913"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.73%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p1365312365910"><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p1365312365910"></a><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p1365312365910"></a><strong id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_b186531223105910"><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_b186531223105910"></a><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_b186531223105910"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_row1265352355912"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p665313232598"><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p665313232598"></a><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p665313232598"></a>IP地址或域名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p2653523145918"><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p2653523145918"></a><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p2653523145918"></a>源数据库的IP地址或域名。</p>
    <div class="note" id="note1778831484919"><a name="note1778831484919"></a><a name="note1778831484919"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p20789141414918"><a name="p20789141414918"></a><a name="p20789141414918"></a>对于RAC集群，建议使用scanip接入，提高访问性能。</p>
    </div></div>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_row765313235597"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p8653172395914"><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p8653172395914"></a><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p8653172395914"></a>端口</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p15653192315910"><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p15653192315910"></a><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p15653192315910"></a>源数据库服务端口，可输入范围为1~65535间的整数。</p>
    </td>
    </tr>
    <tr id="row119010914238"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="p128556486553"><a name="p128556486553"></a><a name="p128556486553"></a>数据库服务名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="p8856174865513"><a name="p8856174865513"></a><a name="p8856174865513"></a>数据库服务名（Service Name/SID），客户端可以通过其连接到Oracle，具体查询方法请参照界面提示。</p>
    </td>
    </tr>
    <tr id="row166292042111219"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="p9629174217122"><a name="p9629174217122"></a><a name="p9629174217122"></a>PDB名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="p18691415141"><a name="p18691415141"></a><a name="p18691415141"></a>PDB同步仅在Oracle12c及以后的版本支持，该功能为选填项，当需要迁移PDB中的表时开启。</p>
    <p id="p4572104191411"><a name="p4572104191411"></a><a name="p4572104191411"></a>PDB功能开启后，只能迁移该PDB中的表，并且需要提供CDB的service name/sid及用户名和密码，不需要PDB的用户名和密码。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_row065352315596"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="p1485684811553"><a name="p1485684811553"></a><a name="p1485684811553"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="p9856174812555"><a name="p9856174812555"></a><a name="p9856174812555"></a>源数据库的用户名。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288918853_row1317210417203"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="p7856348135511"><a name="p7856348135511"></a><a name="p7856348135511"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="p885619484558"><a name="p885619484558"></a><a name="p885619484558"></a>源数据库的用户名所对应的密码。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_row26531923125912"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="p685674812558"><a name="p685674812558"></a><a name="p685674812558"></a>SSL安全连接</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="p168571148145510"><a name="p168571148145510"></a><a name="p168571148145510"></a>通过该功能，用户可以选择是否开启对迁移链路的加密。如果开启该功能，需要用户上传SSL CA根证书。</p>
    <div class="note" id="note88571048145520"><a name="note88571048145520"></a><a name="note88571048145520"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul58571348175514"></a><a name="ul58571348175514"></a><ul id="ul58571348175514"><li>最大支持上传500KB的证书文件。</li><li>如果不使用SSL证书，请自行承担数据安全风险。</li></ul>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >**源数据库的IP地址或域名、数据库用户名和密码，会被系统加密暂存，直至删除该迁移任务后自动清除。**

    **图 4**  GaussDB\(for MySQL\)主备版目标库信息<a name="fig1592113195219"></a>  
    ![](figures/GaussDB(for-MySQL)主备版目标库信息.png "GaussDB(for-MySQL)主备版目标库信息")

    **表 4**  目标库信息

    <a name="zh-cn_topic_0135097933_table157461610185911"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0135097933_row15746151015912"><th class="cellrowborder" valign="top" width="23%" id="mcps1.2.3.1.1"><p id="p1772017480224"><a name="p1772017480224"></a><a name="p1772017480224"></a><strong id="b107201248152214"><a name="b107201248152214"></a><a name="b107201248152214"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="77%" id="mcps1.2.3.1.2"><p id="p167207487229"><a name="p167207487229"></a><a name="p167207487229"></a><strong id="b16720648152219"><a name="b16720648152219"></a><a name="b16720648152219"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0135097933_row0746151020595"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p18720948182213"><a name="p18720948182213"></a><a name="p18720948182213"></a>数据库实例名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p2720648162210"><a name="p2720648162210"></a><a name="p2720648162210"></a>默认为创建迁移任务时选择的关系型数据库实例，不可进行修改。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row2746310155916"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p12720194810221"><a name="p12720194810221"></a><a name="p12720194810221"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p1172011483227"><a name="p1172011483227"></a><a name="p1172011483227"></a>目标数据库对应的数据库用户名。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row107461010135910"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p472064812223"><a name="p472064812223"></a><a name="p472064812223"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p4720248152211"><a name="p4720248152211"></a><a name="p4720248152211"></a>数据库用户名和密码将被系统加密暂存，直至该任务删除后清除。支持在任务创建后修改密码。</p>
    <p id="p20148550151313"><a name="p20148550151313"></a><a name="p20148550151313"></a>任务为启动中、全量同步、增量同步、增量同步失败状态时，可在<span class="uicontrol" id="uicontrol514817508139"><a name="uicontrol514817508139"></a><a name="uicontrol514817508139"></a>“基本信息”</span>页面的<span class="uicontrol" id="uicontrol1314811509134"><a name="uicontrol1314811509134"></a><a name="uicontrol1314811509134"></a>“同步信息”</span>区域，单击<span class="uicontrol" id="uicontrol18148105016134"><a name="uicontrol18148105016134"></a><a name="uicontrol18148105016134"></a>“目标库密码”</span>后的<span class="uicontrol" id="uicontrol1914895091318"><a name="uicontrol1914895091318"></a><a name="uicontrol1914895091318"></a>“替换密码”</span>，在弹出的对话框中修改密码。</p>
    </td>
    </tr>
    </tbody>
    </table>

4.  在“设置同步“页面，选择同步类型和同步对象，单击“下一步“。

    **图 5**  Oracle到GaussDB\(for MySQL\)主备版同步模式<a name="fig14025637142814"></a>  
    ![](figures/Oracle到GaussDB(for-MySQL)主备版同步模式.png "Oracle到GaussDB(for-MySQL)主备版同步模式")

    **表 5**  同步模式和对象

    <a name="table165921932111919"></a>
    <table><thead align="left"><tr id="row165921632141911"><th class="cellrowborder" valign="top" width="16%" id="mcps1.2.3.1.1"><p id="p1759233261916"><a name="p1759233261916"></a><a name="p1759233261916"></a><strong id="b1783318515228"><a name="b1783318515228"></a><a name="b1783318515228"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="84%" id="mcps1.2.3.1.2"><p id="p159273271920"><a name="p159273271920"></a><a name="p159273271920"></a><strong id="b10555114922418"><a name="b10555114922418"></a><a name="b10555114922418"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row593912531914"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p1194016252191"><a name="p1194016252191"></a><a name="p1194016252191"></a>同步类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p65772810236"><a name="p65772810236"></a><a name="p65772810236"></a>可选同步表结构、同步数据、同步索引，根据实际需求进行选择要同步内容。</p>
    <a name="ul9359134216234"></a><a name="ul9359134216234"></a><ul id="ul9359134216234"><li>同步数据为必选项。</li><li>选则同步表结构的时候目标库不能有同名的表。</li><li>不选同步表结构的时候目标库必须有相应的表，且要保证表结构与所选表结构相同。</li></ul>
    </td>
    </tr>
    <tr id="row559273214193"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p14592132171916"><a name="p14592132171916"></a><a name="p14592132171916"></a>同步对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p1833512479145"><a name="p1833512479145"></a><a name="p1833512479145"></a>表级同步，导入对象文件，您可以根据业务场景选择对应的数据进行同步。选择数据的时候支持搜索，以便您快速选择需要的数据库对象。</p>
    <p id="p11545503164"><a name="p11545503164"></a><a name="p11545503164"></a>选择导入对象文件，具体步骤和说明可参考<a href="导入同步对象.md">导入同步对象</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

5.  在“数据加工“页，可对同步数据进行过滤，完成后单击“下一步“，详细参考”[数据加工](数据加工.md)“。
6.  在“预检查“页面，进行同步任务预校验，校验是否可进行实时同步。
    -   查看检查结果，如有不通过的检查项，需要修复不通过项后，单击“重新校验”按钮重新进行任务预校验。

        预检查不通过项处理建议请参见《数据复制服务用户指南》中的“[预检查不通过项修复方法](https://support.huaweicloud.com/usermanual-drs/drs_precheck.html)”。

    -   预检查完成后，且所有检查项结果均通过时，单击“下一步“。

        **图 6**  同步预检查<a name="drs_06_0005_fig23361684715"></a>  
        ![](figures/同步预检查.png "同步预检查")

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >所有检查项结果均通过时，若存在请确认项，需要阅读并确认详情后才可以继续执行下一步操作。


7.  在“任务确认“页面，设置同步任务的启动时间，并确认同步任务信息无误后，勾选协议，单击“启动任务“，提交同步任务。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   同步任务的启动时间可以根据业务需求，设置为“立即启动”或“稍后启动”。
    >-   预计同步任务启动后，会对源数据库和目标数据库的性能产生影响，建议选择业务低峰期，合理设置同步任务的启动时间。

8.  同步任务提交后，您可在“实时同步管理“页面，查看并管理自己的任务。
    -   您可查看任务提交后的状态，状态请参见[任务状态](https://support.huaweicloud.com/qs-drs/drs_06_0004.html)。
    -   在任务列表的右上角，单击![](figures/kwx318612-GAUSS-DBaaS-image-a8fbc7b6-eab2-4798-b522-174e36341a92.png)刷新列表，可查看到最新的任务状态。



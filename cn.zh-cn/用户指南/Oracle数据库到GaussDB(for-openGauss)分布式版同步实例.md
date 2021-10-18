# Oracle数据库到GaussDB\(for openGauss\)分布式版同步实例<a name="drs_03_1123"></a>

本小节以Oracle-\>GaussDB\(for openGauss\)分布式版实时同步为示例，介绍如何使用数据复制服务配置实时同步任务。

## 前提条件<a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_section2097363117427"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   参见[实时同步](https://support.huaweicloud.com/productdesc-drs/drs_01_0302.html)。
-   参见[使用须知](https://support.huaweicloud.com/qs-drs/drs_06_0003.html)。

## 操作步骤<a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_section1324751412355"></a>

1.  在“实时同步管理”页面，单击“创建同步任务”。
2.  <a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_li125644351372"></a>在“同步实例”页面，填选区域、任务名称、任务异常通知信息、SMN主题、时延阈值、任务异常自动结束时间、描述、同步实例信息，单击“下一步”。

    **图 1**  同步任务信息<a name="fig38893269351"></a>  
    ![](figures/同步任务信息.png "同步任务信息")

    **表 1**  任务和描述

    <a name="zh-cn_topic_0288472243_table27686220467"></a>
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

    **图 2**  Oracle到GaussDB\(for openGauss\)分布式版同步实例信息<a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_fig123764616489"></a>  
    ![](figures/Oracle到GaussDB(for-openGauss)分布式版同步实例信息.png "Oracle到GaussDB(for-openGauss)分布式版同步实例信息")

    **表 2**  同步实例信息

    <a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_table476811227463"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row39932329204436"><th class="cellrowborder" valign="top" width="23.87%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p13293221204436"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p13293221204436"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p13293221204436"></a><strong id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_b2587841611355"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_b2587841611355"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_b2587841611355"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.13%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p3009113204436"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p3009113204436"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p3009113204436"></a><strong id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_b1577696211355"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_b1577696211355"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_b1577696211355"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row05147381129"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p951443871218"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p951443871218"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p951443871218"></a>数据流动场景</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p10323458361"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p10323458361"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p10323458361"></a>选择<span class="uicontrol" id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_uicontrol1422913280188"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_uicontrol1422913280188"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_uicontrol1422913280188"></a>“入云”</span>。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row0414184610580"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1414046115813"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1414046115813"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1414046115813"></a>源数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p168249357197"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p168249357197"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p168249357197"></a>选择“Oracle”。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row42411630204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p12790028204436"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p12790028204436"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p12790028204436"></a>目标数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1969552512018"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1969552512018"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1969552512018"></a>选择“<span id="zh-cn_topic_0288472243_text11408149713"><a name="zh-cn_topic_0288472243_text11408149713"></a><a name="zh-cn_topic_0288472243_text11408149713"></a>GaussDB(for openGauss)</span>分布式版”。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row62907306204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p62327044204436"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p62327044204436"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p62327044204436"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p87075558433"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p87075558433"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p87075558433"></a>此处以公网网络为示例。目前支持可选公网网络和VPN、专线网络。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row658644204515"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p53350183204515"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p53350183204515"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p53350183204515"></a>目标数据库实例</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p26397538204515"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p26397538204515"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p26397538204515"></a>用户所创建的<span id="zh-cn_topic_0288472243_text4670112418713"><a name="zh-cn_topic_0288472243_text4670112418713"></a><a name="zh-cn_topic_0288472243_text4670112418713"></a>GaussDB(for openGauss)</span>分布式版实例。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row183713012714"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p01021256155315"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p01021256155315"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p01021256155315"></a>同步实例所在子网</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p18102456175315"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p18102456175315"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p18102456175315"></a>请选择同步实例所在的子网。也可以单击“查看子网”，跳转至“网络控制台”查看实例所在子网帮助选择。</p>
    <p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p47671146133910"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p47671146133910"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p47671146133910"></a>默认值为当前所选数据库实例所在子网，请选择有可用IP地址的子网。为确保同步实例创建成功，仅显示已经开启DHCP的子网。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row1169913195320"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p06786155538"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p06786155538"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p06786155538"></a>同步类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p154111148111120"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p154111148111120"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p154111148111120"></a>全量，增量， 两种选择类型。</p>
    </td>
    </tr>
    <tr id="row168851556716"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p206442047125010"><a name="p206442047125010"></a><a name="p206442047125010"></a>标签</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p27631913145915"><a name="p27631913145915"></a><a name="p27631913145915"></a>可选配置，对同步任务的标识。使用标签可方便管理您的<span id="drs_06_0005_text947798304"><a name="drs_06_0005_text947798304"></a><a name="drs_06_0005_text947798304"></a>实时同步</span>任务。每个任务最多支持10个标签配额。</p>
    <p id="p2064444715507"><a name="p2064444715507"></a><a name="p2064444715507"></a>任务创建成功后，您可以单击实例名称，在<span class="uicontrol" id="uicontrol13644847185019"><a name="uicontrol13644847185019"></a><a name="uicontrol13644847185019"></a>“标签”</span>页签下查看对应标签。关于标签的详细操作，请参见<a href="https://support.huaweicloud.com/usermanual-drs/drs_synchronization_tag.html" target="_blank" rel="noopener noreferrer">标签管理</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，填选源库信息和目标库信息，单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，单击“下一步“。

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

    **图 4**  GaussDB\(for openGauss\)分布式版目标库信息<a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_fig1592113195219"></a>  
    ![](figures/GaussDB(for-openGauss)分布式版目标库信息.png "GaussDB(for-openGauss)分布式版目标库信息")

    **表 4**  目标库信息

    <a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_table157461610185911"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_row15746151015912"><th class="cellrowborder" valign="top" width="23%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p18746101055912"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p18746101055912"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p18746101055912"></a><strong id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_b074631019593"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_b074631019593"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_b074631019593"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="77%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p15746181055920"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p15746181055920"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p15746181055920"></a><strong id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_b1774613108597"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_b1774613108597"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_b1774613108597"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_row0746151020595"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p1674610102597"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p1674610102597"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p1674610102597"></a>数据库实例名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p3746710165918"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p3746710165918"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p3746710165918"></a>默认为创建同步任务时选择的关系型数据库实例，不可进行修改。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_row2746310155916"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p18746310175911"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p18746310175911"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p18746310175911"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_p11696193861913"><a name="zh-cn_topic_0288472243_p11696193861913"></a><a name="zh-cn_topic_0288472243_p11696193861913"></a>目标数据库的用户名。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_row107461010135910"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p47463101599"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p47463101599"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_zh-cn_topic_0135097933_p47463101599"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_p1469615384199"><a name="zh-cn_topic_0288472243_p1469615384199"></a><a name="zh-cn_topic_0288472243_p1469615384199"></a>目标数据库的用户名所对应的密码。数据库用户名和密码将被系统加密暂存，直至该任务删除后清除。</p>
    </td>
    </tr>
    </tbody>
    </table>

4.  在“设置同步“页面，选择同步对象，此处必须手动输入目标数据库名称，完成后单击“下一步“。

    **图 5**  Oracle到GaussDB\(for openGauss\)分布式版同步模式<a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_fig14025637142814"></a>  
    ![](figures/Oracle到GaussDB(for-openGauss)分布式版同步模式.png "Oracle到GaussDB(for-openGauss)分布式版同步模式")

    **表 5**  同步对象

    <a name="zh-cn_topic_0288472243_table165921932111919"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0288472243_row165921632141911"><th class="cellrowborder" valign="top" width="16%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0288472243_p1759233261916"><a name="zh-cn_topic_0288472243_p1759233261916"></a><a name="zh-cn_topic_0288472243_p1759233261916"></a><strong id="zh-cn_topic_0288472243_b1783318515228"><a name="zh-cn_topic_0288472243_b1783318515228"></a><a name="zh-cn_topic_0288472243_b1783318515228"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="84%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0288472243_p159273271920"><a name="zh-cn_topic_0288472243_p159273271920"></a><a name="zh-cn_topic_0288472243_p159273271920"></a><strong id="zh-cn_topic_0288472243_b10555114922418"><a name="zh-cn_topic_0288472243_b10555114922418"></a><a name="zh-cn_topic_0288472243_b10555114922418"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0288472243_row559273214193"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_p14592132171916"><a name="zh-cn_topic_0288472243_p14592132171916"></a><a name="zh-cn_topic_0288472243_p14592132171916"></a>同步对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_p288617596718"><a name="zh-cn_topic_0288472243_p288617596718"></a><a name="zh-cn_topic_0288472243_p288617596718"></a>表级同步和导入对象文件，您可以根据业务场景选择对应的数据进行同步。</p>
    <a name="ul260144315584"></a><a name="ul260144315584"></a><ul id="ul260144315584"><li>在同步对象右侧已选对象框中，可以使用对象名映射功能进行源数据库和目标数据库中的同步对象映射，具体操作可参考<a href="对象名映射.md">对象名映射</a>。</li></ul>
    <a name="zh-cn_topic_0288472243_ul172931323184413"></a><a name="zh-cn_topic_0288472243_ul172931323184413"></a><ul id="zh-cn_topic_0288472243_ul172931323184413"><li>选择导入对象文件，具体步骤和说明可参考<a href="导入同步对象.md">导入同步对象</a>。</li></ul>
    </td>
    </tr>
    </tbody>
    </table>

5.  在“高级设置“”页，可查看之前**[步骤2](#zh-cn_topic_0288472243_zh-cn_topic_0288918853_li125644351372)**选择“全量”同步或“增量”同步的运行参数，当前运行参数为默认值，暂时不支持修改，单击“下一步“。

    **图 6**  Oracle到GaussDB\(for openGauss\)分布式版全量同步<a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_fig362212416544"></a>  
    ![](figures/Oracle到GaussDB(for-openGauss)分布式版全量同步.png "Oracle到GaussDB(for-openGauss)分布式版全量同步")

    **表 6**  全量同步参数说明

    <a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_table14286418203912"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row13287518153911"><th class="cellrowborder" valign="top" width="19.621962196219624%" id="mcps1.2.4.1.1"><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1628771823918"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1628771823918"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1628771823918"></a>参数名</p>
    </th>
    <th class="cellrowborder" valign="top" width="58.32583258325832%" id="mcps1.2.4.1.2"><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p5287121818393"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p5287121818393"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p5287121818393"></a>功能描述</p>
    </th>
    <th class="cellrowborder" valign="top" width="22.05220522052205%" id="mcps1.2.4.1.3"><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1128761863914"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1128761863914"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1128761863914"></a>默认值</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row52871018143910"><td class="cellrowborder" valign="top" width="19.621962196219624%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p0287151813391"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p0287151813391"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p0287151813391"></a>同步类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.32583258325832%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p16287131818391"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p16287131818391"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p16287131818391"></a>可选同步表结构、同步数据、同步索引，根据实际需求进行选择要同步内容。其中同步数据为必选项。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.05220522052205%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p92877183397"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p92877183397"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p92877183397"></a>三项全选。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row10287618193914"><td class="cellrowborder" valign="top" width="19.621962196219624%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p16287121813916"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p16287121813916"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p16287121813916"></a>流模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.32583258325832%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p928711814396"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p928711814396"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p928711814396"></a>该模式下，数据写入目标库是按分片进行提交，一个分片提交一次。否则数据会按照写入目标库数据量进行提交，每写入16M数据提交一次。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.05220522052205%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p3287161819396"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p3287161819396"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p3287161819396"></a>选中。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row162871918173915"><td class="cellrowborder" valign="top" width="19.621962196219624%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p62881181392"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p62881181392"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p62881181392"></a>导出并发数</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.32583258325832%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p2288191815395"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p2288191815395"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p2288191815395"></a>控制启动多少个线程从Oracle导出数据。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.05220522052205%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p82881218163913"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p82881218163913"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p82881218163913"></a>8</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row528811863910"><td class="cellrowborder" valign="top" width="19.621962196219624%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1288161813398"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1288161813398"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1288161813398"></a>导入并发数</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.32583258325832%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1028831853919"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1028831853919"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1028831853919"></a>控制启动多少个线程并发向<span id="text13811287168"><a name="text13811287168"></a><a name="text13811287168"></a>GaussDB(for openGauss)</span>写入数据。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.05220522052205%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p5288218203915"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p5288218203915"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p5288218203915"></a>8</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row4288818123912"><td class="cellrowborder" valign="top" width="19.621962196219624%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p32881018183913"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p32881018183913"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p32881018183913"></a>导入模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.32583258325832%" headers="mcps1.2.4.1.2 "><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_ul13288131819399"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_ul13288131819399"></a><ul id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_ul13288131819399"><li>COPY模式：<p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p728891833917"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p728891833917"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p728891833917"></a>通过<span id="text14221334111614"><a name="text14221334111614"></a><a name="text14221334111614"></a>GaussDB(for openGauss)</span>的copy接口写入数据,效率较高。</p>
    </li><li>INSERT模式：<p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p10288141843914"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p10288141843914"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p10288141843914"></a>通过拼接insert语句的方式写入数据，效率相对较低。但是该方式可以忽略主键冲突数据。</p>
    </li></ul>
    </td>
    <td class="cellrowborder" valign="top" width="22.05220522052205%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p17288171813919"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p17288171813919"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p17288171813919"></a>copy模式。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row92881818173910"><td class="cellrowborder" valign="top" width="19.621962196219624%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p828815183394"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p828815183394"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p828815183394"></a>分片记录数</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.32583258325832%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p17289181823912"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p17289181823912"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p17289181823912"></a>对表进行分片导出，来提供实时同步的效率。</p>
    <a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_ul72891218123912"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_ul72891218123912"></a><ul id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_ul72891218123912"><li>值为0<p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1628921812395"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1628921812395"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1628921812395"></a>对所有表不分片，每张表作为一个整体进行同步。</p>
    </li><li>值为其他数值<p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p328931873916"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p328931873916"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p328931873916"></a>按照指定数值对表进行分片（根据主键列），当表的记录数小于该值时，不分片。</p>
    </li><li>如果表为分区表，则每个分区作为一个分片进行同步，不再按照记录数据分片。</li><li>如果表为无主键和唯一索引表，则不分片，该参数值无意义。</li><li>如果表分析不及时，即ALL_TABLES视图的NUM_ROWS值为空，也不进行分片。</li></ul>
    </td>
    <td class="cellrowborder" valign="top" width="22.05220522052205%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p72891181399"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p72891181399"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p72891181399"></a>520000</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_row16799126101217"><td class="cellrowborder" valign="top" width="19.621962196219624%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0288472243_p1180013671210"><a name="zh-cn_topic_0288472243_p1180013671210"></a><a name="zh-cn_topic_0288472243_p1180013671210"></a>同步位点</p>
    </td>
    <td class="cellrowborder" valign="top" width="58.32583258325832%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0288472243_p1800126181213"><a name="zh-cn_topic_0288472243_p1800126181213"></a><a name="zh-cn_topic_0288472243_p1800126181213"></a>建议设置为当前的SCN，如果设置为将来的SCN或者已删除归档日志所在的SCN范围，将会导致任务失败。</p>
    </td>
    <td class="cellrowborder" valign="top" width="22.05220522052205%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0288472243_p1080066171213"><a name="zh-cn_topic_0288472243_p1080066171213"></a><a name="zh-cn_topic_0288472243_p1080066171213"></a>默认是启动时的SCN。</p>
    </td>
    </tr>
    </tbody>
    </table>

    **图 7**  Oracle到GaussDB\(for openGauss\)分布式版增量同步<a name="zh-cn_topic_0288472243_fig630263018012"></a>  
    ![](figures/Oracle到GaussDB(for-openGauss)分布式版增量同步.png "Oracle到GaussDB(for-openGauss)分布式版增量同步")

    **表 7**  增量同步参数说明

    <a name="zh-cn_topic_0288472243_table82921851101915"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0288472243_row9292135111912"><th class="cellrowborder" valign="top" width="19.621962196219624%" id="mcps1.2.4.1.1"><p id="zh-cn_topic_0288472243_p929285141913"><a name="zh-cn_topic_0288472243_p929285141913"></a><a name="zh-cn_topic_0288472243_p929285141913"></a>参数名</p>
    </th>
    <th class="cellrowborder" valign="top" width="53.45534553455346%" id="mcps1.2.4.1.2"><p id="zh-cn_topic_0288472243_p182928516195"><a name="zh-cn_topic_0288472243_p182928516195"></a><a name="zh-cn_topic_0288472243_p182928516195"></a>功能描述</p>
    </th>
    <th class="cellrowborder" valign="top" width="26.92269226922692%" id="mcps1.2.4.1.3"><p id="zh-cn_topic_0288472243_p329255113198"><a name="zh-cn_topic_0288472243_p329255113198"></a><a name="zh-cn_topic_0288472243_p329255113198"></a>默认值</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0288472243_row7292751171920"><td class="cellrowborder" valign="top" width="19.621962196219624%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0288472243_p1292351131916"><a name="zh-cn_topic_0288472243_p1292351131916"></a><a name="zh-cn_topic_0288472243_p1292351131916"></a>日志抓取并发数</p>
    </td>
    <td class="cellrowborder" valign="top" width="53.45534553455346%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0288472243_p7292451131911"><a name="zh-cn_topic_0288472243_p7292451131911"></a><a name="zh-cn_topic_0288472243_p7292451131911"></a>读取Oracle日志的并发线程数，可配范围1-16。</p>
    </td>
    <td class="cellrowborder" valign="top" width="26.92269226922692%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0288472243_p72931151121919"><a name="zh-cn_topic_0288472243_p72931151121919"></a><a name="zh-cn_topic_0288472243_p72931151121919"></a>1</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_row6293185171911"><td class="cellrowborder" valign="top" width="19.621962196219624%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0288472243_p152931051171912"><a name="zh-cn_topic_0288472243_p152931051171912"></a><a name="zh-cn_topic_0288472243_p152931051171912"></a>抓取启动位点</p>
    </td>
    <td class="cellrowborder" valign="top" width="53.45534553455346%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0288472243_p1429395121917"><a name="zh-cn_topic_0288472243_p1429395121917"></a><a name="zh-cn_topic_0288472243_p1429395121917"></a>指定抓取启动的scn点，这个scn号要根据实际的需求进行设计，它由两部分组成，分别是抓取的起始scn号，和有效数据的scn号，具体的解释需要参考Oracle的scn相关概念。</p>
    </td>
    <td class="cellrowborder" valign="top" width="26.92269226922692%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0288472243_p142931512190"><a name="zh-cn_topic_0288472243_p142931512190"></a><a name="zh-cn_topic_0288472243_p142931512190"></a>空，抓取默认采用数据库的当前scn作为启动点。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_row529315116195"><td class="cellrowborder" valign="top" width="19.621962196219624%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0288472243_p1229325115198"><a name="zh-cn_topic_0288472243_p1229325115198"></a><a name="zh-cn_topic_0288472243_p1229325115198"></a>回放任务并发数</p>
    </td>
    <td class="cellrowborder" valign="top" width="53.45534553455346%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0288472243_p10293105111917"><a name="zh-cn_topic_0288472243_p10293105111917"></a><a name="zh-cn_topic_0288472243_p10293105111917"></a>向<span id="text195751356131613"><a name="text195751356131613"></a><a name="text195751356131613"></a>GaussDB(for openGauss)</span>写入数据的并发线程数，可配范围1-64。</p>
    </td>
    <td class="cellrowborder" valign="top" width="26.92269226922692%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0288472243_p19293195119197"><a name="zh-cn_topic_0288472243_p19293195119197"></a><a name="zh-cn_topic_0288472243_p19293195119197"></a>64</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_row172939514190"><td class="cellrowborder" valign="top" width="19.621962196219624%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0288472243_p929305171917"><a name="zh-cn_topic_0288472243_p929305171917"></a><a name="zh-cn_topic_0288472243_p929305171917"></a>回放启动策略</p>
    </td>
    <td class="cellrowborder" valign="top" width="53.45534553455346%" headers="mcps1.2.4.1.2 "><a name="zh-cn_topic_0288472243_ul929385110197"></a><a name="zh-cn_topic_0288472243_ul929385110197"></a><ul id="zh-cn_topic_0288472243_ul929385110197"><li>自动<p id="zh-cn_topic_0288472243_p112931451101917"><a name="zh-cn_topic_0288472243_p112931451101917"></a><a name="zh-cn_topic_0288472243_p112931451101917"></a>启动任务后，回放组件会自动启动。</p>
    </li><li>手动<p id="zh-cn_topic_0288472243_p586419161133"><a name="zh-cn_topic_0288472243_p586419161133"></a><a name="zh-cn_topic_0288472243_p586419161133"></a>启动任务后，回放组件不启动，需要手动进行单独启动。</p>
    </li></ul>
    </td>
    <td class="cellrowborder" valign="top" width="26.92269226922692%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0288472243_p8294651181913"><a name="zh-cn_topic_0288472243_p8294651181913"></a><a name="zh-cn_topic_0288472243_p8294651181913"></a>自动。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_row82941751111914"><td class="cellrowborder" valign="top" width="19.621962196219624%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0288472243_p14294175112194"><a name="zh-cn_topic_0288472243_p14294175112194"></a><a name="zh-cn_topic_0288472243_p14294175112194"></a>冲突策略</p>
    </td>
    <td class="cellrowborder" valign="top" width="53.45534553455346%" headers="mcps1.2.4.1.2 "><a name="zh-cn_topic_0288472243_ul8294145161912"></a><a name="zh-cn_topic_0288472243_ul8294145161912"></a><ul id="zh-cn_topic_0288472243_ul8294145161912"><li>覆盖<p id="zh-cn_topic_0288472243_p0294125118192"><a name="zh-cn_topic_0288472243_p0294125118192"></a><a name="zh-cn_topic_0288472243_p0294125118192"></a>当数据回放报错时，会用DRS抓取到的数据覆盖掉目标库的数据。</p>
    </li><li>报错<p id="zh-cn_topic_0288472243_p13294155112196"><a name="zh-cn_topic_0288472243_p13294155112196"></a><a name="zh-cn_topic_0288472243_p13294155112196"></a>当数据回放报错时，会直接返回错误，界面报同步异常。</p>
    </li><li>忽略<p id="zh-cn_topic_0288472243_p11294105121911"><a name="zh-cn_topic_0288472243_p11294105121911"></a><a name="zh-cn_topic_0288472243_p11294105121911"></a>当数据回放报错时，会跳过报错的记录，继续运行。</p>
    </li></ul>
    </td>
    <td class="cellrowborder" valign="top" width="26.92269226922692%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0288472243_p1829445115190"><a name="zh-cn_topic_0288472243_p1829445115190"></a><a name="zh-cn_topic_0288472243_p1829445115190"></a>覆盖。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_row122945511197"><td class="cellrowborder" valign="top" width="19.621962196219624%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0288472243_p162941151101910"><a name="zh-cn_topic_0288472243_p162941151101910"></a><a name="zh-cn_topic_0288472243_p162941151101910"></a>回放启动位点</p>
    </td>
    <td class="cellrowborder" valign="top" width="53.45534553455346%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0288472243_p142941251101914"><a name="zh-cn_topic_0288472243_p142941251101914"></a><a name="zh-cn_topic_0288472243_p142941251101914"></a>指定回放启动的scn点。</p>
    </td>
    <td class="cellrowborder" valign="top" width="26.92269226922692%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0288472243_p329435171918"><a name="zh-cn_topic_0288472243_p329435171918"></a><a name="zh-cn_topic_0288472243_p329435171918"></a>空，若不指定，默认和抓取启动位点相同。</p>
    </td>
    </tr>
    </tbody>
    </table>

6.  在“数据加工”页面，选择需要加工的列，进行列加工。

    -   如果不需要数据加工，单击“下一步”。
    -   如果需要加工列，参考[数据加工](数据加工.md)中的列加工，设置相关规则。

    **图 8**  Oracle到GaussDB\(for openGauss\)分布式版数据加工<a name="fig12259113011255"></a>  
    ![](figures/Oracle到GaussDB(for-openGauss)分布式版数据加工.png "Oracle到GaussDB(for-openGauss)分布式版数据加工")

7.  在“预检查“页面，进行同步任务预校验，校验是否可进行实时同步。
    -   查看检查结果，如有不通过的检查项，需要修复不通过项后，单击“重新校验”按钮重新进行任务预校验。

        预检查不通过项处理建议请参见《数据复制服务用户指南》中的“[预检查不通过项修复方法](https://support.huaweicloud.com/usermanual-drs/drs_precheck.html)”。

    -   预检查完成后，且所有检查项结果均通过时，单击“下一步“。

        **图 9**  Oracle到GaussDB\(for openGauss\)分布式版预检查<a name="drs_03_0036_fig3658849112911"></a>  
        ![](figures/Oracle到GaussDB(for-openGauss)分布式版预检查.png "Oracle到GaussDB(for-openGauss)分布式版预检查")

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >所有检查项结果均通过时，若存在请确认项，需要阅读并确认详情后才可以继续执行下一步操作。


8.  在“任务确认“页面，设置同步任务的启动时间，并确认同步任务信息无误后，勾选协议，单击“启动任务“，提交同步任务。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   同步任务的启动时间可以根据业务需求，设置为“立即启动”或“稍后启动”。
    >-   预计同步任务启动后，会对源数据库和目标数据库的性能产生影响，建议选择业务低峰期，合理设置同步任务的启动时间。


## 对比同步项<a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_section153118557111"></a>

对比实时同步项可以清晰反馈出源数据库和目标数据库的数据是否存在差异。为了尽可能减少业务的影响和业务中断时间，实时同步场景提供了数据级对比功能，帮助您确定合适的业务割接时机。

>![](public_sys-resources/icon-note.gif) **说明：** 
>GaussDB\(for openGauss\)分布式版不支持直接更新分布键，所以DRS同步时不支持该场景，否则会导致数据丢失对比不一致。

-   数据级对比：支持对表的行数和内容进行对比，其中内容对比不支持计算资源的选择。
-   增量任务：支持手动创建内容对比和行对比。结束时会自动取消增量校验状态、全量校验状态、运行状态的内容对比和行对比。结束后，已完成的行对比或者取消的内容对比均支持查看对比详细数据。

    **表 8**  增量任务内容对比

    <a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_table1748441719615"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row14854172612"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p74855174619"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p74855174619"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p74855174619"></a>状态</p>
    </th>
    <th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p137822212718"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p137822212718"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p137822212718"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row848517178614"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p104856171364"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p104856171364"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p104856171364"></a>运行中</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p114851217465"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p114851217465"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p114851217465"></a>不支持查看对比详细数据</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row948641717611"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p84861717169"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p84861717169"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p84861717169"></a>增量校验中</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1748617177617"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1748617177617"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1748617177617"></a>支持查看对比详细数据</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row1148681710614"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1148612171263"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1148612171263"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1148612171263"></a>取消</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p74861171615"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p74861171615"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p74861171615"></a>支持查看对比详细数据</p>
    </td>
    </tr>
    </tbody>
    </table>

    **表 9**  增量任务行对比

    <a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_table199021553398"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row1690320531090"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p15299155515102"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p15299155515102"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p15299155515102"></a>状态</p>
    </th>
    <th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1429955511107"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1429955511107"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1429955511107"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row189031053296"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p10300455131013"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p10300455131013"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p10300455131013"></a>运行中</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p7300165518105"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p7300165518105"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p7300165518105"></a>不支持查看对比详细数据</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_row11903253699"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1290355314915"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1290355314915"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p1290355314915"></a>完成</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p14903105313914"><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p14903105313914"></a><a name="zh-cn_topic_0288472243_zh-cn_topic_0288918853_p14903105313914"></a>支持查看对比详细数据</p>
    </td>
    </tr>
    </tbody>
    </table>

-   全量任务：完成后支持手动创建内容对比和行对比。任务结束后，支持查看内容对比和行对比详细数据。

    **表 10**  全量任务内容对比

    <a name="zh-cn_topic_0288472243_table39286244349"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0288472243_row592932453410"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0288472243_p19929132417343"><a name="zh-cn_topic_0288472243_p19929132417343"></a><a name="zh-cn_topic_0288472243_p19929132417343"></a>状态</p>
    </th>
    <th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0288472243_p1292910247343"><a name="zh-cn_topic_0288472243_p1292910247343"></a><a name="zh-cn_topic_0288472243_p1292910247343"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0288472243_row59291924143419"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_p99296247341"><a name="zh-cn_topic_0288472243_p99296247341"></a><a name="zh-cn_topic_0288472243_p99296247341"></a>运行中</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_p20929192493417"><a name="zh-cn_topic_0288472243_p20929192493417"></a><a name="zh-cn_topic_0288472243_p20929192493417"></a>不支持查看对比详细数据</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_row292932413419"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_p19301524153412"><a name="zh-cn_topic_0288472243_p19301524153412"></a><a name="zh-cn_topic_0288472243_p19301524153412"></a>全量校验中</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_p1093012244347"><a name="zh-cn_topic_0288472243_p1093012244347"></a><a name="zh-cn_topic_0288472243_p1093012244347"></a>不支持查看对比详细数据</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_row1893012453414"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_p1993013247342"><a name="zh-cn_topic_0288472243_p1993013247342"></a><a name="zh-cn_topic_0288472243_p1993013247342"></a>完成</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_p1593042414343"><a name="zh-cn_topic_0288472243_p1593042414343"></a><a name="zh-cn_topic_0288472243_p1593042414343"></a>支持查看对比详细数据</p>
    </td>
    </tr>
    </tbody>
    </table>

    **表 11**  全量任务行对比

    <a name="zh-cn_topic_0288472243_table1482864073420"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0288472243_row1829134043410"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0288472243_p6829144019349"><a name="zh-cn_topic_0288472243_p6829144019349"></a><a name="zh-cn_topic_0288472243_p6829144019349"></a>状态</p>
    </th>
    <th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0288472243_p10829174011344"><a name="zh-cn_topic_0288472243_p10829174011344"></a><a name="zh-cn_topic_0288472243_p10829174011344"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0288472243_row208292407343"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_p282964053413"><a name="zh-cn_topic_0288472243_p282964053413"></a><a name="zh-cn_topic_0288472243_p282964053413"></a>运行中</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_p782954013346"><a name="zh-cn_topic_0288472243_p782954013346"></a><a name="zh-cn_topic_0288472243_p782954013346"></a>不支持查看对比详细数据</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288472243_row158291440143415"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0288472243_p382920407346"><a name="zh-cn_topic_0288472243_p382920407346"></a><a name="zh-cn_topic_0288472243_p382920407346"></a>完成</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288472243_p6829040113419"><a name="zh-cn_topic_0288472243_p6829040113419"></a><a name="zh-cn_topic_0288472243_p6829040113419"></a>支持查看对比详细数据</p>
    </td>
    </tr>
    </tbody>
    </table>

-   Oracle-\>GaussDB\(for openGauss\)数据内容同步对比中，针对不同的数据类型，有特殊的处理，详细请参考数据复制服务DRS产品介绍“数据类型映射关系”章节中的内容。
-   注意，以下情况不支持内容对比：
    -   当源库和目标库不一致数据大于10000条。
    -   当源库和目标库中，表列数不一样。
    -   当源库和目标库中，表列名不一样。
    -   当源库和目标库中，表主键名不一样。
    -   无主键的表。
    -   源库和目的库同种字段精度不一致。



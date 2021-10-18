# DDM数据库到Kafka同步实例<a name="drs_11_0446"></a>

本小节以DDM-\>Kafka的出云实时同步为示例，介绍如何使用数据复制服务配置实时同步任务。

## 前提条件<a name="section2097363117427"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   参见[实时同步](https://support.huaweicloud.com/productdesc-drs/drs_01_0302.html)。
-   参见[使用须知](https://support.huaweicloud.com/qs-drs/drs_06_0003.html)。

## 操作步骤<a name="section12451414195820"></a>

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

    **图 2**  DDM到Kafka同步实例信息<a name="fig123764616489"></a>  
    ![](figures/DDM到Kafka同步实例信息.png "DDM到Kafka同步实例信息")

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
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p10323458361"><a name="p10323458361"></a><a name="p10323458361"></a>选择<span class="uicontrol" id="uicontrol1422913280188"><a name="uicontrol1422913280188"></a><a name="uicontrol1422913280188"></a>“出云”</span>。</p>
    </td>
    </tr>
    <tr id="row0414184610580"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1414046115813"><a name="p1414046115813"></a><a name="p1414046115813"></a>源数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p168249357197"><a name="p168249357197"></a><a name="p168249357197"></a>选择<span class="uicontrol" id="uicontrol051853118180"><a name="uicontrol051853118180"></a><a name="uicontrol051853118180"></a>“DDM”</span>。</p>
    </td>
    </tr>
    <tr id="row42411630204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p12790028204436"><a name="p12790028204436"></a><a name="p12790028204436"></a>目标数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1969552512018"><a name="p1969552512018"></a><a name="p1969552512018"></a>选择<span class="uicontrol" id="uicontrol154014364188"><a name="uicontrol154014364188"></a><a name="uicontrol154014364188"></a>“Kafka”</span>。</p>
    </td>
    </tr>
    <tr id="row62907306204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p62327044204436"><a name="p62327044204436"></a><a name="p62327044204436"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p87075558433"><a name="p87075558433"></a><a name="p87075558433"></a>此处以<span class="uicontrol" id="uicontrol12676440161816"><a name="uicontrol12676440161816"></a><a name="uicontrol12676440161816"></a>“公网网络”</span>为示例。目前支持可选公网网络、VPC网络和VPN、专线网络。</p>
    </td>
    </tr>
    <tr id="row658644204515"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p202721112171115"><a name="p202721112171115"></a><a name="p202721112171115"></a>源数据库实例</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p26397538204515"><a name="p26397538204515"></a><a name="p26397538204515"></a>可用的DDM实例。</p>
    </td>
    </tr>
    <tr id="row15177111612817"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p01021256155315"><a name="p01021256155315"></a><a name="p01021256155315"></a>同步实例所在子网</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p122632913613"><a name="p122632913613"></a><a name="p122632913613"></a>请选择同步实例所在的子网。也可以单击“查看子网”，跳转至“网络控制台”查看实例所在子网帮助选择。</p>
    <p id="p112261929960"><a name="p112261929960"></a><a name="p112261929960"></a>默认值为当前所选数据库实例所在子网，请选择有可用IP地址的子网。为确保同步实例创建成功，仅显示已经开启DHCP的子网。</p>
    </td>
    </tr>
    <tr id="row1169913195320"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p06786155538"><a name="p06786155538"></a><a name="p06786155538"></a>同步类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1767891515533"><a name="p1767891515533"></a><a name="p1767891515533"></a>增量。</p>
    <p id="p0678161516531"><a name="p0678161516531"></a><a name="p0678161516531"></a>增量同步通过解析日志等技术，将源端产生的增量<span id="text1688771251"><a name="text1688771251"></a><a name="text1688771251"></a>实时同步</span>至目标端。</p>
    <p id="p17241506610"><a name="p17241506610"></a><a name="p17241506610"></a>无需中断业务，实现同步过程中源业务和数据库继续对外提供访问。</p>
    </td>
    </tr>
    <tr id="row1112613477361"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1017716536718"><a name="p1017716536718"></a><a name="p1017716536718"></a>企业项目</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p795282881017"><a name="p795282881017"></a><a name="p795282881017"></a>对于已成功关联企业项目的用户，仅需在“企业项目”下拉框中选择目标项目。</p>
    <p id="p8952152819109"><a name="p8952152819109"></a><a name="p8952152819109"></a>如果需要自定义企业项目，请前往项目管理服务进行创建。关于如何创建项目，详见《项目管理用户指南》。</p>
    </td>
    </tr>
    <tr id="row11681455143620"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1276314133599"><a name="p1276314133599"></a><a name="p1276314133599"></a>标签</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p14349194793116"><a name="p14349194793116"></a><a name="p14349194793116"></a>可选配置，对同步任务的标识。使用标签可方便管理您的<span id="drs_06_0005_text947798304"><a name="drs_06_0005_text947798304"></a><a name="drs_06_0005_text947798304"></a>实时同步</span>任务。每个任务最多支持10个标签配额。</p>
    <p id="p8307101212113"><a name="p8307101212113"></a><a name="p8307101212113"></a>任务创建成功后，您可以单击实例名称，在<span class="uicontrol" id="zh-cn_topic_0078078071_uicontrol1433412554316"><a name="zh-cn_topic_0078078071_uicontrol1433412554316"></a><a name="zh-cn_topic_0078078071_uicontrol1433412554316"></a>“标签”</span>页签下查看对应标签。关于标签的详细操作，请参见<a href="https://support.huaweicloud.com/usermanual-drs/drs_synchronization_tag.html" target="_blank" rel="noopener noreferrer">标签管理</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，同步实例创建成功后，填选源库信息和目标库信息，建议您单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，单击“下一步“。

    **图 3**  DDM出云源库信息<a name="fig20498162055215"></a>  
    ![](figures/DDM出云源库信息.png "DDM出云源库信息")

    **表 3**  源库信息

    <a name="zh-cn_topic_0135097933_table157461610185911"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0135097933_row15746151015912"><th class="cellrowborder" valign="top" width="23%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0135097933_p18746101055912"><a name="zh-cn_topic_0135097933_p18746101055912"></a><a name="zh-cn_topic_0135097933_p18746101055912"></a><strong id="zh-cn_topic_0135097933_b074631019593"><a name="zh-cn_topic_0135097933_b074631019593"></a><a name="zh-cn_topic_0135097933_b074631019593"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="77%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0135097933_p15746181055920"><a name="zh-cn_topic_0135097933_p15746181055920"></a><a name="zh-cn_topic_0135097933_p15746181055920"></a><strong id="zh-cn_topic_0135097933_b1774613108597"><a name="zh-cn_topic_0135097933_b1774613108597"></a><a name="zh-cn_topic_0135097933_b1774613108597"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0135097933_row0746151020595"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p1674610102597"><a name="zh-cn_topic_0135097933_p1674610102597"></a><a name="zh-cn_topic_0135097933_p1674610102597"></a>数据库实例名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p3746710165918"><a name="zh-cn_topic_0135097933_p3746710165918"></a><a name="zh-cn_topic_0135097933_p3746710165918"></a>默认为创建迁移任务时选择的关系型数据库实例，不可进行修改。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row107461010135910"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p86531023135911"><a name="zh-cn_topic_0135097933_p86531023135911"></a><a name="zh-cn_topic_0135097933_p86531023135911"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p665318234591"><a name="zh-cn_topic_0135097933_p665318234591"></a><a name="zh-cn_topic_0135097933_p665318234591"></a>源数据库的用户名。</p>
    </td>
    </tr>
    <tr id="row14154134183419"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p1470623191117"><a name="p1470623191117"></a><a name="p1470623191117"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p127064313117"><a name="p127064313117"></a><a name="p127064313117"></a>源数据库的用户名所对应的密码。</p>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >**源数据库IP地址、端口、用户名和密码将在同步过程中被加密暂存到数据库和同步实例主机上，待该任务删除后会永久清除。**

    **图 4**  Kafka目标库信息<a name="fig1592113195219"></a>  
    ![](figures/Kafka目标库信息.png "Kafka目标库信息")

    **表 4**  源库信息

    <a name="table670434692318"></a>
    <table><thead align="left"><tr id="row1370444614233"><th class="cellrowborder" valign="top" width="23.29%" id="mcps1.2.3.1.1"><p id="p0704346192311"><a name="p0704346192311"></a><a name="p0704346192311"></a><strong id="b1470410468238"><a name="b1470410468238"></a><a name="b1470410468238"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.71%" id="mcps1.2.3.1.2"><p id="p1470417467233"><a name="p1470417467233"></a><a name="p1470417467233"></a><strong id="b670424615238"><a name="b670424615238"></a><a name="b670424615238"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row27051946102314"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p6705174662310"><a name="p6705174662310"></a><a name="p6705174662310"></a>IP地址或域名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p570512469237"><a name="p570512469237"></a><a name="p570512469237"></a>目标数据库的IP地址或域名。</p>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >**目标数据库的用户名和密码将在同步过程中被加密暂存到数据库和同步实例主机上，待该任务删除后会永久清除。**

4.  在“设置同步“页面，选择同步策略、数据格式和同步对象，单击“下一步“。

    **图 5**  DDM到Kafka同步模式<a name="fig14025637142814"></a>  
    ![](figures/DDM到Kafka同步模式.png "DDM到Kafka同步模式")

    **表 5**  同步对象

    <a name="table165921932111919"></a>
    <table><thead align="left"><tr id="row165921632141911"><th class="cellrowborder" valign="top" width="16%" id="mcps1.2.3.1.1"><p id="p1759233261916"><a name="p1759233261916"></a><a name="p1759233261916"></a><strong id="b1783318515228"><a name="b1783318515228"></a><a name="b1783318515228"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="84%" id="mcps1.2.3.1.2"><p id="p159273271920"><a name="p159273271920"></a><a name="p159273271920"></a><strong id="b10555114922418"><a name="b10555114922418"></a><a name="b10555114922418"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row61064915127"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p1107109131214"><a name="p1107109131214"></a><a name="p1107109131214"></a>同步Topic策略</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p02621419181419"><a name="p02621419181419"></a><a name="p02621419181419"></a>同步Topic策略，可选择“集中投递到一个Topic”或者“自动生成Topic名字”。</p>
    </td>
    </tr>
    <tr id="row61271125113917"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p71288255399"><a name="p71288255399"></a><a name="p71288255399"></a>Topic</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p71281325133915"><a name="p71281325133915"></a><a name="p71281325133915"></a>选择目标端需要同步到的Topic，同步Topic策略选择“集中投递到一个Topic”时可见。</p>
    </td>
    </tr>
    <tr id="row14912505165"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p11961454181616"><a name="p11961454181616"></a><a name="p11961454181616"></a>Topic名字格式</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p10968540163"><a name="p10968540163"></a><a name="p10968540163"></a>Topic名字格式，同步Topic策略选择“自动生成Topic名字”时可见。</p>
    <p id="p15920547113214"><a name="p15920547113214"></a><a name="p15920547113214"></a>Topic名字格式支持database和tablename两个变量，其他字符都当做常量。分别用$database$代替数据库名，$tablename$代替表名。</p>
    <p id="p11921124716323"><a name="p11921124716323"></a><a name="p11921124716323"></a>例如：配置成$database$-$tablename$时，如果数据库名称为db1，表名为tab1，则Topic名字为db1-tab1。如果是DDL语句，$tablename$为空，则Topic名字为db1.</p>
    </td>
    </tr>
    <tr id="row16571125965410"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p05721159205410"><a name="p05721159205410"></a><a name="p05721159205410"></a>同步到kafka partition策略</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p1709291615"><a name="p1709291615"></a><a name="p1709291615"></a>同步到kafka partition策略。</p>
    <a name="ul1175313402567"></a><a name="ul1175313402567"></a><ul id="ul1175313402567"><li>按库名+表名的hash值投递到不同Partition：适用于单表的查询场景，表内保序，表与表之间不保序，可以提高单表读写性能，推荐使用此选项。</li><li>全部投递到Partition 0：适用于有事务要求的场景，事务保序，可以保证完全按照事务顺序消费，写入性能比较差，如果没有强事务要求，不推荐使用此选项。投递到Partition 0必须是自动创建Topic，选择已有Topic不支持该选项。</li><li>按表的主键值hash值投递到不同的Partion：适用于一个表一个Topic的场景。</li></ul>
    </td>
    </tr>
    <tr id="row18351020113612"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p1351122017367"><a name="p1351122017367"></a><a name="p1351122017367"></a>投送到kafka的数据格式</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p114861232381"><a name="p114861232381"></a><a name="p114861232381"></a>选择投送到kafka的数据格式。</p>
    <a name="ul574420499552"></a><a name="ul574420499552"></a><ul id="ul574420499552"><li>Avro：可以显示Avro二进制编码，高效获取数据。</li><li>JSON：为Json消息格式，方便解释格式，但需要占用更多的空间。</li><li>JSON-C：一种能够兼容多个批量，流式计算框架的数据格式。</li></ul>
    <p id="p97597118202"><a name="p97597118202"></a><a name="p97597118202"></a>详细格式可参考<a href="Kafka消息格式.md">Kafka消息格式</a>。</p>
    </td>
    </tr>
    <tr id="row559273214193"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p14592132171916"><a name="p14592132171916"></a><a name="p14592132171916"></a>同步对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p85921932191910"><a name="p85921932191910"></a><a name="p85921932191910"></a>同步对象支持表级同步和库级同步，您可以根据业务场景选择对应的数据进行同步。</p>
    <p id="p1827094910335"><a name="p1827094910335"></a><a name="p1827094910335"></a>选择对象的时候支持搜索，以便您快速选择需要的数据库对象。</p>
    </td>
    </tr>
    </tbody>
    </table>

5.  在“预检查“页面，进行同步任务预校验，校验是否可进行实时同步。
    -   查看检查结果，如有不通过的检查项，需要修复不通过项后，单击“重新校验”按钮重新进行任务预校验。

        预检查不通过项处理建议请参见《数据复制服务用户指南》中的“[预检查不通过项修复方法](https://support.huaweicloud.com/usermanual-drs/drs_precheck.html)”。

    -   预检查完成后，且所有检查项结果均通过时，单击“下一步“。

        **图 6**  DDM到Kafka预检查<a name="zh-cn_topic_0188781319_fig783414142414"></a>  
        ![](figures/DDM到Kafka预检查.png "DDM到Kafka预检查")

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >所有检查项结果均通过时，若存在待确认项，需要阅读并确认详情后才可以继续执行下一步操作。


6.  在“任务确认“页面，设置同步任务的启动时间，并确认同步任务信息无误后，勾选协议，单击“启动任务“，提交同步任务。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   同步任务的启动时间可以根据业务需求，设置为“立即启动”或“稍后启动”。
    >-   预计同步任务启动后，会对源数据库和目标数据库的性能产生影响，建议选择业务低峰期，合理设置同步任务的启动时间。

7.  同步任务提交后，您可在“实时同步管理“页面，查看并管理自己的任务。
    -   您可查看任务提交后的状态，状态请参见[任务状态](https://support.huaweicloud.com/qs-drs/drs_06_0004.html)。
    -   在任务列表的右上角，单击![](figures/kwx318612-GAUSS-DBaaS-image-a8fbc7b6-eab2-4798-b522-174e36341a92.png)刷新列表，可查看到最新的任务状态。



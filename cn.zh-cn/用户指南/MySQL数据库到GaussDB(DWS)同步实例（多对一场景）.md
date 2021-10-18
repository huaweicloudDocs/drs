# MySQL数据库到GaussDB\(DWS\)同步实例（多对一场景）<a name="drs_03_0040"></a>

本小节以RDS for MySQL-\>GaussDB\(DWS\)多对一场景的实时同步为示例，介绍如何使用数据复制服务配置实时同步任务。

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

    <a name="table72481933193813"></a>
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

    **图 2**  MySQL到GaussDB\(DWS\)同步实例信息\(VPC网络\)<a name="fig64227355911"></a>  
    ![](figures/MySQL到GaussDB(DWS)同步实例信息(VPC网络).png "MySQL到GaussDB(DWS)同步实例信息(VPC网络)")

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
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p168249357197"><a name="p168249357197"></a><a name="p168249357197"></a>选择<span class="uicontrol" id="uicontrol051853118180"><a name="uicontrol051853118180"></a><a name="uicontrol051853118180"></a>“MySQL”</span>。</p>
    </td>
    </tr>
    <tr id="row42411630204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p12790028204436"><a name="p12790028204436"></a><a name="p12790028204436"></a>目标数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1969552512018"><a name="p1969552512018"></a><a name="p1969552512018"></a>选择<span class="uicontrol" id="uicontrol154014364188"><a name="uicontrol154014364188"></a><a name="uicontrol154014364188"></a>“<span id="text65053161335"><a name="text65053161335"></a><a name="text65053161335"></a>GaussDB(DWS)</span>”</span>。</p>
    </td>
    </tr>
    <tr id="row62907306204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p62327044204436"><a name="p62327044204436"></a><a name="p62327044204436"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p87075558433"><a name="p87075558433"></a><a name="p87075558433"></a>此处以<span class="uicontrol" id="uicontrol12676440161816"><a name="uicontrol12676440161816"></a><a name="uicontrol12676440161816"></a>“VPC网络”</span>为示例。目前支持可选公网网络和VPC网络。</p>
    </td>
    </tr>
    <tr id="row658644204515"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p53350183204515"><a name="p53350183204515"></a><a name="p53350183204515"></a>目标数据库实例</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p26397538204515"><a name="p26397538204515"></a><a name="p26397538204515"></a>可用的<span id="text112607233338"><a name="text112607233338"></a><a name="text112607233338"></a>GaussDB(DWS)</span>实例。</p>
    </td>
    </tr>
    <tr id="row15177111612817"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p01021256155315"><a name="p01021256155315"></a><a name="p01021256155315"></a>同步实例所在子网</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p18102456175315"><a name="p18102456175315"></a><a name="p18102456175315"></a>请选择同步实例所在的子网。也可以单击“查看子网”，跳转至“网络控制台”查看实例所在子网帮助选择。</p>
    <p id="p47671146133910"><a name="p47671146133910"></a><a name="p47671146133910"></a>默认值为当前所选数据库实例所在子网，请选择有可用IP地址的子网。为确保同步实例创建成功，仅显示已经开启DHCP的子网。</p>
    </td>
    </tr>
    <tr id="row1169913195320"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p06786155538"><a name="p06786155538"></a><a name="p06786155538"></a>同步类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p3659125011577"><a name="p3659125011577"></a><a name="p3659125011577"></a>全量+增量</p>
    <p id="p9660115025713"><a name="p9660115025713"></a><a name="p9660115025713"></a>该模式为数据持续性实时同步，通过全量过程完成目标端数据库的初始化后，增量同步阶段通过解析日志等技术，将源端和目标端数据保持数据持续一致。</p>
    <div class="note" id="note3678415155319"><a name="note3678415155319"></a><a name="note3678415155319"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p16678121514537"><a name="p16678121514537"></a><a name="p16678121514537"></a>选择<span class="uicontrol" id="uicontrol18678615205315"><a name="uicontrol18678615205315"></a><a name="uicontrol18678615205315"></a>“全量+增量”</span>同步模式，增量同步可以在全量同步完成的基础上实现数据的持续同步，无需中断业务，实现同步过程中源业务和数据库继续对外提供访问。</p>
    </div></div>
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
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p941692643313"><a name="p941692643313"></a><a name="p941692643313"></a>可选配置，对同步任务的标识。使用标签可方便管理您的<span id="drs_06_0005_text947798304"><a name="drs_06_0005_text947798304"></a><a name="drs_06_0005_text947798304"></a>实时同步</span>任务。每个任务最多支持10个标签配额。</p>
    <p id="p8307101212113"><a name="p8307101212113"></a><a name="p8307101212113"></a>任务创建成功后，您可以单击实例名称，在<span class="uicontrol" id="zh-cn_topic_0078078071_uicontrol1433412554316"><a name="zh-cn_topic_0078078071_uicontrol1433412554316"></a><a name="zh-cn_topic_0078078071_uicontrol1433412554316"></a>“标签”</span>页签下查看对应标签。关于标签的详细操作，请参见<a href="https://support.huaweicloud.com/usermanual-drs/drs_synchronization_tag.html" target="_blank" rel="noopener noreferrer">标签管理</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，同步实例创建成功后，填选源库信息和目标库信息，建议您单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，勾选协议，单击“下一步“。

    **图 3**  MySQL源库信息\(VPC网络\)<a name="fig20498162055215"></a>  
    ![](figures/MySQL源库信息(VPC网络).png "MySQL源库信息(VPC网络)")

    **表 3**  源库信息

    <a name="table5457114616020"></a>
    <table><thead align="left"><tr id="row64572461706"><th class="cellrowborder" valign="top" width="23.27%" id="mcps1.2.3.1.1"><p id="p1245711467016"><a name="p1245711467016"></a><a name="p1245711467016"></a><strong id="b154574464019"><a name="b154574464019"></a><a name="b154574464019"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.73%" id="mcps1.2.3.1.2"><p id="p945754617013"><a name="p945754617013"></a><a name="p945754617013"></a><strong id="b2045744616014"><a name="b2045744616014"></a><a name="b2045744616014"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row119266691013"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="p1792711611016"><a name="p1792711611016"></a><a name="p1792711611016"></a>源库类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="p592712631010"><a name="p592712631010"></a><a name="p592712631010"></a>源数据库类型，可选“ECS自建库”和“RDS实例”，此处以<span class="uicontrol" id="uicontrol7968142821515"><a name="uicontrol7968142821515"></a><a name="uicontrol7968142821515"></a>“RDS实例”</span>为示例。</p>
    </td>
    </tr>
    <tr id="row194573467019"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="p16457134611018"><a name="p16457134611018"></a><a name="p16457134611018"></a>数据库实例名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="p1745714461609"><a name="p1745714461609"></a><a name="p1745714461609"></a>选择待同步的RDS实例。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row9653102325913"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="p379718114"><a name="p379718114"></a><a name="p379718114"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="p17971681118"><a name="p17971681118"></a><a name="p17971681118"></a>源数据库的用户名。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row065352315596"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="p187971581712"><a name="p187971581712"></a><a name="p187971581712"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="p18797208618"><a name="p18797208618"></a><a name="p18797208618"></a>源数据库的用户名所对应的密码。</p>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >**源数据库的数据库用户名和密码，会被系统加密暂存，直至删除该任务后自动清除。**

    **图 4**  GaussDB\(DWS\)目标库信息<a name="fig13180125314180"></a>  
    ![](figures/GaussDB(DWS)目标库信息.png "GaussDB(DWS)目标库信息")

    **表 4**  目标库信息

    <a name="zh-cn_topic_0135097933_table157461610185911"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0135097933_row15746151015912"><th class="cellrowborder" valign="top" width="23%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0135097933_p18746101055912"><a name="zh-cn_topic_0135097933_p18746101055912"></a><a name="zh-cn_topic_0135097933_p18746101055912"></a><strong id="zh-cn_topic_0135097933_b074631019593"><a name="zh-cn_topic_0135097933_b074631019593"></a><a name="zh-cn_topic_0135097933_b074631019593"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="77%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0135097933_p15746181055920"><a name="zh-cn_topic_0135097933_p15746181055920"></a><a name="zh-cn_topic_0135097933_p15746181055920"></a><strong id="zh-cn_topic_0135097933_b1774613108597"><a name="zh-cn_topic_0135097933_b1774613108597"></a><a name="zh-cn_topic_0135097933_b1774613108597"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0135097933_row0746151020595"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p1674610102597"><a name="zh-cn_topic_0135097933_p1674610102597"></a><a name="zh-cn_topic_0135097933_p1674610102597"></a>数据库实例名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p3746710165918"><a name="zh-cn_topic_0135097933_p3746710165918"></a><a name="zh-cn_topic_0135097933_p3746710165918"></a>默认为创建同步任务时选择的关系型数据库实例，不可进行修改。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row2746310155916"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p18746310175911"><a name="zh-cn_topic_0135097933_p18746310175911"></a><a name="zh-cn_topic_0135097933_p18746310175911"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p874691012591"><a name="zh-cn_topic_0135097933_p874691012591"></a><a name="zh-cn_topic_0135097933_p874691012591"></a>目标数据库对应的数据库用户名。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row107461010135910"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p47463101599"><a name="zh-cn_topic_0135097933_p47463101599"></a><a name="zh-cn_topic_0135097933_p47463101599"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p47461410155914"><a name="zh-cn_topic_0135097933_p47461410155914"></a><a name="zh-cn_topic_0135097933_p47461410155914"></a>数据库用户名和密码将被系统加密暂存，直至该任务删除后清除。</p>
    </td>
    </tr>
    </tbody>
    </table>

4.  在“设置同步“页面，选择同步对象类型和同步对象。单击“下一步“。

    **图 5**  MySQL到GaussDB\(DWS\) 同步模式<a name="fig14025637142814"></a>  
    ![](figures/MySQL到GaussDB(DWS)-同步模式.png "MySQL到GaussDB(DWS)-同步模式")

    **表 5**  同步模式和对象

    <a name="table145503432154"></a>
    <table><thead align="left"><tr id="row8551543131515"><th class="cellrowborder" valign="top" width="18.58%" id="mcps1.2.3.1.1"><p id="p17551184313154"><a name="p17551184313154"></a><a name="p17551184313154"></a><strong id="b16551134381519"><a name="b16551134381519"></a><a name="b16551134381519"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="81.42%" id="mcps1.2.3.1.2"><p id="p105511643151512"><a name="p105511643151512"></a><a name="p105511643151512"></a><strong id="b13551174321519"><a name="b13551174321519"></a><a name="b13551174321519"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1759750171316"><td class="cellrowborder" valign="top" width="18.58%" headers="mcps1.2.3.1.1 "><p id="p62641951123917"><a name="p62641951123917"></a><a name="p62641951123917"></a>流速模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.42%" headers="mcps1.2.3.1.2 "><p id="p6265105163918"><a name="p6265105163918"></a><a name="p6265105163918"></a>流速模式支持限速和不限速，默认为不限速。</p>
    <a name="ul142651151123918"></a><a name="ul142651151123918"></a><ul id="ul142651151123918"><li>限速<p id="p1026565110390"><a name="p1026565110390"></a><a name="p1026565110390"></a>自定义的最大同步速度，全量同步过程中的同步速度将不会超过该速度。</p>
    <p id="p9266851103914"><a name="p9266851103914"></a><a name="p9266851103914"></a>当流速模式选择了“限速”时，你需要通过流速设置来定时控制同步速度。流速设置通常包括限速时间段和流速大小的设置。默认的限速时间段为全天限流，您也可以根据业务需求自定义时段限流。自定义的时段限流支持最多设置3个定时任务，每个定时任务之间不能存在交叉的时间段，未设定在限速时间段的时间默认为不限速。</p>
    <p id="p1826625163912"><a name="p1826625163912"></a><a name="p1826625163912"></a>流速的大小需要根据业务场景来设置，不能超过9999MB/s。</p>
    <div class="fignone" id="fig1326635163917"><a name="fig1326635163917"></a><a name="fig1326635163917"></a><span class="figcap"><b>图1 </b>MySQL到GaussDB(DWS) 设置流速模式</span><br><a name="image1266125119393"></a><a name="image1266125119393"></a><span><img id="image1266125119393" src="figures/MySQL到GaussDB(DWS)-设置流速模式.png" height="159.61197" width="352.1175"></span></div>
    </li><li>不限速<div class="p" id="p112664518395"><a name="p112664518395"></a><a name="p112664518395"></a>对同步速度不进行限制，通常会最大化使用源数据库的出口带宽。该流速模式同时会对源数据库造成读消耗，消耗取决于源数据库的出口带宽。比如源数据库的出口带宽为100MB/s，假设高速模式使用了80%带宽，则同步对源数据库将造成80MB/s的读操作IO消耗。<div class="note" id="note1426618512396"><a name="note1426618512396"></a><a name="note1426618512396"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul4267135143911"></a><a name="ul4267135143911"></a><ul id="ul4267135143911"><li>限速模式只对全量阶段生效，增量阶段不生效。</li><li>您也可以在创建任务后修改流速模式。具体方法请参见<a href="https://support.huaweicloud.com/usermanual-drs/drs_10_0401.html" target="_blank" rel="noopener noreferrer">修改流速模式</a>。</li></ul>
    </div></div>
    </div>
    </li></ul>
    </td>
    </tr>
    <tr id="row19367182916553"><td class="cellrowborder" valign="top" width="18.58%" headers="mcps1.2.3.1.1 "><p id="p1194016252191"><a name="p1194016252191"></a><a name="p1194016252191"></a>同步对象类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.42%" headers="mcps1.2.3.1.2 "><p id="p65772810236"><a name="p65772810236"></a><a name="p65772810236"></a>可选同步表结构、同步数据、同步索引，根据实际需求进行选择要同步内容。</p>
    <a name="ul9359134216234"></a><a name="ul9359134216234"></a><ul id="ul9359134216234"><li>同步数据为必选项。</li><li>选择同步表结构的时候目标库不能有同名的表。</li><li>不选同步表结构的时候目标库必须有相应的表，且要保证表结构与所选表结构相同。</li></ul>
    </td>
    </tr>
    <tr id="row24118316505"><td class="cellrowborder" valign="top" width="18.58%" headers="mcps1.2.3.1.1 "><p id="p34253145015"><a name="p34253145015"></a><a name="p34253145015"></a>增量阶段冲突策略</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.42%" headers="mcps1.2.3.1.2 "><p id="p1042113155012"><a name="p1042113155012"></a><a name="p1042113155012"></a>该冲突策略特指增量同步中的冲突处理策略，全量阶段的冲突默认忽略。</p>
    </td>
    </tr>
    <tr id="row16476034203"><td class="cellrowborder" valign="top" width="18.58%" headers="mcps1.2.3.1.1 "><p id="p14592132171916"><a name="p14592132171916"></a><a name="p14592132171916"></a>同步对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.42%" headers="mcps1.2.3.1.2 "><p id="p174271414164712"><a name="p174271414164712"></a><a name="p174271414164712"></a>可选表级同步、库级同步、导入对象文件，您可以根据业务场景选择对应的数据进行同步。</p>
    <a name="ul24981905240"></a><a name="ul24981905240"></a><ul id="ul24981905240"><li>选择数据的时候支持搜索，以便您快速选择需要的数据库对象。</li><li>可以使用对象名映射功能进行源数据库和目标数据库中的同步对象映射，具体操作可参考<a href="对象名映射.md">对象名映射</a>。</li><li>如果有切换源数据库的操作，请在选择同步对象前单击右上角的<a name="image59959528353"></a><a name="image59959528353"></a><span><img id="image59959528353" src="figures/icon-刷新.png"></span>，以确保待选择的对象为最新源数据库对象。</li></ul>
    <a name="ul15632207202419"></a><a name="ul15632207202419"></a><ul id="ul15632207202419"><li>选择<span class="uicontrol" id="uicontrol165312532262"><a name="uicontrol165312532262"></a><a name="uicontrol165312532262"></a>“导入对象文件”</span>，具体操作如下：<a name="ol17531615252"></a><a name="ol17531615252"></a><ol id="ol17531615252"><li>单击<span class="uicontrol" id="uicontrol99651412274"><a name="uicontrol99651412274"></a><a name="uicontrol99651412274"></a>“下载模板”</span>。</li><li>在下载的Excel模板中，填写需要导入的对象信息。</li><li>单击<span class="uicontrol" id="uicontrol22492394277"><a name="uicontrol22492394277"></a><a name="uicontrol22492394277"></a>“添加文件”</span>，在对话框中选择编辑完成的模板。</li><li>单击<span class="uicontrol" id="uicontrol163306420277"><a name="uicontrol163306420277"></a><a name="uicontrol163306420277"></a>“上传文件”</span>。</li></ol>
    <div class="note" id="note20738054164915"><a name="note20738054164915"></a><a name="note20738054164915"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul127396547493"></a><a name="ul127396547493"></a><ul id="ul127396547493"><li>文件导入仅支持导入Windows Microsoft Excel 97-2003版本（*.xls），2007及以上版本（*.xlsx）的文件，下载的压缩包提供上述两个版本模板。</li><li>文件名支持的有效字符：大小写字母，数字，“-”，“_”,“(”，“)”</li><li>模板中的对象信息需按照SchemaName.TableName的格式进行填写，不支持“&lt;”，“&gt;”，"."和“"”，且不支持以空格开头或结尾的对象。</li><li>文件导入成功后，必须保留本次上传的文件，以便需要再编辑该任务的数据库对象范围时，可直接基于此文件修改，然后再次上传。</li><li>用文件导入功能所创建的任务，任务启动之后再编辑时，不支持切换到“表级同步”和“库级同步”功能。</li><li>配置中的任务，可使用“表级同步”，“库级同步”或“文件导入”三种方式，每次切换新的方式后，当前选择或者导入的数据库对象被清空，需重新选择或导入。</li><li>任务再编辑导入对象时，将自动弹出增加和删除的对象。</li><li>上传文件后校验失败，可单击“查看失败详情”下载错误信息。</li></ul>
    </div></div>
    </li></ul>
    </td>
    </tr>
    </tbody>
    </table>

    在选择同步对象阶段可通过设置映射关系，实现多张表对GaussDB\(DWS\)一张表的同步。

    1.  在同步对象右侧已选对象框中，选择需要进行映射的表，单击“编辑“按钮。
    2.  在“编辑库名和表名“的弹出框中，填写新的数据库名和新表名，单击“是“，修改后的名称即为保存在目标数据库中的库名。

        **图 7**  编辑库名和表名<a name="fig1793411269416"></a>  
        ![](figures/编辑库名和表名.png "编辑库名和表名")

    3.  文件导入对象也支持多张表对GaussDB\(DWS\)一张表的映射，由于消息体限制最多导入10000个表（表名长度过长或者规则过长也会影响导入数量）。

        >![](public_sys-resources/icon-caution.gif) **注意：** 
        >-   使用多对一操作时，需要使用数据加工的附加列操作来避免数据冲突。
        >-   源库和目标库多对一的表的结构要一致。


5.  在“数据加工“页面，选择需要加工的表对象，填写需要添加的列名、类型、操作类型信息，检查无误后，单击“下一步“。

    **图 8**  MySQL到GaussDB\(DWS\) 数据加工<a name="fig3318173591414"></a>  
    ![](figures/MySQL到GaussDB(DWS)-数据加工.png "MySQL到GaussDB(DWS)-数据加工")

    >![](public_sys-resources/icon-caution.gif) **注意：** 
    >-   不允许对唯一主键列进行数据加工。
    >-   “以serverName@database@table为列填充列”该操作会使用@符号拼接serverName、源库的库名和表名填充新加的列，并且该列会与源端表的主键形成复合主键。

6.  在“预检查“页面，进行同步任务预校验，校验是否可进行实时同步。
    -   查看检查结果，如有不通过的检查项，需要修复不通过项后，单击“重新校验”按钮重新进行任务预校验。

        预检查不通过项处理建议请参见《数据复制服务用户指南》中的“[预检查不通过项修复方法](https://support.huaweicloud.com/usermanual-drs/drs_precheck.html)”。

    -   预检查完成后，且所有检查项结果均通过时，单击“下一步“。

        **图 9**  同步预检查<a name="drs_06_0005_fig23361684715"></a>  
        ![](figures/同步预检查.png "同步预检查")

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >所有检查项结果均通过时，若存在请确认项，需要阅读并确认详情后才可以继续执行下一步操作。


7.  在“任务确认“页面，设置同步任务的启动时间，并确认同步任务信息无误后，勾选协议，单击“启动任务“，提交同步任务。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   同步任务的启动时间可以根据业务需求，设置为“立即启动”或“稍后启动”。
    >-   预计同步任务启动后，会对源数据库和目标数据库的性能产生影响，建议选择业务低峰期，合理设置同步任务的启动时间。

8.  同步任务提交后，您可在“实时同步管理“页面，查看并管理自己的任务。
    -   您可查看任务提交后的状态，状态请参见[任务状态](https://support.huaweicloud.com/qs-drs/drs_06_0004.html)。
    -   在任务列表的右上角，单击![](figures/icon-刷新.png)刷新列表，可查看到最新的任务状态。



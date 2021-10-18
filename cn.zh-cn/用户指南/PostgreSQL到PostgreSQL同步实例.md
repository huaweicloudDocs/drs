# PostgreSQL到PostgreSQL同步实例<a name="drs_11_0452"></a>

本小节以PostgreSQL-\>PostgreSQL的入云同步为示例，介绍如何使用数据复制服务配置实时同步任务。

## 前提条件<a name="section2097363117427"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   参见[实时同步](https://support.huaweicloud.com/productdesc-drs/drs_01_0302.html)。
-   参见[使用须知](https://support.huaweicloud.com/qs-drs/drs_06_0003.html)。

## 操作步骤<a name="section429621210368"></a>

1.  在“实时同步管理”页面，单击“创建同步任务”。
2.  在“同步实例”页面，填选区域、任务名称、任务异常通知信息、SMN主题、时延阈值、任务异常自动结束时间、描述、同步实例信息，单击“下一步”。

    **图 1**  同步任务信息<a name="fig1482755010405"></a>  
    ![](figures/同步任务信息.png "同步任务信息")

    **表 1**  任务和描述

    <a name="table10284161414418"></a>
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

    **图 2**  PostgreSQL同步实例信息<a name="fig123764616489"></a>  
    ![](figures/PostgreSQL同步实例信息.png "PostgreSQL同步实例信息")

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
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p168249357197"><a name="p168249357197"></a><a name="p168249357197"></a>选择<span class="uicontrol" id="uicontrol051853118180"><a name="uicontrol051853118180"></a><a name="uicontrol051853118180"></a>“PostgreSQL”</span>。</p>
    </td>
    </tr>
    <tr id="row42411630204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p12790028204436"><a name="p12790028204436"></a><a name="p12790028204436"></a>目标数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1969552512018"><a name="p1969552512018"></a><a name="p1969552512018"></a>选择<span class="uicontrol" id="uicontrol13830131163712"><a name="uicontrol13830131163712"></a><a name="uicontrol13830131163712"></a>“PostgreSQL”</span> 。</p>
    </td>
    </tr>
    <tr id="row62907306204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p62327044204436"><a name="p62327044204436"></a><a name="p62327044204436"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p87075558433"><a name="p87075558433"></a><a name="p87075558433"></a>此处以<span class="uicontrol" id="uicontrol12676440161816"><a name="uicontrol12676440161816"></a><a name="uicontrol12676440161816"></a>“VPC网络”</span>为示例。</p>
    </td>
    </tr>
    <tr id="row658644204515"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p53350183204515"><a name="p53350183204515"></a><a name="p53350183204515"></a>目标数据库实例</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p26397538204515"><a name="p26397538204515"></a><a name="p26397538204515"></a>目标数据库为关系型PostgreSQL数据库实例。</p>
    </td>
    </tr>
    <tr id="row198991858776"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p01021256155315"><a name="p01021256155315"></a><a name="p01021256155315"></a>同步实例所在子网</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0288918853_p18102456175315"><a name="zh-cn_topic_0288918853_p18102456175315"></a><a name="zh-cn_topic_0288918853_p18102456175315"></a>请选择同步实例所在的子网。也可以单击“查看子网”，跳转至“网络控制台”查看实例所在子网帮助选择。</p>
    <p id="zh-cn_topic_0288918853_p47671146133910"><a name="zh-cn_topic_0288918853_p47671146133910"></a><a name="zh-cn_topic_0288918853_p47671146133910"></a>默认值为当前所选数据库实例所在子网，请选择有可用IP地址的子网。为确保同步实例创建成功，仅显示已经开启DHCP的子网。</p>
    </td>
    </tr>
    <tr id="row1169913195320"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p06786155538"><a name="p06786155538"></a><a name="p06786155538"></a>同步类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1767891515533"><a name="p1767891515533"></a><a name="p1767891515533"></a>全量+增量：</p>
    <p id="p17241506610"><a name="p17241506610"></a><a name="p17241506610"></a>该模式为数据持续性实时同步，通过全量过程完成目标端数据库的初始化后，增量同步阶段通过解析日志等技术，将源端和目标端数据保持数据持续一致。</p>
    </td>
    </tr>
    <tr id="row143231850112715"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1017716536718"><a name="p1017716536718"></a><a name="p1017716536718"></a>企业项目</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p795282881017"><a name="p795282881017"></a><a name="p795282881017"></a>对于已成功关联企业项目的用户，仅需在“企业项目”下拉框中选择目标项目。</p>
    <p id="p8952152819109"><a name="p8952152819109"></a><a name="p8952152819109"></a>如果需要自定义企业项目，请前往项目管理服务进行创建。关于如何创建项目，详见《项目管理用户指南》。</p>
    </td>
    </tr>
    <tr id="row19775555162713"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1276314133599"><a name="p1276314133599"></a><a name="p1276314133599"></a>标签</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p26298276355"><a name="p26298276355"></a><a name="p26298276355"></a>可选配置，对同步任务的标识。使用标签可方便管理您的<span id="drs_06_0005_text947798304"><a name="drs_06_0005_text947798304"></a><a name="drs_06_0005_text947798304"></a>实时同步</span>任务。每个任务最多支持10个标签配额。</p>
    <p id="p8307101212113"><a name="p8307101212113"></a><a name="p8307101212113"></a>任务创建成功后，您可以单击实例名称，在<span class="uicontrol" id="zh-cn_topic_0078078071_uicontrol1433412554316"><a name="zh-cn_topic_0078078071_uicontrol1433412554316"></a><a name="zh-cn_topic_0078078071_uicontrol1433412554316"></a>“标签”</span>页签下查看对应标签。关于标签的详细操作，请参见<a href="https://support.huaweicloud.com/usermanual-drs/drs_synchronization_tag.html" target="_blank" rel="noopener noreferrer">标签管理</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，同步实例创建成功后，填选源库信息和目标库信息，建议您单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，勾选协议，单击“下一步“。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >此处源库类型分为ECS自建库和RDS实例，需要根据源数据库的实际来源选择相应的分类。两种场景下的参数配置不一样，需要根据具体场景进行配置。

    -   场景一：ECS自建库源库信息配置

        **图 3**  ECS自建PostgreSQL库场景源库信息<a name="fig4819182126"></a>  
        ![](figures/ECS自建PostgreSQL库场景源库信息.png "ECS自建PostgreSQL库场景源库信息")

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
        <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p2819421021"><a name="p2819421021"></a><a name="p2819421021"></a>选择<span class="uicontrol" id="uicontrol1143331018106"><a name="uicontrol1143331018106"></a><a name="uicontrol1143331018106"></a>“ECS自建库”</span>。</p>
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
        <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p68272021522"><a name="p68272021522"></a><a name="p68272021522"></a>通过该功能，用户可以选择是否开启对同步链路的加密。如果开启该功能，需要用户上传SSL CA根证书。</p>
        <div class="note" id="note118041213163"><a name="note118041213163"></a><a name="note118041213163"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul266710518121"></a><a name="ul266710518121"></a><ul id="ul266710518121"><li>最大支持上传500KB的证书文件。</li><li>如果不使用SSL证书，请自行承担数据安全风险。</li></ul>
        </div></div>
        </td>
        </tr>
        </tbody>
        </table>

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >**源数据库的IP地址或域名、数据库用户名和密码，会被系统加密暂存，直至删除该迁移任务后自动清除。**

    -   场景二：RDS实例源库信息配置

        **图 4**  RDS for PostgreSQL实例场景源库信息<a name="fig982712210213"></a>  
        ![](figures/RDS-for-PostgreSQL实例场景源库信息.png "RDS-for-PostgreSQL实例场景源库信息")

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
        <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p158276215212"><a name="p158276215212"></a><a name="p158276215212"></a>选择<span class="uicontrol" id="uicontrol1060175191019"><a name="uicontrol1060175191019"></a><a name="uicontrol1060175191019"></a>“RDS实例”</span>。</p>
        </td>
        </tr>
        <tr id="row1982742821"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p3827162426"><a name="p3827162426"></a><a name="p3827162426"></a>数据库实例名称</p>
        </td>
        <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p1082792823"><a name="p1082792823"></a><a name="p1082792823"></a>选择待同步的关系型PostgreSQL数据库实例作为源数据库实例。</p>
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

    **图 5**  PostgreSQL目标库信息<a name="fig1592113195219"></a>  
    ![](figures/PostgreSQL目标库信息.png "PostgreSQL目标库信息")

    **表 5**  目标库信息

    <a name="zh-cn_topic_0135097933_table1665310232597"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0135097933_row12653123195919"><th class="cellrowborder" valign="top" width="23.29%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0135097933_p156531623165916"><a name="zh-cn_topic_0135097933_p156531623165916"></a><a name="zh-cn_topic_0135097933_p156531623165916"></a><strong id="zh-cn_topic_0135097933_b20653923155913"><a name="zh-cn_topic_0135097933_b20653923155913"></a><a name="zh-cn_topic_0135097933_b20653923155913"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.71%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0135097933_p1365312365910"><a name="zh-cn_topic_0135097933_p1365312365910"></a><a name="zh-cn_topic_0135097933_p1365312365910"></a><strong id="zh-cn_topic_0135097933_b186531223105910"><a name="zh-cn_topic_0135097933_b186531223105910"></a><a name="zh-cn_topic_0135097933_b186531223105910"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0135097933_row1265352355912"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p921615874619"><a name="p921615874619"></a><a name="p921615874619"></a>数据库实例名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p6216185874614"><a name="p6216185874614"></a><a name="p6216185874614"></a>默认为创建迁移任务时选择的关系型PostgreSQL数据库实例，不可进行修改。</p>
    </td>
    </tr>
    <tr id="row233825074616"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p12217165811467"><a name="p12217165811467"></a><a name="p12217165811467"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p5217458114610"><a name="p5217458114610"></a><a name="p5217458114610"></a>目标数据库的用户名。</p>
    </td>
    </tr>
    <tr id="row8383114534615"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p122171758204619"><a name="p122171758204619"></a><a name="p122171758204619"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p721735824611"><a name="p721735824611"></a><a name="p721735824611"></a>目标数据库的用户名所对应的密码。</p>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >**源和目标数据库用户名和密码将在同步过程中被加密暂存到数据库和同步实例主机上，待该任务删除后会永久清除。**

4.  在“设置同步“页面，选择同步对象和同步用户，单击“下一步“。

    **图 6**  PostgreSQL同步模式<a name="fig14025637142814"></a>  
    ![](figures/PostgreSQL同步模式.png "PostgreSQL同步模式")

    **表 6**  同步对象

    <a name="table165921932111919"></a>
    <table><thead align="left"><tr id="row165921632141911"><th class="cellrowborder" valign="top" width="20%" id="mcps1.2.3.1.1"><p id="p1759233261916"><a name="p1759233261916"></a><a name="p1759233261916"></a><strong id="b1783318515228"><a name="b1783318515228"></a><a name="b1783318515228"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="80%" id="mcps1.2.3.1.2"><p id="p159273271920"><a name="p159273271920"></a><a name="p159273271920"></a><strong id="b10555114922418"><a name="b10555114922418"></a><a name="b10555114922418"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1016617632811"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p1416716102812"><a name="p1416716102812"></a><a name="p1416716102812"></a>增量阶段冲突策略</p>
    </td>
    <td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p3550125515228"><a name="p3550125515228"></a><a name="p3550125515228"></a>数据复制服务提供的<span id="text619486027"><a name="text619486027"></a><a name="text619486027"></a>实时同步</span>功能使用了主键或唯一键冲突策略，这些策略可以由您自主选择，尽可能保证源数据库中有主键约束或唯一键约束的表同步到目标数据库是符合预期的。</p>
    <p id="p1223813819246"><a name="p1223813819246"></a><a name="p1223813819246"></a>冲突策略目前支持如下三种形式：</p>
    <a name="ul4261248155512"></a><a name="ul4261248155512"></a><ul id="ul4261248155512"><li>忽略<p id="p01231425173720"><a name="p01231425173720"></a><a name="p01231425173720"></a>当同步数据与目标数据库已有数据冲突时（主键/唯一键存在重复等），将跳过冲突数据，继续进行后续同步。</p>
    </li><li>报错<p id="p3607133514375"><a name="p3607133514375"></a><a name="p3607133514375"></a>当同步数据与目标数据库已有数据冲突时（主键/唯一键存在重复等），同步任务将失败并立即中止。</p>
    </li><li>覆盖<p id="p31591925122820"><a name="p31591925122820"></a><a name="p31591925122820"></a>当同步数据与目标数据库已有数据冲突时（主键/唯一键存在重复等），将覆盖原来的冲突数据。</p>
    </li></ul>
    <p id="p3733215113711"><a name="p3733215113711"></a><a name="p3733215113711"></a>当数据发生冲突时，针对如下情况，建议选择“忽略”或者<span class="uicontrol" id="uicontrol15409187193316"><a name="uicontrol15409187193316"></a><a name="uicontrol15409187193316"></a>“覆盖”</span>，否则建议选择“报错”：</p>
    <a name="ul366812291748"></a><a name="ul366812291748"></a><ul id="ul366812291748"><li>目标数据库存在数据</li><li>多对一同步场景</li><li>目标数据库手动更新数据</li></ul>
    </td>
    </tr>
    <tr id="row5167176122819"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p1516710616289"><a name="p1516710616289"></a><a name="p1516710616289"></a>对象同步范围</p>
    </td>
    <td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p16167465286"><a name="p16167465286"></a><a name="p16167465286"></a>对象同步范围支持增量DDL同步。您可以根据业务需求选择是否进行同步。</p>
    </td>
    </tr>
    <tr id="row61671260283"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p81681265288"><a name="p81681265288"></a><a name="p81681265288"></a>快照模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p5813253132916"><a name="p5813253132916"></a><a name="p5813253132916"></a>如果您选择的是全量迁移模式的任务，数据复制服务支持设置快照模式。</p>
    <a name="ul178135537296"></a><a name="ul178135537296"></a><ul id="ul178135537296"><li>非快照式<p id="p981319534293"><a name="p981319534293"></a><a name="p981319534293"></a>适用于停止业务数据写入的导出，如果全量迁移中仍然有业务数据的修改，则导出数据为时间点非水平一致。稳定性和性能要优于快照式全量迁移。</p>
    </li><li>快照式<p id="p178131053162912"><a name="p178131053162912"></a><a name="p178131053162912"></a>可以在业务运行时产生一份时间水平一致的快照数据，具有业务数据分析价值，过程中的数据变化不会体现在导出数据中。</p>
    <div class="note" id="note18810222163016"><a name="note18810222163016"></a><a name="note18810222163016"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p188111822163017"><a name="p188111822163017"></a><a name="p188111822163017"></a>全量阶段使用快照模式导出能够有效提升全量+增量场景下的数据同步效率，但PostgreSQL的快照机制会使导出期间数据库的历史数据不能被回收，可能有空间膨胀的现象。建议在全量或增量数据量大且源库磁盘空间充足的情况下使用该方式。</p>
    </div></div>
    </li></ul>
    </td>
    </tr>
    <tr id="row559273214193"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p14592132171916"><a name="p14592132171916"></a><a name="p14592132171916"></a>同步对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p85921932191910"><a name="p85921932191910"></a><a name="p85921932191910"></a>同步对象支持表级同步和库级同步，您可以根据业务场景选择对应的数据进行同步。</p>
    <a name="ul992418431121"></a><a name="ul992418431121"></a><ul id="ul992418431121"><li>选择对象的时候支持搜索，以便您快速选择需要的数据库对象。</li><li>在同步对象右侧已选对象框中，可以使用对象名映射功能进行源数据库和目标数据库中的同步对象映射，具体操作可参考<a href="对象名映射.md">对象名映射</a>。</li></ul>
    </td>
    </tr>
    <tr id="row1133774212269"><td class="cellrowborder" valign="top" width="20%" headers="mcps1.2.3.1.1 "><p id="p633815423261"><a name="p633815423261"></a><a name="p633815423261"></a>同步用户</p>
    </td>
    <td class="cellrowborder" valign="top" width="80%" headers="mcps1.2.3.1.2 "><p id="p44831019115516"><a name="p44831019115516"></a><a name="p44831019115516"></a>数据库的同步过程中，同步用户需要进行单独处理。</p>
    <p id="p144836195551"><a name="p144836195551"></a><a name="p144836195551"></a>同步用户一般分为两类：可同步的用户和不支持同步的用户。对于不支持同步的用户，在备注列的查看详情中会提示具体的原因，您可以根据业务需求选择是否同步用户和权限。</p>
    </td>
    </tr>
    </tbody>
    </table>

5.  在“预检查“页面，进行同步任务预校验，校验是否可进行实时同步。
    -   查看检查结果，如有不通过的检查项，需要修复不通过项后，单击“重新校验”按钮重新进行任务预校验。

        预检查不通过项处理建议请参见《数据复制服务用户指南》中的“[预检查不通过项修复方法](https://support.huaweicloud.com/usermanual-drs/drs_precheck.html)”。

    -   预检查完成后，且所有检查项结果均通过时，单击“下一步“。

        **图 7**  PostgreSQL预检查<a name="zh-cn_topic_0141892586_fig23361684715"></a>  
        ![](figures/PostgreSQL预检查.png "PostgreSQL预检查")

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >所有检查项结果均通过时，若存在请确认项，需要阅读并确认详情后才可以继续执行下一步操作。


6.  在“任务确认“页面，设置同步任务的启动时间，并确认同步任务信息无误后，勾选协议，单击“启动任务“，提交同步任务。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   同步任务的启动时间可以根据业务需求，设置为“立即启动”或“稍后启动”。
    >-   预计同步任务启动后，会对源数据库和目标数据库的性能产生影响，建议选择业务低峰期，合理设置同步任务的启动时间。

7.  同步任务提交后，您可在“实时同步管理“页面，查看并管理自己的任务。
    -   您可查看任务提交后的状态，状态请参见[任务状态](https://support.huaweicloud.com/qs-drs/drs_06_0004.html)。
    -   在任务列表的右上角，单击![](figures/icon-刷新.png)刷新列表，可查看到最新的任务状态。



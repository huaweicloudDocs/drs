# GaussDB\(for openGauss\)主备版到Kafka同步实例<a name="drs_11_0445"></a>

本小节以GaussDB\(for openGauss\)主备版-\>Kafka的实时同步为示例，介绍如何使用数据复制服务配置实时同步任务。

## 前提条件<a name="zh-cn_topic_0288918853_section2097363117427"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   参见[实时同步](https://support.huaweicloud.com/productdesc-drs/drs_01_0302.html)。
-   参见[使用须知](https://support.huaweicloud.com/qs-drs/drs_06_0003.html)。

## 操作步骤<a name="section10151145510588"></a>

1.  在“实时同步管理”页面，单击“创建同步任务”。
2.  在“同步实例”页面，填选区域、任务名称、任务异常通知信息、SMN主题、时延阈值、任务异常自动结束时间、描述、同步实例信息，单击“下一步”。。

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

    **图 2**  GaussDB\(for openGauss\)主备版到Kafka同步实例信息<a name="zh-cn_topic_0288918853_fig123764616489"></a>  
    ![](figures/GaussDB(for-openGauss)主备版到Kafka同步实例信息.png "GaussDB(for-openGauss)主备版到Kafka同步实例信息")

    **表 2**  同步实例信息

    <a name="table1570115321414"></a>
    <table><thead align="left"><tr id="row1070212324120"><th class="cellrowborder" valign="top" width="23.87%" id="mcps1.2.3.1.1"><p id="p170220321515"><a name="p170220321515"></a><a name="p170220321515"></a><strong id="b147021332818"><a name="b147021332818"></a><a name="b147021332818"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.13%" id="mcps1.2.3.1.2"><p id="p20702103219114"><a name="p20702103219114"></a><a name="p20702103219114"></a><strong id="b9702232915"><a name="b9702232915"></a><a name="b9702232915"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row570213324110"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p157023328114"><a name="p157023328114"></a><a name="p157023328114"></a>数据流动场景</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p107021326115"><a name="p107021326115"></a><a name="p107021326115"></a>选择<span class="uicontrol" id="uicontrol147021632313"><a name="uicontrol147021632313"></a><a name="uicontrol147021632313"></a>“出云”</span>。</p>
    </td>
    </tr>
    <tr id="row87023321215"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p270283215118"><a name="p270283215118"></a><a name="p270283215118"></a>源数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p207027328115"><a name="p207027328115"></a><a name="p207027328115"></a>选择“<span id="text3902200193412"><a name="text3902200193412"></a><a name="text3902200193412"></a>GaussDB(for openGauss)</span>主备版”。</p>
    </td>
    </tr>
    <tr id="row1770216321015"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p8702123215111"><a name="p8702123215111"></a><a name="p8702123215111"></a>目标数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p77038327113"><a name="p77038327113"></a><a name="p77038327113"></a>选择“Kafka”。</p>
    </td>
    </tr>
    <tr id="row11703032218"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p8703183216113"><a name="p8703183216113"></a><a name="p8703183216113"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p470313324119"><a name="p470313324119"></a><a name="p470313324119"></a>此处以公网网络为示例。目前支持可选公网网络和VPN、专线网络。</p>
    </td>
    </tr>
    <tr id="row170313321315"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1870311321617"><a name="p1870311321617"></a><a name="p1870311321617"></a>源数据库实例</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p870311321319"><a name="p870311321319"></a><a name="p870311321319"></a>用户所创建的<span id="text4670112418713"><a name="text4670112418713"></a><a name="text4670112418713"></a>GaussDB(for openGauss)</span>主备版实例。</p>
    </td>
    </tr>
    <tr id="row17032032315"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1170333212111"><a name="p1170333212111"></a><a name="p1170333212111"></a>同步实例所在子网</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p177031232718"><a name="p177031232718"></a><a name="p177031232718"></a>请选择同步实例所在的子网。也可以单击“查看子网”，跳转至“网络控制台”查看实例所在子网帮助选择。</p>
    <p id="p127036328112"><a name="p127036328112"></a><a name="p127036328112"></a>默认值为当前所选数据库实例所在子网，请选择有可用IP地址的子网。为确保同步实例创建成功，仅显示已经开启DHCP的子网。</p>
    </td>
    </tr>
    <tr id="row107031432511"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1670303211110"><a name="p1670303211110"></a><a name="p1670303211110"></a>同步类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p27032329115"><a name="p27032329115"></a><a name="p27032329115"></a>增量。</p>
    </td>
    </tr>
    <tr id="row12345165417514"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1017716536718"><a name="p1017716536718"></a><a name="p1017716536718"></a>企业项目</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p795282881017"><a name="p795282881017"></a><a name="p795282881017"></a>对于已成功关联企业项目的用户，仅需在“企业项目”下拉框中选择目标项目。</p>
    <p id="p8952152819109"><a name="p8952152819109"></a><a name="p8952152819109"></a>如果需要自定义企业项目，请前往项目管理服务进行创建。关于如何创建项目，详见《项目管理用户指南》。</p>
    </td>
    </tr>
    <tr id="row434625435118"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1276314133599"><a name="p1276314133599"></a><a name="p1276314133599"></a>标签</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p16021376352"><a name="p16021376352"></a><a name="p16021376352"></a>可选配置，对同步任务的标识。使用标签可方便管理您的<span id="drs_06_0005_text947798304"><a name="drs_06_0005_text947798304"></a><a name="drs_06_0005_text947798304"></a>实时同步</span>任务。每个任务最多支持10个标签配额。</p>
    <p id="p8307101212113"><a name="p8307101212113"></a><a name="p8307101212113"></a>任务创建成功后，您可以单击实例名称，在<span class="uicontrol" id="zh-cn_topic_0078078071_uicontrol1433412554316"><a name="zh-cn_topic_0078078071_uicontrol1433412554316"></a><a name="zh-cn_topic_0078078071_uicontrol1433412554316"></a>“标签”</span>页签下查看对应标签。关于标签的详细操作，请参见<a href="https://support.huaweicloud.com/usermanual-drs/drs_synchronization_tag.html" target="_blank" rel="noopener noreferrer">标签管理</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，待同步实例创建成功后，填选源库信息和目标库信息，单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，单击“下一步“。

    **图 3**  GaussDB\(for openGauss\)主备版源库信息<a name="zh-cn_topic_0288918853_fig20498162055215"></a>  
    ![](figures/GaussDB(for-openGauss)主备版源库信息.png "GaussDB(for-openGauss)主备版源库信息")

    **表 3**  源库信息

    <a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_table1665310232597"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_row12653123195919"><th class="cellrowborder" valign="top" width="23.27%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p156531623165916"><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p156531623165916"></a><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p156531623165916"></a><strong id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_b20653923155913"><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_b20653923155913"></a><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_b20653923155913"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.73%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p1365312365910"><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p1365312365910"></a><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_p1365312365910"></a><strong id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_b186531223105910"><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_b186531223105910"></a><a name="zh-cn_topic_0288918853_zh-cn_topic_0135097933_b186531223105910"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_row1265352355912"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="p17989341131512"><a name="p17989341131512"></a><a name="p17989341131512"></a>数据库实例名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="p1798918413155"><a name="p1798918413155"></a><a name="p1798918413155"></a>默认为创建同步任务时选择的关系型数据库实例，不可进行修改。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0288918853_zh-cn_topic_0135097933_row765313235597"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="p169901341181514"><a name="p169901341181514"></a><a name="p169901341181514"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p665318234591"><a name="zh-cn_topic_0135097933_p665318234591"></a><a name="zh-cn_topic_0135097933_p665318234591"></a>源数据库的用户名。</p>
    </td>
    </tr>
    <tr id="row119010914238"><td class="cellrowborder" valign="top" width="23.27%" headers="mcps1.2.3.1.1 "><p id="p11990184141512"><a name="p11990184141512"></a><a name="p11990184141512"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.73%" headers="mcps1.2.3.1.2 "><p id="p127064313117"><a name="p127064313117"></a><a name="p127064313117"></a>源数据库的用户名所对应的密码。</p>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >**源数据库的数据库用户名和密码，会被系统加密暂存，直至删除该迁移任务后自动清除。**

    **图 4**  Kafka目标库信息<a name="fig158911712244"></a>  
    ![](figures/Kafka目标库信息.png "Kafka目标库信息")

    **表 4**  目标库信息

    <a name="table614313221229"></a>
    <table><thead align="left"><tr id="row12143192211228"><th class="cellrowborder" valign="top" width="23%" id="mcps1.2.3.1.1"><p id="p1814313225224"><a name="p1814313225224"></a><a name="p1814313225224"></a><strong id="b131431722162219"><a name="b131431722162219"></a><a name="b131431722162219"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="77%" id="mcps1.2.3.1.2"><p id="p11143142232220"><a name="p11143142232220"></a><a name="p11143142232220"></a><strong id="b31431922182216"><a name="b31431922182216"></a><a name="b31431922182216"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row9621838142215"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p15621143818226"><a name="p15621143818226"></a><a name="p15621143818226"></a>IP地址或域名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p196211338182217"><a name="p196211338182217"></a><a name="p196211338182217"></a>目标数据库的IP地址或域名，格式为IP地址/域名:端口。其中目标数据库服务端口，可输入范围为1~65534间的整数。</p>
    <p id="zh-cn_topic_0135097933_p2653523145918"><a name="zh-cn_topic_0135097933_p2653523145918"></a><a name="zh-cn_topic_0135097933_p2653523145918"></a>该输入框最多支持填写10组目标数据库的IP地址或者域名信息，多个值需要使用英文逗号隔开。例如：192.168.0.1:8080,192.168.0.2:8080。</p>
    </td>
    </tr>
    </tbody>
    </table>

4.  在“设置同步“页面，选择同步策略、数据格式和同步对象，单击“下一步“。

    **图 5**  GaussDB\(for openGauss\)主备版到Kafka同步模式<a name="fig14025637142814"></a>  
    ![](figures/GaussDB(for-openGauss)主备版到Kafka同步模式.png "GaussDB(for-openGauss)主备版到Kafka同步模式")

    **表 5**  同步对象

    <a name="table1150196185416"></a>
    <table><thead align="left"><tr id="row35015619542"><th class="cellrowborder" valign="top" width="16%" id="mcps1.2.3.1.1"><p id="p65012612549"><a name="p65012612549"></a><a name="p65012612549"></a><strong id="b35017675412"><a name="b35017675412"></a><a name="b35017675412"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="84%" id="mcps1.2.3.1.2"><p id="p95021264540"><a name="p95021264540"></a><a name="p95021264540"></a><strong id="b1750217665412"><a name="b1750217665412"></a><a name="b1750217665412"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row61064915127"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p1107109131214"><a name="p1107109131214"></a><a name="p1107109131214"></a>同步Topic策略</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p02621419181419"><a name="p02621419181419"></a><a name="p02621419181419"></a>同步Topic策略，可选择集中投递到一个Topic或者按照格式自动生成Topic名字。</p>
    </td>
    </tr>
    <tr id="row61271125113917"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p71288255399"><a name="p71288255399"></a><a name="p71288255399"></a>Topic</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p71281325133915"><a name="p71281325133915"></a><a name="p71281325133915"></a>选择目标端需要同步到的Topic，同步Topic策略选择集中投递到一个Topic时可见。</p>
    </td>
    </tr>
    <tr id="row14912505165"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p11961454181616"><a name="p11961454181616"></a><a name="p11961454181616"></a>Topic名字格式</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p10968540163"><a name="p10968540163"></a><a name="p10968540163"></a>同步Topic策略选择自动生成Topic名字时可见。</p>
    </td>
    </tr>
    <tr id="row18351020113612"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p1351122017367"><a name="p1351122017367"></a><a name="p1351122017367"></a>Partition个数</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p932820168314"><a name="p932820168314"></a><a name="p932820168314"></a>同步Topic策略选择自动生成Topic名字时可见。</p>
    <p id="p16758938232"><a name="p16758938232"></a><a name="p16758938232"></a>用来设置topic的分区个数。每个topic都可以创建多个partition，越多的partition可以提供更高的吞吐量，越多的partition会消耗更多的资源，建议根据broker节点的实际情况来设置partition的数量。</p>
    </td>
    </tr>
    <tr id="row17197432174310"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p171981332104311"><a name="p171981332104311"></a><a name="p171981332104311"></a>副本个数</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p197080191036"><a name="p197080191036"></a><a name="p197080191036"></a>同步Topic策略选择自动生成Topic名字时可见。</p>
    <p id="p929020559318"><a name="p929020559318"></a><a name="p929020559318"></a>用来设置topic的副本数。每个topic可以有多个副本，副本位于集群中不同的broker上，副本的数量不能超过broker的数量，否则创建topic时会失败。</p>
    </td>
    </tr>
    <tr id="row1928214584213"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p27972052035"><a name="p27972052035"></a><a name="p27972052035"></a>同步到kafka partition策略</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p1797951630"><a name="p1797951630"></a><a name="p1797951630"></a>同步到kafka partition策略。</p>
    <a name="ul979710518319"></a><a name="ul979710518319"></a><ul id="ul979710518319"><li>按不同的hash值投递到不同Partition：适用于单表的查询场景，表内保序，表与表之间不保序，可以提高单表读写性能，推荐使用此选项。</li><li>全部投递到Partition 0：适用于有事务要求的场景，事务保序，可以保证完全按照事务顺序消费，写入性能比较差，如果没有强事务要求，不推荐使用此选项。</li></ul>
    </td>
    </tr>
    <tr id="row15033619540"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p13503126105416"><a name="p13503126105416"></a><a name="p13503126105416"></a>同步对象</p>
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

        **图 6**  GaussDB\(for openGauss\)分布式版到GaussDB\(DWS\)预检查<a name="drs_11_0443_zh-cn_topic_0221102801_fig3658849112911"></a>  
        ![](figures/GaussDB(for-openGauss)分布式版到GaussDB(DWS)预检查.png "GaussDB(for-openGauss)分布式版到GaussDB(DWS)预检查")

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >所有检查项结果均通过时，若存在请确认项，需要阅读并确认详情后才可以继续执行下一步操作。


6.  在“任务确认“页面，设置同步任务的启动时间，并确认同步任务信息无误后，勾选协议，单击“启动任务“，提交同步任务。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   同步任务的启动时间可以根据业务需求，设置为“立即启动”或“稍后启动”。
    >-   预计同步任务启动后，会对源数据库和目标数据库的性能产生影响，建议选择业务低峰期，合理设置同步任务的启动时间。



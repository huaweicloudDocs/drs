# MySQL自建到Kafka同步实例<a name="drs_03_1122"></a>

本小节以MySQL自建-\>Kafka自建的实时同步为示例，介绍如何使用数据复制服务配置实时同步任务。

## 前提条件<a name="section2097363117427"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   参见[实时同步](https://support.huaweicloud.com/productdesc-drs/drs_01_0302.html)。
-   参见[使用须知](https://support.huaweicloud.com/qs-drs/drs_06_0003.html)。

## 操作步骤<a name="section15351446124811"></a>

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

    **图 2**  MySQL自建到Kafka同步实例信息<a name="fig123764616489"></a>  
    ![](figures/MySQL自建到Kafka同步实例信息.png "MySQL自建到Kafka同步实例信息")

    **表 2**  同步实例信息

    <a name="table7640047195011"></a>
    <table><thead align="left"><tr id="row166411047105013"><th class="cellrowborder" valign="top" width="23.87%" id="mcps1.2.3.1.1"><p id="p14641147165017"><a name="p14641147165017"></a><a name="p14641147165017"></a><strong id="b66411847105019"><a name="b66411847105019"></a><a name="b66411847105019"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.13%" id="mcps1.2.3.1.2"><p id="p10641184717508"><a name="p10641184717508"></a><a name="p10641184717508"></a><strong id="b15641114765014"><a name="b15641114765014"></a><a name="b15641114765014"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row2064114711508"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p20641124712505"><a name="p20641124712505"></a><a name="p20641124712505"></a>数据流动方向</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1364154785018"><a name="p1364154785018"></a><a name="p1364154785018"></a>选择<span class="uicontrol" id="uicontrol12641124712500"><a name="uicontrol12641124712500"></a><a name="uicontrol12641124712500"></a>“自建-自建”</span>。</p>
    </td>
    </tr>
    <tr id="row1964144712506"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p19641144755017"><a name="p19641144755017"></a><a name="p19641144755017"></a>源数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p196411447125011"><a name="p196411447125011"></a><a name="p196411447125011"></a>选择<span class="uicontrol" id="uicontrol1064134745012"><a name="uicontrol1064134745012"></a><a name="uicontrol1064134745012"></a>“MySQL”</span>。</p>
    </td>
    </tr>
    <tr id="row164274755010"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p5642184715018"><a name="p5642184715018"></a><a name="p5642184715018"></a>目标数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1664244745010"><a name="p1664244745010"></a><a name="p1664244745010"></a>选择<span class="uicontrol" id="uicontrol182111736174115"><a name="uicontrol182111736174115"></a><a name="uicontrol182111736174115"></a>“Kafka”</span>。</p>
    </td>
    </tr>
    <tr id="row864212474509"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p164254713502"><a name="p164254713502"></a><a name="p164254713502"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p20642047155016"><a name="p20642047155016"></a><a name="p20642047155016"></a>此处以<span class="uicontrol" id="uicontrol1364219478509"><a name="uicontrol1364219478509"></a><a name="uicontrol1364219478509"></a>“公网网络”</span>为示例。目前支持可选公网网络、VPC网络和VPN、专线网络。</p>
    </td>
    </tr>
    <tr id="row20591449462"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p65921748463"><a name="p65921748463"></a><a name="p65921748463"></a>可用区</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p55924474615"><a name="p55924474615"></a><a name="p55924474615"></a>选择DRS实例创建在哪个可用区，选择跟源或目标库相同的可用区性能更优。</p>
    </td>
    </tr>
    <tr id="row5642247155010"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p16642184712508"><a name="p16642184712508"></a><a name="p16642184712508"></a>VPC</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1664215475504"><a name="p1664215475504"></a><a name="p1664215475504"></a>选择可用的虚拟私有云。</p>
    </td>
    </tr>
    <tr id="row15177111612817"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1564294795014"><a name="p1564294795014"></a><a name="p1564294795014"></a>同步实例所在子网</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p764264711503"><a name="p764264711503"></a><a name="p764264711503"></a>请选择同步实例所在的子网。也可以单击“查看子网”，跳转至“网络控制台”查看实例所在子网帮助选择。</p>
    <p id="p186421947145018"><a name="p186421947145018"></a><a name="p186421947145018"></a>默认值为当前所选数据库实例所在子网，请选择有可用IP地址的子网。为确保同步实例创建成功，仅显示已经开启DHCP的子网。</p>
    </td>
    </tr>
    <tr id="row12368181619"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1647891610"><a name="p1647891610"></a><a name="p1647891610"></a>内网安全组</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p441883169"><a name="p441883169"></a><a name="p441883169"></a>请选择内网安全组。内网安全组限制实例的安全访问规则，加强安全访问。</p>
    </td>
    </tr>
    <tr id="row186434470500"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p136435476503"><a name="p136435476503"></a><a name="p136435476503"></a>同步类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p5284175155320"><a name="p5284175155320"></a><a name="p5284175155320"></a><span class="uicontrol" id="uicontrol79554417126"><a name="uicontrol79554417126"></a><a name="uicontrol79554417126"></a>“增量”</span>。</p>
    </td>
    </tr>
    <tr id="row1112613477361"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1364364719508"><a name="p1364364719508"></a><a name="p1364364719508"></a>企业项目</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p7643184720500"><a name="p7643184720500"></a><a name="p7643184720500"></a>对于已成功关联企业项目的用户，仅需在“企业项目”下拉框中选择目标项目。</p>
    <p id="p5644194765019"><a name="p5644194765019"></a><a name="p5644194765019"></a>如果需要自定义企业项目，请前往项目管理服务进行创建。关于如何创建项目，详见《项目管理用户指南》。</p>
    </td>
    </tr>
    <tr id="row11681455143620"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p206442047125010"><a name="p206442047125010"></a><a name="p206442047125010"></a>标签</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p27631913145915"><a name="p27631913145915"></a><a name="p27631913145915"></a>可选配置，对同步任务的标识。使用标签可方便管理您的<span id="drs_06_0005_text947798304"><a name="drs_06_0005_text947798304"></a><a name="drs_06_0005_text947798304"></a>实时同步</span>任务。每个任务最多支持10个标签配额。</p>
    <p id="p2064444715507"><a name="p2064444715507"></a><a name="p2064444715507"></a>任务创建成功后，您可以单击实例名称，在<span class="uicontrol" id="uicontrol13644847185019"><a name="uicontrol13644847185019"></a><a name="uicontrol13644847185019"></a>“标签”</span>页签下查看对应标签。关于标签的详细操作，请参见<a href="https://support.huaweicloud.com/usermanual-drs/drs_synchronization_tag.html" target="_blank" rel="noopener noreferrer">标签管理</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，同步实例创建成功后，填选源库信息和目标库信息，建议您单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，勾选协议，单击“下一步“。

    **图 3**  自建MySQL源库信息<a name="fig169581658195520"></a>  
    ![](figures/自建MySQL源库信息.png "自建MySQL源库信息")

    **表 3**  源库信息

    <a name="table5457114616020"></a>
    <table><thead align="left"><tr id="row64572461706"><th class="cellrowborder" valign="top" width="23.29%" id="mcps1.2.3.1.1"><p id="p1245711467016"><a name="p1245711467016"></a><a name="p1245711467016"></a><strong id="b154574464019"><a name="b154574464019"></a><a name="b154574464019"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.71%" id="mcps1.2.3.1.2"><p id="p945754617013"><a name="p945754617013"></a><a name="p945754617013"></a><strong id="b2045744616014"><a name="b2045744616014"></a><a name="b2045744616014"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row194573467019"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p16457134611018"><a name="p16457134611018"></a><a name="p16457134611018"></a>IP地址或域名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p1745714461609"><a name="p1745714461609"></a><a name="p1745714461609"></a>源数据库的IP地址或域名。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row765313235597"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p8653172395914"><a name="zh-cn_topic_0135097933_p8653172395914"></a><a name="zh-cn_topic_0135097933_p8653172395914"></a>端口</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p15653192315910"><a name="zh-cn_topic_0135097933_p15653192315910"></a><a name="zh-cn_topic_0135097933_p15653192315910"></a>源数据库服务端口，可输入范围为1~65535间的整数。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row9653102325913"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p379718114"><a name="p379718114"></a><a name="p379718114"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p17971681118"><a name="p17971681118"></a><a name="p17971681118"></a>源数据库的用户名。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row065352315596"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p187971581712"><a name="p187971581712"></a><a name="p187971581712"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p18797208618"><a name="p18797208618"></a><a name="p18797208618"></a>源数据库的用户名所对应的密码。</p>
    </td>
    </tr>
    <tr id="zh-cn_topic_0135097933_row26531923125912"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p2653112395910"><a name="zh-cn_topic_0135097933_p2653112395910"></a><a name="zh-cn_topic_0135097933_p2653112395910"></a>SSL安全连接</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p765310236599"><a name="zh-cn_topic_0135097933_p765310236599"></a><a name="zh-cn_topic_0135097933_p765310236599"></a>通过该功能，用户可以选择是否开启对迁移链路的加密。如果开启该功能，需要用户上传SSL CA根证书。</p>
    <div class="note" id="note174414299197"><a name="note174414299197"></a><a name="note174414299197"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul89474461410"></a><a name="ul89474461410"></a><ul id="ul89474461410"><li>最大支持上传500KB的证书文件。</li><li>如果不使用SSL证书，请自行承担数据安全风险。</li></ul>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >**源数据库的数据库用户名和密码，会被系统加密暂存，直至删除该迁移任务后自动清除。**

    **图 4**  Kafka目标库信息<a name="fig158911712244"></a>  
    ![](figures/Kafka目标库信息.png "Kafka目标库信息")

    **表 4**  源库信息

    <a name="zh-cn_topic_0135097933_table1665310232597"></a>
    <table><thead align="left"><tr id="zh-cn_topic_0135097933_row12653123195919"><th class="cellrowborder" valign="top" width="23.29%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0135097933_p156531623165916"><a name="zh-cn_topic_0135097933_p156531623165916"></a><a name="zh-cn_topic_0135097933_p156531623165916"></a><strong id="zh-cn_topic_0135097933_b20653923155913"><a name="zh-cn_topic_0135097933_b20653923155913"></a><a name="zh-cn_topic_0135097933_b20653923155913"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.71%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0135097933_p1365312365910"><a name="zh-cn_topic_0135097933_p1365312365910"></a><a name="zh-cn_topic_0135097933_p1365312365910"></a><strong id="zh-cn_topic_0135097933_b186531223105910"><a name="zh-cn_topic_0135097933_b186531223105910"></a><a name="zh-cn_topic_0135097933_b186531223105910"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="zh-cn_topic_0135097933_row1265352355912"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0135097933_p665313232598"><a name="zh-cn_topic_0135097933_p665313232598"></a><a name="zh-cn_topic_0135097933_p665313232598"></a>IP地址或域名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0135097933_p2653523145918"><a name="zh-cn_topic_0135097933_p2653523145918"></a><a name="zh-cn_topic_0135097933_p2653523145918"></a>目标数据库的IP地址或域名。</p>
    </td>
    </tr>
    </tbody>
    </table>

4.  在“设置同步“页面，选择同步策略、数据格式和同步对象，单击“下一步“。

    **图 5**  MySQL自建到Kafka同步模式<a name="fig14025637142814"></a>  
    ![](figures/MySQL自建到Kafka同步模式.png "MySQL自建到Kafka同步模式")

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
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p02621419181419"><a name="p02621419181419"></a><a name="p02621419181419"></a>同步Topic策略，可选择</p>
    <a name="ul2665115121316"></a><a name="ul2665115121316"></a><ul id="ul2665115121316"><li>集中投递到一个Topic：适合源库业务量不大的场景。</li><li>自动生成Topic名字：适合每张表数据量都较大的场景，按每一张库表来确定一个Topic。</li></ul>
    </td>
    </tr>
    <tr id="row61271125113917"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p71288255399"><a name="p71288255399"></a><a name="p71288255399"></a>Topic</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p71281325133915"><a name="p71281325133915"></a><a name="p71281325133915"></a>选择目标端需要同步到的Topic，同步Topic策略选择集中投递到一个Topic时可见。</p>
    </td>
    </tr>
    <tr id="row14912505165"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p11961454181616"><a name="p11961454181616"></a><a name="p11961454181616"></a>Topic名字格式</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p10968540163"><a name="p10968540163"></a><a name="p10968540163"></a>Topic名字格式，同步Topic策略选择自动生成Topic名字时可见。</p>
    <p id="p15920547113214"><a name="p15920547113214"></a><a name="p15920547113214"></a>Topic名字格式支持database和tablename两个变量，其他字符都当做常量。分别用$database$代替数据库名，$tablename$代替表名。</p>
    <p id="p11921124716323"><a name="p11921124716323"></a><a name="p11921124716323"></a>例如：配置成$database$-$tablename$时，如果数据库名称为db1，表名为tab1，则Topic名字为db1-tab1。如果是DDL语句，$tablename$为空，则Topic名字为db1.</p>
    </td>
    </tr>
    <tr id="row16571125965410"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p05721159205410"><a name="p05721159205410"></a><a name="p05721159205410"></a>同步到kafka partition策略</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p5191113710569"><a name="p5191113710569"></a><a name="p5191113710569"></a>同步到kafka partition策略。</p>
    <a name="ul1175313402567"></a><a name="ul1175313402567"></a><ul id="ul1175313402567"><li>按库名+表名的hash值投递到不同Partition：适用于单表的查询场景，可以提高单表读写性能，推荐使用此选项。</li><li>全部投递到Partition 0：适用于有事务要求的场景，写入性能比较差，如果没有强事务要求，不推荐使用此选项。</li><li>按表的主键值hash值投递到不同的Partion：适用于一个表一个Topic的场景，避免该表都写到同一个分区，消费者可以并行从各分区获取数据。</li></ul>
    </td>
    </tr>
    <tr id="row18351020113612"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p1351122017367"><a name="p1351122017367"></a><a name="p1351122017367"></a>投送到kafka的数据格式</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p114861232381"><a name="p114861232381"></a><a name="p114861232381"></a>选择MySQL投送到kafka的数据格式。</p>
    <a name="ul574420499552"></a><a name="ul574420499552"></a><ul id="ul574420499552"><li>Avro：可以显示Avro二进制编码，高效获取数据。</li><li>JSON：为Json消息格式，方便解释格式，但需要占用更多的空间。</li><li>JSON-C：一种能够兼容多个批量，流式计算框架的数据格式。</li></ul>
    <p id="p97597118202"><a name="p97597118202"></a><a name="p97597118202"></a>详细格式可参考<a href="Kafka消息格式.md">Kafka消息格式</a>。</p>
    </td>
    </tr>
    <tr id="row559273214193"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p14592132171916"><a name="p14592132171916"></a><a name="p14592132171916"></a>同步对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p85921932191910"><a name="p85921932191910"></a><a name="p85921932191910"></a>同步对象支持表级同步和库级同步，您可以根据业务场景选择对应的数据进行同步。</p>
    <a name="ul13693174744610"></a><a name="ul13693174744610"></a><ul id="ul13693174744610"><li>选择对象的时候支持搜索，以便您快速选择需要的数据库对象。</li><li>在同步对象右侧已选对象框中，可以使用对象名映射功能进行源数据库和目标数据库中的同步对象映射，具体操作可参考<a href="对象名映射.md">对象名映射</a>。</li></ul>
    </td>
    </tr>
    </tbody>
    </table>

5.  在“数据加工”页面，选择需要加工的列，进行列加工。

    -   如果不需要数据加工，单击“下一步”。
    -   如果需要加工列，参考[数据加工](数据加工.md)章节，设置相关规则。

    **图 6**  MySQL自建到Kafka数据加工<a name="fig155445215364"></a>  
    ![](figures/MySQL自建到Kafka数据加工.png "MySQL自建到Kafka数据加工")

6.  在“预检查“页面，进行同步任务预校验，校验是否可进行实时同步。
    -   查看检查结果，如有不通过的检查项，需要修复不通过项后，单击“重新校验”按钮重新进行任务预校验。

        预检查不通过项处理建议请参见《数据复制服务用户指南》中的“[预检查不通过项修复方法](https://support.huaweicloud.com/usermanual-drs/drs_precheck.html)”。

    -   预检查完成后，且所有检查项结果均通过时，单击“下一步“。

        **图 7**  同步预检查<a name="drs_06_0005_fig23361684715"></a>  
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



# MySQL数据库到GaussDB\(for MySQL\)主备版同步实例<a name="drs_11_0448"></a>

本小节以MySQL-\>GaussDB\(for MySQL\)主备版的实时同步为示例，介绍如何使用数据复制服务配置实时同步任务。

## 前提条件<a name="section2097363117427"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   参见[实时同步](https://support.huaweicloud.com/productdesc-drs/drs_01_0302.html)。
-   参见[使用须知](https://support.huaweicloud.com/qs-drs/drs_06_0003.html)。

## 操作步骤<a name="section1043012137161"></a>

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

    **图 2**  MySQL到GaussDB\(for MySQL\)主备版同步实例信息<a name="fig123764616489"></a>  
    ![](figures/MySQL到GaussDB(for-MySQL)主备版同步实例信息.png "MySQL到GaussDB(for-MySQL)主备版同步实例信息")

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
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1969552512018"><a name="p1969552512018"></a><a name="p1969552512018"></a>选择<span class="uicontrol" id="uicontrol154014364188"><a name="uicontrol154014364188"></a><a name="uicontrol154014364188"></a>“<span id="text361503919504"><a name="text361503919504"></a><a name="text361503919504"></a>GaussDB(for MySQL)</span>主备版”</span>。</p>
    </td>
    </tr>
    <tr id="row62907306204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p62327044204436"><a name="p62327044204436"></a><a name="p62327044204436"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p87075558433"><a name="p87075558433"></a><a name="p87075558433"></a>此处以<span class="uicontrol" id="uicontrol12676440161816"><a name="uicontrol12676440161816"></a><a name="uicontrol12676440161816"></a>“公网网络”</span>为示例。目前支持可选公网网络、VPC网络和VPN、专线网络。</p>
    </td>
    </tr>
    <tr id="row658644204515"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p53350183204515"><a name="p53350183204515"></a><a name="p53350183204515"></a>目标数据库实例</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p26397538204515"><a name="p26397538204515"></a><a name="p26397538204515"></a>可用的<span class="uicontrol" id="uicontrol1285819434015"><a name="uicontrol1285819434015"></a><a name="uicontrol1285819434015"></a>“<span id="text17859043207"><a name="text17859043207"></a><a name="text17859043207"></a>GaussDB(for MySQL)</span>主备版”</span>实例。</p>
    </td>
    </tr>
    <tr id="row15177111612817"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p01021256155315"><a name="p01021256155315"></a><a name="p01021256155315"></a>同步实例所在子网</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p18102456175315"><a name="p18102456175315"></a><a name="p18102456175315"></a>请选择同步实例所在的子网。也可以单击“查看子网”，跳转至“网络控制台”查看实例所在子网帮助选择。</p>
    <p id="p47671146133910"><a name="p47671146133910"></a><a name="p47671146133910"></a>默认值为当前所选数据库实例所在子网，请选择有可用IP地址的子网。为确保同步实例创建成功，仅显示已经开启DHCP的子网。</p>
    </td>
    </tr>
    <tr id="row1169913195320"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p06786155538"><a name="p06786155538"></a><a name="p06786155538"></a>同步模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><a name="ul8912048626"></a><a name="ul8912048626"></a><ul id="ul8912048626"><li>全量+增量</li></ul>
    <p id="p9660115025713"><a name="p9660115025713"></a><a name="p9660115025713"></a>该模式为数据持续性实时同步，通过全量过程完成目标端数据库的初始化后，增量同步阶段通过解析日志等技术，将源端和目标端数据保持数据持续一致。</p>
    <a name="ul4660044728"></a><a name="ul4660044728"></a><ul id="ul4660044728"><li>增量。</li></ul>
    <p id="p0678161516531"><a name="p0678161516531"></a><a name="p0678161516531"></a>增量同步通过解析日志等技术，将源端产生的增量<span id="text1494429456"><a name="text1494429456"></a><a name="text1494429456"></a>实时同步</span>至目标端。</p>
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
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p19809151110331"><a name="p19809151110331"></a><a name="p19809151110331"></a>可选配置，对同步任务的标识。使用标签可方便管理您的<span id="drs_06_0005_text947798304"><a name="drs_06_0005_text947798304"></a><a name="drs_06_0005_text947798304"></a>实时同步</span>任务。每个任务最多支持10个标签配额。</p>
    <p id="p8307101212113"><a name="p8307101212113"></a><a name="p8307101212113"></a>任务创建成功后，您可以单击实例名称，在<span class="uicontrol" id="zh-cn_topic_0078078071_uicontrol1433412554316"><a name="zh-cn_topic_0078078071_uicontrol1433412554316"></a><a name="zh-cn_topic_0078078071_uicontrol1433412554316"></a>“标签”</span>页签下查看对应标签。关于标签的详细操作，请参见<a href="https://support.huaweicloud.com/usermanual-drs/drs_synchronization_tag.html" target="_blank" rel="noopener noreferrer">标签管理</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，同步实例创建成功后，填选源库信息和目标库信息，建议您单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，勾选协议，单击“下一步“。

    **图 3**  MySQL源库信息<a name="fig20498162055215"></a>  
    ![](figures/MySQL源库信息.png "MySQL源库信息")

    **表 3**  源库信息

    <a name="table2017905351814"></a>
    <table><thead align="left"><tr id="row16179125311813"><th class="cellrowborder" valign="top" width="23.29%" id="mcps1.2.3.1.1"><p id="p8179753181819"><a name="p8179753181819"></a><a name="p8179753181819"></a><strong id="b12179155391820"><a name="b12179155391820"></a><a name="b12179155391820"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.71%" id="mcps1.2.3.1.2"><p id="p151795537188"><a name="p151795537188"></a><a name="p151795537188"></a><strong id="b11179553141816"><a name="b11179553141816"></a><a name="b11179553141816"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row217913530187"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p161796535188"><a name="p161796535188"></a><a name="p161796535188"></a>IP地址或域名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p91791653121819"><a name="p91791653121819"></a><a name="p91791653121819"></a>源数据库的IP地址或域名。</p>
    </td>
    </tr>
    <tr id="row417985321817"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p15179195371814"><a name="p15179195371814"></a><a name="p15179195371814"></a>端口</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p10179553161820"><a name="p10179553161820"></a><a name="p10179553161820"></a>源数据库服务端口，可输入范围为1~65535间的整数。</p>
    </td>
    </tr>
    <tr id="row2179175351818"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p11180175361811"><a name="p11180175361811"></a><a name="p11180175361811"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p8180145314188"><a name="p8180145314188"></a><a name="p8180145314188"></a>源数据库的用户名。</p>
    </td>
    </tr>
    <tr id="row218095315186"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p41805534182"><a name="p41805534182"></a><a name="p41805534182"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p5180115316182"><a name="p5180115316182"></a><a name="p5180115316182"></a>源数据库的用户名所对应的密码。</p>
    </td>
    </tr>
    <tr id="row161801553161810"><td class="cellrowborder" valign="top" width="23.29%" headers="mcps1.2.3.1.1 "><p id="p118045361819"><a name="p118045361819"></a><a name="p118045361819"></a>SSL安全连接</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.71%" headers="mcps1.2.3.1.2 "><p id="p718095319187"><a name="p718095319187"></a><a name="p718095319187"></a>通过该功能，用户可以选择是否开启对迁移链路的加密。如果开启该功能，需要用户上传SSL CA根证书。</p>
    <div class="note" id="note1318016536186"><a name="note1318016536186"></a><a name="note1318016536186"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul131801653191816"></a><a name="ul131801653191816"></a><ul id="ul131801653191816"><li>最大支持上传500KB的证书文件。</li><li>如果不使用SSL证书，请自行承担数据安全风险。</li></ul>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >**源数据库的数据库用户名和密码，会被系统加密暂存，直至删除该迁移任务后自动清除。**

    **图 4**  GaussDB\(for MySQL\)主备版目标库信息<a name="fig13180125314180"></a>  
    ![](figures/GaussDB(for-MySQL)主备版目标库信息.png "GaussDB(for-MySQL)主备版目标库信息")

    **表 4**  目标库信息

    <a name="table71811153141814"></a>
    <table><thead align="left"><tr id="row17181653181815"><th class="cellrowborder" valign="top" width="23%" id="mcps1.2.3.1.1"><p id="p16181185331814"><a name="p16181185331814"></a><a name="p16181185331814"></a><strong id="b118115538180"><a name="b118115538180"></a><a name="b118115538180"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="77%" id="mcps1.2.3.1.2"><p id="p13181115301817"><a name="p13181115301817"></a><a name="p13181115301817"></a><strong id="b1918145310187"><a name="b1918145310187"></a><a name="b1918145310187"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row4181453161819"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p318195361819"><a name="p318195361819"></a><a name="p318195361819"></a>数据库实例名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p121813530188"><a name="p121813530188"></a><a name="p121813530188"></a>默认为创建同步任务时选择的关系型数据库实例，不可进行修改。</p>
    </td>
    </tr>
    <tr id="row618118532187"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p12181553121810"><a name="p12181553121810"></a><a name="p12181553121810"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p1118245371816"><a name="p1118245371816"></a><a name="p1118245371816"></a>目标数据库对应的数据库用户名。</p>
    </td>
    </tr>
    <tr id="row7182553111815"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p1818225391818"><a name="p1818225391818"></a><a name="p1818225391818"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p111821053111818"><a name="p111821053111818"></a><a name="p111821053111818"></a>数据库用户名和密码将被系统加密暂存，直至该任务删除后清除。</p>
    </td>
    </tr>
    </tbody>
    </table>

4.  在“设置同步“页面，选择同步对象类型和同步对象，单击“下一步“。

    **图 5**  MySQL到GaussDB\(for MySQL\)主备版同步模式<a name="fig32941637141913"></a>  
    ![](figures/MySQL到GaussDB(for-MySQL)主备版同步模式.png "MySQL到GaussDB(for-MySQL)主备版同步模式")

    **表 5**  同步模式和对象

    <a name="table112941737141919"></a>
    <table><thead align="left"><tr id="row2297183711193"><th class="cellrowborder" valign="top" width="20.599999999999998%" id="mcps1.2.3.1.1"><p id="p13297173717190"><a name="p13297173717190"></a><a name="p13297173717190"></a><strong id="b6297103751911"><a name="b6297103751911"></a><a name="b6297103751911"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="79.4%" id="mcps1.2.3.1.2"><p id="p1429715377197"><a name="p1429715377197"></a><a name="p1429715377197"></a><strong id="b5298037171914"><a name="b5298037171914"></a><a name="b5298037171914"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1729811375198"><td class="cellrowborder" valign="top" width="20.599999999999998%" headers="mcps1.2.3.1.1 "><p id="p829803711919"><a name="p829803711919"></a><a name="p829803711919"></a>对象同步范围</p>
    </td>
    <td class="cellrowborder" valign="top" width="79.4%" headers="mcps1.2.3.1.2 "><p id="p12981737151915"><a name="p12981737151915"></a><a name="p12981737151915"></a>选择是否同步“普通索引”。</p>
    <p id="p177893082014"><a name="p177893082014"></a><a name="p177893082014"></a>DRS将默认同步主键/唯一索引，普通索引是指除主键/唯一索引以外的其他类型索引。勾选普通索引将会同步全部的索引，不勾选则仅同步主键/唯一索引，普通索引不会同步。</p>
    </td>
    </tr>
    <tr id="row7298103791920"><td class="cellrowborder" valign="top" width="20.599999999999998%" headers="mcps1.2.3.1.1 "><p id="p12984372199"><a name="p12984372199"></a><a name="p12984372199"></a>同步对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="79.4%" headers="mcps1.2.3.1.2 "><p id="p16298637101913"><a name="p16298637101913"></a><a name="p16298637101913"></a>可选表级同步、库级同步、导入对象文件，您可以根据业务场景选择对应的数据进行同步。</p>
    <a name="ul14298153711196"></a><a name="ul14298153711196"></a><ul id="ul14298153711196"><li>选择数据的时候支持搜索，以便您快速选择需要的数据库对象。</li><li>如果有切换源数据库的操作，请在选择同步对象前单击右上角的<a name="image534341813472"></a><a name="image534341813472"></a><span><img id="image534341813472" src="figures/icon-刷新.png"></span>，以确保待选择的对象为最新源数据库对象。</li><li>在同步对象右侧已选对象框中，可以使用对象名映射功能进行源数据库和目标数据库中的同步对象映射，具体操作可参考<a href="对象名映射.md">对象名映射</a>。</li><li>选择导入对象文件，具体步骤和说明可参考<a href="导入同步对象.md">导入同步对象</a>。</li></ul>
    </td>
    </tr>
    </tbody>
    </table>

5.  在“数据加工“页面，可对需要加工的表对象进行数据过滤或添加附加列，完成后单击“下一步“。
    -   如果需要设置数据过滤，选择“数据过滤”，设置相关过滤规则。
    -   如果需要设置添加附加列，选择“附加列”，填写需要添加的列名和操作类型信息。

        相关操作可参考[数据加工](https://support.huaweicloud.com/usermanual-drs/drs_03_0035.html)。

        **图 6**  MySQL到GaussDB\(for MySQL\)主备版数据加工<a name="fig6202408381"></a>  
        ![](figures/MySQL到GaussDB(for-MySQL)主备版数据加工.png "MySQL到GaussDB(for-MySQL)主备版数据加工")

6.  在“预检查“页面，进行同步任务预校验，校验是否可进行实时同步。
    -   查看检查结果，如有不通过的检查项，需要修复不通过项后，单击“重新校验”按钮重新进行任务预校验。

        预检查不通过项处理建议请参见《数据复制服务用户指南》中的“[预检查不通过项修复方法](https://support.huaweicloud.com/usermanual-drs/drs_precheck.html)”。

    -   预检查完成后，且所有检查项结果均通过时，单击“下一步“。

        **图 7**  MySQL到GaussDB\(for MySQL\)主备版预检查<a name="zh-cn_topic_0141892586_fig23361684715"></a>  
        ![](figures/MySQL到GaussDB(for-MySQL)主备版预检查.png "MySQL到GaussDB(for-MySQL)主备版预检查")

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >所有检查项结果均通过时，若存在请确认项，需要阅读并确认详情后才可以继续执行下一步操作。


7.  在“任务确认“页面，设置同步任务的启动时间，并确认同步任务信息无误后，勾选协议，单击“启动任务“，提交同步任务。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   同步任务的启动时间可以根据业务需求，设置为“立即启动”或“稍后启动”。
    >-   预计同步任务启动后，会对源数据库和目标数据库的性能产生影响，建议选择业务低峰期，合理设置同步任务的启动时间。

8.  同步任务提交后，您可在“实时同步管理“页面，查看并管理自己的任务。
    -   您可查看任务提交后的状态，状态请参见[任务状态](https://support.huaweicloud.com/qs-drs/drs_06_0004.html)。
    -   在任务列表的右上角，单击![](figures/icon-刷新.png)刷新列表，可查看到最新的任务状态。



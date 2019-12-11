# 场景三：从本地Oracle数据库迁移到RDS for MySQL<a name="drs_07_0010"></a>

数据复制服务支持本地自建的Oracle数据库迁移至本云RDS for MySQL实例。

本小节将介绍通过公网网络方式进行 Oracle数据库-\>RDS for MySQL实例的数据迁移任务配置流程，其他引擎的配置流程类似。

## 前提条件<a name="section12806144412541"></a>

-   已登录数据复制服务控制台。
-   账户余额大于等于0元。
-   参见[在线迁移](https://support.huaweicloud.com/productdesc-drs/drs_01_0301.html)。
-   参见[使用须知](https://support.huaweicloud.com/qs-drs/drs_online_migration.html)。
-   参见[数据类型映射关系](https://support.huaweicloud.com/usermanual-drs/drs_08_0002.html)。

## 迁移步骤<a name="section12716329897"></a>

1.  在“在线迁移管理“页面，单击“创建迁移任务“，进入创建迁移任务页面。
2.  在“迁移实例”页面，填选任务名称、通知收件人信息、描述、迁移实例信息，单击“下一步”。

    **图 1**  迁移任务信息<a name="fig1616181811155"></a>  
    ![](figures/迁移任务信息-34.png "迁移任务信息-34")

    **表 1**  任务和描述

    <a name="table8146244204420"></a>
    <table><thead align="left"><tr id="row55731924204420"><th class="cellrowborder" valign="top" width="18.42%" id="mcps1.2.3.1.1"><p id="p17991967204420"><a name="p17991967204420"></a><a name="p17991967204420"></a><strong id="b1611223511352"><a name="b1611223511352"></a><a name="b1611223511352"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="81.58%" id="mcps1.2.3.1.2"><p id="p48063227204420"><a name="p48063227204420"></a><a name="p48063227204420"></a><strong id="b3002268111352"><a name="b3002268111352"></a><a name="b3002268111352"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row807311204420"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p65392260204420"><a name="p65392260204420"></a><a name="p65392260204420"></a>任务名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p62281730204420"><a name="p62281730204420"></a><a name="p62281730204420"></a>任务名称在4位到64位之间，必须以字母开头，不区分大小写，可以包含字母、数字、中划线或下划线，不能包含其他的特殊字符。</p>
    </td>
    </tr>
    <tr id="row1080215433911"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p158027493912"><a name="p158027493912"></a><a name="p158027493912"></a>任务异常通知设置</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p38891258184013"><a name="p38891258184013"></a><a name="p38891258184013"></a>该项为可选参数，开启之后，需要填写手机号码或者邮箱作为指定收件人。当迁移任务状态异常时，系统将发送通知给指定收件人。</p>
    <div class="note" id="note158461433104913"><a name="note158461433104913"></a><a name="note158461433104913"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p138461333114917"><a name="p138461333114917"></a><a name="p138461333114917"></a>收到确认短信或邮件之后，需要在48小时内处理，否则该功能订阅无效。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row38242492156"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p1677373232818"><a name="p1677373232818"></a><a name="p1677373232818"></a>时延阈值</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p6681185532914"><a name="p6681185532914"></a><a name="p6681185532914"></a>在增量迁移阶段，源数据库和目标数据库之间的同步有时会存在一个时间差，称为时延，单位为秒。</p>
    <p id="p75251915133018"><a name="p75251915133018"></a><a name="p75251915133018"></a>时延阈值设置是指时延超过一定的值后（时间阈值范围为1—3600s），DRS可以发送告警通知给指定收件人。告警通知将在时延稳定超过设定的阈值6min后发送，避免出现由于时延波动反复发送告警通知的情况。</p>
    <div class="note" id="note47298209309"><a name="note47298209309"></a><a name="note47298209309"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul354514492087"></a><a name="ul354514492087"></a><ul id="ul354514492087"><li>首次进入增量迁移阶段，会有较多数据等待同步，存在较大的时延，属于正常情况，不在此功能的监控范围之内。</li><li>设置时间阈值之前，需要填写收件人手机号或邮箱。</li><li>目前Oracle-&gt;PostgreSQL的迁移不支持设置时延阈值。</li></ul>
    </div></div>
    </td>
    </tr>
    <tr id="row23664659204420"><td class="cellrowborder" valign="top" width="18.42%" headers="mcps1.2.3.1.1 "><p id="p37789232204420"><a name="p37789232204420"></a><a name="p37789232204420"></a>描述</p>
    </td>
    <td class="cellrowborder" valign="top" width="81.58%" headers="mcps1.2.3.1.2 "><p id="p41028970204420"><a name="p41028970204420"></a><a name="p41028970204420"></a>描述不能超过256位，且不能包含!=&lt;&gt;&amp;'"特殊字符。</p>
    </td>
    </tr>
    </tbody>
    </table>

    **图 2**  迁移实例信息<a name="fig6487192516156"></a>  
    ![](figures/迁移实例信息-35.png "迁移实例信息-35")

    **表 2**  迁移实例信息

    <a name="table54580728204436"></a>
    <table><thead align="left"><tr id="row39932329204436"><th class="cellrowborder" valign="top" width="23.87%" id="mcps1.2.3.1.1"><p id="p13293221204436"><a name="p13293221204436"></a><a name="p13293221204436"></a><strong id="b2587841611355"><a name="b2587841611355"></a><a name="b2587841611355"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="76.13%" id="mcps1.2.3.1.2"><p id="p3009113204436"><a name="p3009113204436"></a><a name="p3009113204436"></a><strong id="b1577696211355"><a name="b1577696211355"></a><a name="b1577696211355"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row05147381129"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p951443871218"><a name="p951443871218"></a><a name="p951443871218"></a>数据流动方向</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p11514173891212"><a name="p11514173891212"></a><a name="p11514173891212"></a>选择入云。</p>
    <p id="p1983838136"><a name="p1983838136"></a><a name="p1983838136"></a>入云指目标端数据库为本云关系型数据库。</p>
    </td>
    </tr>
    <tr id="row0414184610580"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p1414046115813"><a name="p1414046115813"></a><a name="p1414046115813"></a>源数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p168249357197"><a name="p168249357197"></a><a name="p168249357197"></a>选择Oracle数据库。</p>
    </td>
    </tr>
    <tr id="row42411630204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p12790028204436"><a name="p12790028204436"></a><a name="p12790028204436"></a>目标数据库引擎</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p1969552512018"><a name="p1969552512018"></a><a name="p1969552512018"></a>选择MySQL数据库。</p>
    <p id="p1879851205213"><a name="p1879851205213"></a><a name="p1879851205213"></a>目前支持可选的数据库引擎有：MySQL和PostgreSQL。</p>
    </td>
    </tr>
    <tr id="row62907306204436"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p62327044204436"><a name="p62327044204436"></a><a name="p62327044204436"></a>网络类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p34229323253"><a name="p34229323253"></a><a name="p34229323253"></a>默认为公网网络类型，支持公网网络和VPN、专线网络。</p>
    <p id="p2932133722411"><a name="p2932133722411"></a><a name="p2932133722411"></a>您可以根据实际情况选用合适的网络方式，此处以公网网络方式为示例。</p>
    </td>
    </tr>
    <tr id="row658644204515"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p53350183204515"><a name="p53350183204515"></a><a name="p53350183204515"></a>目标数据库实例</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><p id="p26397538204515"><a name="p26397538204515"></a><a name="p26397538204515"></a>用户所创建的目标数据库实例。</p>
    </td>
    </tr>
    <tr id="row1781142655112"><td class="cellrowborder" valign="top" width="23.87%" headers="mcps1.2.3.1.1 "><p id="p128192616518"><a name="p128192616518"></a><a name="p128192616518"></a>迁移模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.13%" headers="mcps1.2.3.1.2 "><a name="ul493112214103"></a><a name="ul493112214103"></a><ul id="ul493112214103"><li>全量<div class="p" id="p16545111015102"><a name="p16545111015102"></a><a name="p16545111015102"></a>该模式为数据库一次性迁移，适用于可中断业务的<span class="keyword" id="keyword8520910122110"><a name="keyword8520910122110"></a><a name="keyword8520910122110"></a>数据库迁移</span>场景，全量迁移将用户选择的数据库对象和数据一次性迁移至目标端数据库。<div class="note" id="note1989394717302"><a name="note1989394717302"></a><a name="note1989394717302"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p12614191914218"><a name="p12614191914218"></a><a name="p12614191914218"></a>如果用户只进行全量迁移时，建议停止对源数据库的操作，否则迁移过程中源数据库产生的新数据不会同步到目标数据库。</p>
    </div></div>
    </div>
    </li><li>全量+增量<p id="p75178431296"><a name="p75178431296"></a><a name="p75178431296"></a>该模式为数据库持续性迁移，适用于对业务中断敏感的场景，通过全量迁移过程完成目标端数据库的初始化后，增量迁移阶段通过解析日志等技术，将源端和目标端数据库保持数据持续一致。</p>
    <div class="note" id="note15794162815109"><a name="note15794162815109"></a><a name="note15794162815109"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul819763691118"></a><a name="ul819763691118"></a><ul id="ul819763691118"><li>目前Oracle-&gt;PostgreSQL的迁移不支持选择全量+增量的迁移模式。</li><li>选择<span class="uicontrol" id="uicontrol24738122117"><a name="uicontrol24738122117"></a><a name="uicontrol24738122117"></a>“全量+增量”</span>迁移模式，增量迁移可以在全量迁移完成的基础上实现数据的持续同步，无需中断业务，实现迁移过程中源业务和数据库继续对外提供访问。</li></ul>
    </div></div>
    </li></ul>
    </td>
    </tr>
    </tbody>
    </table>

3.  在“源库及目标库”页面，迁移实例创建成功后，填选源库信息和目标库信息，建议您单击“源库和目标库“处的“测试连接“，分别测试并确定与源库和目标库连通后，勾选协议，单击“下一步“。

    **图 3**  源库信息配置<a name="fig7958531468"></a>  
    ![](figures/源库信息配置.png "源库信息配置")

    **表 3**  源库信息

    <a name="table5827152923"></a>
    <table><thead align="left"><tr id="row48273219210"><th class="cellrowborder" valign="top" width="22.869999999999997%" id="mcps1.2.3.1.1"><p id="p198276214213"><a name="p198276214213"></a><a name="p198276214213"></a><strong id="b98275220212"><a name="b98275220212"></a><a name="b98275220212"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="77.13%" id="mcps1.2.3.1.2"><p id="p1282713218211"><a name="p1282713218211"></a><a name="p1282713218211"></a><strong id="b168271421523"><a name="b168271421523"></a><a name="b168271421523"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row198277210215"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p68272021227"><a name="p68272021227"></a><a name="p68272021227"></a>IP地址或域名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p696045254811"><a name="p696045254811"></a><a name="p696045254811"></a>源数据库的IP地址或域名。</p>
    </td>
    </tr>
    <tr id="row1982742821"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p3827162426"><a name="p3827162426"></a><a name="p3827162426"></a>端口</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p1082792823"><a name="p1082792823"></a><a name="p1082792823"></a>源数据库服务端口，可输入范围为1~65535间的整数。</p>
    </td>
    </tr>
    <tr id="row188271221621"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p16827121429"><a name="p16827121429"></a><a name="p16827121429"></a>数据库服务名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p1282702525"><a name="p1282702525"></a><a name="p1282702525"></a>数据库服务名（Service Name/SID）指定了客户端可以通过其连接到Oracle数据库。</p>
    <p id="p34591096106"><a name="p34591096106"></a><a name="p34591096106"></a>配置该项信息时，选填Service Name或者SID中任何一种均可，具体的名称需要与所选的类型对应。</p>
    <p id="p188910613418"><a name="p188910613418"></a><a name="p188910613418"></a>您可以通过如下方法获取具体的数据库服务名，查询数据库服务名称时需要使用具备DBA权限的用户进行查询：</p>
    <a name="ul1185073217520"></a><a name="ul1185073217520"></a><ul id="ul1185073217520"><li>查看Service Name：使用如下语句中任何一种均可。<a name="ul563302616"></a><a name="ul563302616"></a><ul id="ul563302616"><li>语句一<pre class="codeblock" id="codeblock634110220129"><a name="codeblock634110220129"></a><a name="codeblock634110220129"></a>select value from v$parameter where name like '%service_name%';</pre>
    </li><li>语句二<pre class="codeblock" id="codeblock1736711012134"><a name="codeblock1736711012134"></a><a name="codeblock1736711012134"></a>show parameter service_name;</pre>
    </li></ul>
    </li><li>查看SID：<pre class="codeblock" id="codeblock933642420138"><a name="codeblock933642420138"></a><a name="codeblock933642420138"></a>select instance_name from V$instance;</pre>
    </li></ul>
    </td>
    </tr>
    <tr id="row16827162722"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p128271529210"><a name="p128271529210"></a><a name="p128271529210"></a>数据库用户名</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p1754762917167"><a name="p1754762917167"></a><a name="p1754762917167"></a>源数据库的用户名。</p>
    </td>
    </tr>
    <tr id="row178118576471"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p181195714474"><a name="p181195714474"></a><a name="p181195714474"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p2826124491610"><a name="p2826124491610"></a><a name="p2826124491610"></a>源数据库的用户名所对应的密码。</p>
    </td>
    </tr>
    <tr id="row1798013414810"><td class="cellrowborder" valign="top" width="22.869999999999997%" headers="mcps1.2.3.1.1 "><p id="p59804420484"><a name="p59804420484"></a><a name="p59804420484"></a>SSL安全连接</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.13%" headers="mcps1.2.3.1.2 "><p id="p10548132911617"><a name="p10548132911617"></a><a name="p10548132911617"></a>通过该功能，用户可以选择是否开启对迁移链路的加密。如果开启该功能，需要用户上传SSL CA根证书。</p>
    <div class="note" id="note1413165611199"><a name="note1413165611199"></a><a name="note1413165611199"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p1413205651918"><a name="p1413205651918"></a><a name="p1413205651918"></a>最大支持上传500KB的证书文件。</p>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

    **图 4**  目标库信息配置<a name="fig348042394017"></a>  
    ![](figures/目标库信息配置.png "目标库信息配置")

    **表 4**  目标库信息

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
    <tr id="row16827721222"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p1682742623"><a name="p1682742623"></a><a name="p1682742623"></a>数据库密码</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p121331113174115"><a name="p121331113174115"></a><a name="p121331113174115"></a>目标数据库对应的数据库密码。</p>
    <p id="p19827328211"><a name="p19827328211"></a><a name="p19827328211"></a>数据库用户名和密码将被系统加密暂存，直至该任务删除后清除。</p>
    </td>
    </tr>
    </tbody>
    </table>

4.  在“迁移设置“页面，设置迁移对象，单击“下一步“。

    **图 5**  设定迁移<a name="fig46205265911"></a>  
    ![](figures/设定迁移.png "设定迁移")

    **表 5**  迁移对象

    <a name="table165921932111919"></a>
    <table><thead align="left"><tr id="row165921632141911"><th class="cellrowborder" valign="top" width="16%" id="mcps1.2.3.1.1"><p id="p1759233261916"><a name="p1759233261916"></a><a name="p1759233261916"></a><strong id="b1783318515228"><a name="b1783318515228"></a><a name="b1783318515228"></a>参数</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="84%" id="mcps1.2.3.1.2"><p id="p159273271920"><a name="p159273271920"></a><a name="p159273271920"></a><strong id="b10555114922418"><a name="b10555114922418"></a><a name="b10555114922418"></a>描述</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row559273214193"><td class="cellrowborder" valign="top" width="16%" headers="mcps1.2.3.1.1 "><p id="p14592132171916"><a name="p14592132171916"></a><a name="p14592132171916"></a>迁移对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="84%" headers="mcps1.2.3.1.2 "><p id="p884981051017"><a name="p884981051017"></a><a name="p884981051017"></a>目前迁移对象仅支持自定义对象，选择的粒度为视图和表。 数据库对象迁移成功之后，在目标数据库中以小写的名称进行保存。如果有切换源数据库的操作，请在选择迁移对象前单击右上角的<a name="image93591350193213"></a><a name="image93591350193213"></a><span><img id="image93591350193213" src="figures/drs_icon-2.png"></span>，以确保待选择的对象为最新源数据库对象。</p>
    <div class="note" id="note6192135932115"><a name="note6192135932115"></a><a name="note6192135932115"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul1912265111211"></a><a name="ul1912265111211"></a><ul id="ul1912265111211"><li>若所选的数据库进行迁移时，由于视图、表等对象可能与其他数据库的视图、表存在依赖关系，若所依赖的视图或表未迁移，则会导致迁移失败。建议您在迁移之前进行确认。</li><li>Oracle到PostgreSQL的场景迁移对象最多只能选择一个数据库。</li></ul>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

5.  在“预检查“页面，进行迁移任务预校验，校验是否可进行迁移。
    -   查看检查结果，如有失败的检查项，需要修复失败项后，单击“重新校验”按钮重新进行迁移任务预校验。

        预检查失败项处理建议请参见《数据复制服务用户指南》中的“[预检查失败项修复方法](https://support.huaweicloud.com/usermanual-drs/drs_precheck.html)”。

        **图 6**  预检查<a name="fig237882315489"></a>  
        ![](figures/预检查-36.png "预检查-36")

    -   预检查完成后，且预检查通过率为100%时，单击“下一步”。

        >![](public_sys-resources/icon-note.gif) **说明：**   
        >所有检查项结果均成功时，若存在告警，需要阅读并确认告警详情后才可以继续执行下一步操作。  


6.  在“任务确认“页面，设置迁移任务的启动时间，并确认迁移任务信息无误后，单击“启动任务“，提交迁移任务。

    迁移任务的启动时间可以根据业务需求，设置为“立即启动”或“稍后启动”。

    预计迁移任务启动后，会对源数据库和目标数据库的性能产生影响，建议选择业务低峰期，合理设置迁移任务的启动时间。

7.  迁移任务提交后，您可在“在线迁移管理“页面，查看并管理自己的任务。
    -   您可查看任务提交后的状态，状态请参见[任务状态](https://support.huaweicloud.com/qs-drs/drs_03_0001.html)。
    -   在任务列表的右上角，单击![](figures/drs_icon-2.png)刷新列表，可查看到最新的任务状态。

8.  迁移任务创建成功后，请参见《数据复制服务快速入门》的[使用流程](https://support.huaweicloud.com/qs-drs/drs_02_0001.html)，进行完整的数据业务割接。


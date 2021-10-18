# SDK接口介绍<a name="drs_15_0007"></a>

SDK中定义了多种类对象，本小节简单介绍SDK的这些类的接口定义。

-   SubscribeContext接口定义

    **表 1**  SubscribeContext接口定义

    <a name="table36371119151313"></a>
    <table><thead align="left"><tr id="row196375194138"><th class="cellrowborder" valign="top" width="30%" id="mcps1.2.3.1.1"><p id="p13637919151318"><a name="p13637919151318"></a><a name="p13637919151318"></a><strong id="b1538917585143"><a name="b1538917585143"></a><a name="b1538917585143"></a>函数名称</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="70%" id="mcps1.2.3.1.2"><p id="p1165331941314"><a name="p1165331941314"></a><a name="p1165331941314"></a><strong id="b133891058131419"><a name="b133891058131419"></a><a name="b133891058131419"></a>说明</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row176531719131315"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p166061945130"><a name="p166061945130"></a><a name="p166061945130"></a>setDomainName(String domainName)</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p175749512198"><a name="p175749512198"></a><a name="p175749512198"></a>设置用户名。</p>
    <p id="p06531719141310"><a name="p06531719141310"></a><a name="p06531719141310"></a>参数为创建所需数据订阅任务的本云帐号。</p>
    </td>
    </tr>
    <tr id="row13653101913134"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p1565331910138"><a name="p1565331910138"></a><a name="p1565331910138"></a>setPassword(String password)</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p210614117191"><a name="p210614117191"></a><a name="p210614117191"></a>设置用户密码。</p>
    <p id="p165381913137"><a name="p165381913137"></a><a name="p165381913137"></a>参数为创建所需数据订阅任务的本云帐号密码。</p>
    </td>
    </tr>
    <tr id="row1165311911313"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p136065491318"><a name="p136065491318"></a><a name="p136065491318"></a>setIp(String ip)</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p1474681410193"><a name="p1474681410193"></a><a name="p1474681410193"></a>设置订阅通道的IP。</p>
    <p id="p7653181911131"><a name="p7653181911131"></a><a name="p7653181911131"></a>在数据订阅页面，选择指定订阅任务，单击任务名称，在基本信息页签下，获取订阅实例信息的内部IP即可。</p>
    </td>
    </tr>
    <tr id="row2065315199130"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p6653131911320"><a name="p6653131911320"></a><a name="p6653131911320"></a>setUserId(String userId)</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p93314151819"><a name="p93314151819"></a><a name="p93314151819"></a>用户ID。</p>
    <p id="p2653319151314"><a name="p2653319151314"></a><a name="p2653319151314"></a>登录控制台之后，单击右上角“账户名&gt;我的凭证&gt;用户ID”，复制用户ID即可。</p>
    </td>
    </tr>
    </tbody>
    </table>

-   ClusterClient接口定义

    **表 2**  ClusterClient接口定义

    <a name="table912181412011"></a>
    <table><thead align="left"><tr id="row151291420205"><th class="cellrowborder" valign="top" width="30%" id="mcps1.2.3.1.1"><p id="p1712171415208"><a name="p1712171415208"></a><a name="p1712171415208"></a><strong id="b102868417208"><a name="b102868417208"></a><a name="b102868417208"></a>函数名称</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="70%" id="mcps1.2.3.1.2"><p id="p61211142206"><a name="p61211142206"></a><a name="p61211142206"></a><strong id="b228614172016"><a name="b228614172016"></a><a name="b228614172016"></a>说明</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row191213145207"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p14128149208"><a name="p14128149208"></a><a name="p14128149208"></a>void addClusterListener(ClusterListener var1)</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p589036134917"><a name="p589036134917"></a><a name="p589036134917"></a>添加下游监听者。监听者加入到一个ClusterClient中，才可以订阅订阅通道中的增量数据。</p>
    <p id="p104331640182113"><a name="p104331640182113"></a><a name="p104331640182113"></a>参数ClusterListener arg0 为类ClusterListener的对象。</p>
    </td>
    </tr>
    <tr id="row4121014132018"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p1612214202017"><a name="p1612214202017"></a><a name="p1612214202017"></a>void start()</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p8124141208"><a name="p8124141208"></a><a name="p8124141208"></a>启动SDK客户端，开始订阅增量数据。</p>
    </td>
    </tr>
    <tr id="row131281411203"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p312414152014"><a name="p312414152014"></a><a name="p312414152014"></a>void stop()</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p1812171418208"><a name="p1812171418208"></a><a name="p1812171418208"></a>停止订阅增量数据。</p>
    </td>
    </tr>
    </tbody>
    </table>

-   ClusterListener接口定义

    **表 3**  ClusterListener接口定义

    <a name="table1686713286230"></a>
    <table><thead align="left"><tr id="row108671028112318"><th class="cellrowborder" valign="top" width="30%" id="mcps1.2.3.1.1"><p id="p5867192832320"><a name="p5867192832320"></a><a name="p5867192832320"></a><strong id="b1880481093517"><a name="b1880481093517"></a><a name="b1880481093517"></a>函数名称</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="70%" id="mcps1.2.3.1.2"><p id="p18867132819234"><a name="p18867132819234"></a><a name="p18867132819234"></a><strong id="b198198107350"><a name="b198198107350"></a><a name="b198198107350"></a>说明</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1886732817236"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p15867202862315"><a name="p15867202862315"></a><a name="p15867202862315"></a>void notify(List&lt;ClusterMessage&gt; var1)</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p186720282233"><a name="p186720282233"></a><a name="p186720282233"></a>该函数主要用于定义增量数据的消费。当SDK接收到数据时，会通过notify通知ClusterListner消费数据。例如<a href="SDK使用说明.md#section14870536164719">SDK使用模版</a>的消费方式，就是将订阅数据打印到屏幕上。</p>
    <p id="p1912510620256"><a name="p1912510620256"></a><a name="p1912510620256"></a>该函数输入参数类型为：List &lt;ClusterMessage&gt;, 其中ClusterMessage为订阅数据存储的结构对象，具体定义详见<a href="#table5115642614">表4</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

-   ClusterMessage接口定义

    每个ClusterMessage保存RDS中的一个事务的数据记录，事务中的每条记录通过Record保存。

    **表 4**  ClusterMessage接口定义

    <a name="table5115642614"></a>
    <table><thead align="left"><tr id="row111176132611"><th class="cellrowborder" valign="top" width="30%" id="mcps1.2.3.1.1"><p id="p181126122615"><a name="p181126122615"></a><a name="p181126122615"></a><strong id="b3820184633414"><a name="b3820184633414"></a><a name="b3820184633414"></a>函数名称</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="70%" id="mcps1.2.3.1.2"><p id="p171146192613"><a name="p171146192613"></a><a name="p171146192613"></a><strong id="b19820164653416"><a name="b19820164653416"></a><a name="b19820164653416"></a>说明</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row911116152614"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p1111126162610"><a name="p1111126162610"></a><a name="p1111126162610"></a>Record getRecord()</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p8116632611"><a name="p8116632611"></a><a name="p8116632611"></a>该接口从ClusterMessage中获取一条变更记录。这个变更记录表示RDS的binlog文件中的每一条记录，例如begin，commit，update，insert等。</p>
    </td>
    </tr>
    </tbody>
    </table>

-   Record接口定义

    Record代表订阅的RDS的binlog文件中的每条记录，例如begin，commit，update等。

    **表 5**  Record接口定义

    <a name="table147521811143120"></a>
    <table><thead align="left"><tr id="row1775231153120"><th class="cellrowborder" valign="top" width="30%" id="mcps1.2.3.1.1"><p id="p77521411113115"><a name="p77521411113115"></a><a name="p77521411113115"></a><strong id="b330473519313"><a name="b330473519313"></a><a name="b330473519313"></a>函数名称</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="70%" id="mcps1.2.3.1.2"><p id="p15752131113319"><a name="p15752131113319"></a><a name="p15752131113319"></a><strong id="b10304035163115"><a name="b10304035163115"></a><a name="b10304035163115"></a>说明</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row20752411113110"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p19752101117314"><a name="p19752101117314"></a><a name="p19752101117314"></a>String getAttribute(final String key)</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p5752201113311"><a name="p5752201113311"></a><a name="p5752201113311"></a>该函数可以获取Record中主要的一些属性值。传入参数为属性名，返回这个属性的值。</p>
    <p id="p342931012328"><a name="p342931012328"></a><a name="p342931012328"></a>可以调用这个函数获取的属性名及对应的属性值如<a href="#table16273123023">表6</a>所示。</p>
    </td>
    </tr>
    <tr id="row18752141133111"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p1575219114319"><a name="p1575219114319"></a><a name="p1575219114319"></a>Type getOpt()</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p7112191815911"><a name="p7112191815911"></a><a name="p7112191815911"></a>获取这条记录的变更类型，包括： insert、delete、update、replace、ddl、begin、commit、heartbeat。</p>
    </td>
    </tr>
    <tr id="row197522116313"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p1575221143115"><a name="p1575221143115"></a><a name="p1575221143115"></a>String getCheckpoint()</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p211221819915"><a name="p211221819915"></a><a name="p211221819915"></a>获取这条变更记录在binlog中的位点，返回的位点格式为：binlog_offset@binlog_fid。</p>
    <p id="p11112201811911"><a name="p11112201811911"></a><a name="p11112201811911"></a>其中binlog_offset为变更记录在binlog文件中的偏移量，binlog_fid为binlog文件的数字后缀，例如binlog文件名为mysql-bin.00092，那么binlog_fid为92。</p>
    </td>
    </tr>
    <tr id="row1275241173110"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p10752311153111"><a name="p10752311153111"></a><a name="p10752311153111"></a>int getFieldCount()</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p197521711103110"><a name="p197521711103110"></a><a name="p197521711103110"></a>获取这条变更记录的字段Field的个数。</p>
    </td>
    </tr>
    <tr id="row175215115316"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p19752161153115"><a name="p19752161153115"></a><a name="p19752161153115"></a>List &lt;Field&gt; getFieldList()</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p7326954145810"><a name="p7326954145810"></a><a name="p7326954145810"></a>该函数返回结果的数据类型为List &lt;Field&gt;。</p>
    <p id="p1411271812915"><a name="p1411271812915"></a><a name="p1411271812915"></a>List &lt;Field&gt; 包含了这条变更记录对应表的所有字段的定义及变更前后的镜像值，Field对象的定义详见<a href="#table0167101163715">表7</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

    **表 6**  属性信息

    <a name="table16273123023"></a>
    <table><thead align="left"><tr id="row1227332320216"><th class="cellrowborder" valign="top" width="30%" id="mcps1.2.3.1.1"><p id="p927312317212"><a name="p927312317212"></a><a name="p927312317212"></a><strong id="b9728202620104"><a name="b9728202620104"></a><a name="b9728202620104"></a>key</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="70%" id="mcps1.2.3.1.2"><p id="p132734238213"><a name="p132734238213"></a><a name="p132734238213"></a><strong id="b1970710817561"><a name="b1970710817561"></a><a name="b1970710817561"></a>说明</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row142739231626"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p15273112318217"><a name="p15273112318217"></a><a name="p15273112318217"></a>record_id</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p1227316231024"><a name="p1227316231024"></a><a name="p1227316231024"></a>这条Record的ID，这个ID在订阅过程中不保证递增。</p>
    </td>
    </tr>
    <tr id="row227313231828"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p827312320214"><a name="p827312320214"></a><a name="p827312320214"></a>instance</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p1327313237212"><a name="p1327313237212"></a><a name="p1327313237212"></a>这条Record对应的数据库实例的连接地址，格式为：ip:port。</p>
    </td>
    </tr>
    <tr id="row16273192311217"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p11273923624"><a name="p11273923624"></a><a name="p11273923624"></a>source_type</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p9273923321"><a name="p9273923321"></a><a name="p9273923321"></a>这条Record对应数据库实例的引擎类型，目前只支持MySQL。</p>
    </td>
    </tr>
    <tr id="row027382313212"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p182731123121"><a name="p182731123121"></a><a name="p182731123121"></a>source_category</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p12731923126"><a name="p12731923126"></a><a name="p12731923126"></a>这条Record的类型，目前只支持full_recorded。</p>
    </td>
    </tr>
    <tr id="row132739231224"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p1027315230217"><a name="p1027315230217"></a><a name="p1027315230217"></a>timestamp</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p1695511146110"><a name="p1695511146110"></a><a name="p1695511146110"></a>这条Record写入binlog的时间，这个时间同时也是这条SQL在RDS中执行的时间。</p>
    </td>
    </tr>
    <tr id="row6273123829"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p02730231823"><a name="p02730231823"></a><a name="p02730231823"></a>checkpoint</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p995520141115"><a name="p995520141115"></a><a name="p995520141115"></a>这条Record对应的binlog文件的位点，格式为:file_offset@file_name，file_name为binlog文件的数字后缀。</p>
    </td>
    </tr>
    <tr id="row152731239210"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p1627392316210"><a name="p1627392316210"></a><a name="p1627392316210"></a>record_type</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p1395518141712"><a name="p1395518141712"></a><a name="p1395518141712"></a>这条Record对应的操作类型，主要取值包括：insert/update/delete/replace/ddl/begin/commit/heartbeat。</p>
    </td>
    </tr>
    <tr id="row172732234211"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p4273423825"><a name="p4273423825"></a><a name="p4273423825"></a>db</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p10273142313217"><a name="p10273142313217"></a><a name="p10273142313217"></a>这条Record更新对应的数据库名。</p>
    </td>
    </tr>
    <tr id="row1427318231724"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p627311231123"><a name="p627311231123"></a><a name="p627311231123"></a>table_name</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p327314231228"><a name="p327314231228"></a><a name="p327314231228"></a>这条Record更新表的表名。</p>
    </td>
    </tr>
    <tr id="row1273192312210"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p1227314232213"><a name="p1227314232213"></a><a name="p1227314232213"></a>record_recording</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p527310232219"><a name="p527310232219"></a><a name="p527310232219"></a>这条Record对应的编码。</p>
    </td>
    </tr>
    </tbody>
    </table>

-   Field接口定义

    Field类定义了每个字段的编码、类型、字段名、字段值以及是否为主键等属性，Field类的各个接口定义如[表7](#table0167101163715)所示。

    **表 7**  Field接口定义

    <a name="table0167101163715"></a>
    <table><thead align="left"><tr id="row1916721116376"><th class="cellrowborder" valign="top" width="30%" id="mcps1.2.3.1.1"><p id="p71671111173719"><a name="p71671111173719"></a><a name="p71671111173719"></a><strong id="b1125873923717"><a name="b1125873923717"></a><a name="b1125873923717"></a>函数名称</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="70%" id="mcps1.2.3.1.2"><p id="p10167171114378"><a name="p10167171114378"></a><a name="p10167171114378"></a><strong id="b1425819398377"><a name="b1425819398377"></a><a name="b1425819398377"></a>说明</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1516715118376"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p141671511103717"><a name="p141671511103717"></a><a name="p141671511103717"></a>String getEncoding()</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p71674115379"><a name="p71674115379"></a><a name="p71674115379"></a>获取该字段值的编码格式。</p>
    </td>
    </tr>
    <tr id="row916711112373"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p111671811103711"><a name="p111671811103711"></a><a name="p111671811103711"></a>String getFieldname()</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p2016711133710"><a name="p2016711133710"></a><a name="p2016711133710"></a>获取该字段的名称。</p>
    </td>
    </tr>
    <tr id="row2167411173715"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p20415121153811"><a name="p20415121153811"></a><a name="p20415121153811"></a>Type getType()</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p2167111123716"><a name="p2167111123716"></a><a name="p2167111123716"></a>获取该字段的数据类型，Type的定义具体参见字段类型定义。</p>
    </td>
    </tr>
    <tr id="row3167011173710"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p616731133711"><a name="p616731133711"></a><a name="p616731133711"></a>ByteString getValue()</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p141673116372"><a name="p141673116372"></a><a name="p141673116372"></a>获取该字段的值，返回类型为ByteString,当值为空时，返回NULL。</p>
    </td>
    </tr>
    <tr id="row5167151123711"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.2.3.1.1 "><p id="p1367984616388"><a name="p1367984616388"></a><a name="p1367984616388"></a>Boolean isPrimary()</p>
    </td>
    <td class="cellrowborder" valign="top" width="70%" headers="mcps1.2.3.1.2 "><p id="p71671811163718"><a name="p71671811163718"></a><a name="p71671811163718"></a>判断该字段是否是表的主键列，如果是返回True，否则返回False。</p>
    </td>
    </tr>
    </tbody>
    </table>



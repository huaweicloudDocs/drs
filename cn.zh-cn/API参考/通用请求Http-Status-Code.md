# 通用请求Http Status Code<a name="drs_05_0003"></a>

-   正常

    **表 1**  正常返回说明

    <a name="table7063486"></a>
    <table><thead align="left"><tr id="row7125975"><th class="cellrowborder" valign="top" width="15.15%" id="mcps1.2.3.1.1"><p id="p40333087"><a name="p40333087"></a><a name="p40333087"></a><strong id="b1839231819351"><a name="b1839231819351"></a><a name="b1839231819351"></a>返回值</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="84.85000000000001%" id="mcps1.2.3.1.2"><p id="p45754591"><a name="p45754591"></a><a name="p45754591"></a><strong id="b3392141818358"><a name="b3392141818358"></a><a name="b3392141818358"></a>说明</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row15134400"><td class="cellrowborder" valign="top" width="15.15%" headers="mcps1.2.3.1.1 "><p id="p17926889"><a name="p17926889"></a><a name="p17926889"></a>200</p>
    </td>
    <td class="cellrowborder" valign="top" width="84.85000000000001%" headers="mcps1.2.3.1.2 "><p id="p42791939"><a name="p42791939"></a><a name="p42791939"></a>请求成功。</p>
    </td>
    </tr>
    <tr id="row49583138"><td class="cellrowborder" valign="top" width="15.15%" headers="mcps1.2.3.1.1 "><p id="p56811240"><a name="p56811240"></a><a name="p56811240"></a>202</p>
    </td>
    <td class="cellrowborder" valign="top" width="84.85000000000001%" headers="mcps1.2.3.1.2 "><p id="p38307698"><a name="p38307698"></a><a name="p38307698"></a>异步请求成功提交（任务执行等）。</p>
    </td>
    </tr>
    </tbody>
    </table>


-   异常

    **表 2**  异常返回说明

    <a name="table49008235"></a>
    <table><thead align="left"><tr id="row2282555"><th class="cellrowborder" valign="top" width="43.43%" id="mcps1.2.3.1.1"><p id="p50669287"><a name="p50669287"></a><a name="p50669287"></a><strong id="b18956102811354"><a name="b18956102811354"></a><a name="b18956102811354"></a>返回值</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="56.57%" id="mcps1.2.3.1.2"><p id="p10571616"><a name="p10571616"></a><a name="p10571616"></a><strong id="b1395642853518"><a name="b1395642853518"></a><a name="b1395642853518"></a>说明</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row50994573"><td class="cellrowborder" valign="top" width="43.43%" headers="mcps1.2.3.1.1 "><p id="p36919767"><a name="p36919767"></a><a name="p36919767"></a>400 Bad Request</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.57%" headers="mcps1.2.3.1.2 "><p id="p37711141"><a name="p37711141"></a><a name="p37711141"></a>服务器未能处理请求。</p>
    </td>
    </tr>
    <tr id="row3855953"><td class="cellrowborder" valign="top" width="43.43%" headers="mcps1.2.3.1.1 "><p id="p43896801"><a name="p43896801"></a><a name="p43896801"></a>401 Unauthorized</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.57%" headers="mcps1.2.3.1.2 "><p id="p65980010"><a name="p65980010"></a><a name="p65980010"></a>被请求的页面需要用户名和密码。</p>
    </td>
    </tr>
    <tr id="row56949179"><td class="cellrowborder" valign="top" width="43.43%" headers="mcps1.2.3.1.1 "><p id="p49480747"><a name="p49480747"></a><a name="p49480747"></a>403 Forbidden</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.57%" headers="mcps1.2.3.1.2 "><p id="p48517543"><a name="p48517543"></a><a name="p48517543"></a>对被请求页面的访问被禁止。</p>
    </td>
    </tr>
    <tr id="row34004710"><td class="cellrowborder" valign="top" width="43.43%" headers="mcps1.2.3.1.1 "><p id="p2918112"><a name="p2918112"></a><a name="p2918112"></a>404 Not Found</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.57%" headers="mcps1.2.3.1.2 "><p id="p35040539"><a name="p35040539"></a><a name="p35040539"></a>服务器无法找到被请求的页面。</p>
    </td>
    </tr>
    <tr id="row46929400"><td class="cellrowborder" valign="top" width="43.43%" headers="mcps1.2.3.1.1 "><p id="p43185079"><a name="p43185079"></a><a name="p43185079"></a>405 Method Not Allowed</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.57%" headers="mcps1.2.3.1.2 "><p id="p8330506"><a name="p8330506"></a><a name="p8330506"></a>请求中指定的方法不被允许。</p>
    </td>
    </tr>
    <tr id="row7865695"><td class="cellrowborder" valign="top" width="43.43%" headers="mcps1.2.3.1.1 "><p id="p33141548"><a name="p33141548"></a><a name="p33141548"></a>409 Conflict</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.57%" headers="mcps1.2.3.1.2 "><p id="p110849"><a name="p110849"></a><a name="p110849"></a>由于冲突，请求无法被完成。</p>
    </td>
    </tr>
    <tr id="row997647"><td class="cellrowborder" valign="top" width="43.43%" headers="mcps1.2.3.1.1 "><p id="p13700548"><a name="p13700548"></a><a name="p13700548"></a>413 Request Entity Too Large</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.57%" headers="mcps1.2.3.1.2 "><p id="p36002581"><a name="p36002581"></a><a name="p36002581"></a>请求超过资源配额。</p>
    </td>
    </tr>
    <tr id="row55587780"><td class="cellrowborder" valign="top" width="43.43%" headers="mcps1.2.3.1.1 "><p id="p6316364"><a name="p6316364"></a><a name="p6316364"></a>415 Unsupported Media Type</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.57%" headers="mcps1.2.3.1.2 "><p id="p41863460"><a name="p41863460"></a><a name="p41863460"></a>请求头中携带的Content-Type类型不正确，必须为application/json。</p>
    </td>
    </tr>
    <tr id="row41226821"><td class="cellrowborder" valign="top" width="43.43%" headers="mcps1.2.3.1.1 "><p id="p51038233"><a name="p51038233"></a><a name="p51038233"></a>422 Unprocessable Entity</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.57%" headers="mcps1.2.3.1.2 "><p id="p40456209"><a name="p40456209"></a><a name="p40456209"></a>请求中的参数或对象不能被正确识别。</p>
    </td>
    </tr>
    <tr id="row28561566"><td class="cellrowborder" valign="top" width="43.43%" headers="mcps1.2.3.1.1 "><p id="p31785544"><a name="p31785544"></a><a name="p31785544"></a>500 Internal Server Error</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.57%" headers="mcps1.2.3.1.2 "><p id="p24492299"><a name="p24492299"></a><a name="p24492299"></a>请求未完成。服务异常。</p>
    </td>
    </tr>
    <tr id="row19104101"><td class="cellrowborder" valign="top" width="43.43%" headers="mcps1.2.3.1.1 "><p id="p3928319"><a name="p3928319"></a><a name="p3928319"></a>501 Not Implemented</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.57%" headers="mcps1.2.3.1.2 "><p id="p49758405"><a name="p49758405"></a><a name="p49758405"></a>请求未完成。服务器不支持所请求的功能。</p>
    </td>
    </tr>
    <tr id="row45172469"><td class="cellrowborder" valign="top" width="43.43%" headers="mcps1.2.3.1.1 "><p id="p35091369"><a name="p35091369"></a><a name="p35091369"></a>503 Service Unavailable</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.57%" headers="mcps1.2.3.1.2 "><p id="p23828670"><a name="p23828670"></a><a name="p23828670"></a>请求未完成。系统暂时异常。</p>
    </td>
    </tr>
    </tbody>
    </table>



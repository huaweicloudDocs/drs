# Token认证<a name="drs_01_0005"></a>

## 应用场景<a name="section62137769"></a>

当您使用Token认证方式完成认证鉴权时，需要获取用户Token并在调用接口时增加“X-Auth-Token”到业务接口请求消息头中。

本节介绍如何调用接口完成Token认证。

## 调用接口步骤<a name="section22369015"></a>

1.  发送“POST https://_xxx_/v3/auth/tokens”请求。

    上述“xxx”表示IAM的Endpoint信息，获取IAM的Endpoint信息以及消息体中的区域名称，请参见[地区和终端节点](http://developer.huaweicloud.com/endpoint.html)。

    **表 1**  Header参数说明

    <a name="table27409210"></a>
    <table><thead align="left"><tr id="row16913743"><th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.1"><p id="p27835949"><a name="p27835949"></a><a name="p27835949"></a><strong id="b610071881012"><a name="b610071881012"></a><a name="b610071881012"></a>名称</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.2"><p id="p40119436"><a name="p40119436"></a><a name="p40119436"></a><strong id="b71471218131015"><a name="b71471218131015"></a><a name="b71471218131015"></a>描述</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.3"><p id="p28448916"><a name="p28448916"></a><a name="p28448916"></a><strong id="b7147418111013"><a name="b7147418111013"></a><a name="b7147418111013"></a>是否必选</strong></p>
    </th>
    <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.4"><p id="p22660844"><a name="p22660844"></a><a name="p22660844"></a><strong id="b17147191841019"><a name="b17147191841019"></a><a name="b17147191841019"></a>示例</strong></p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row23589052"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p31665069"><a name="p31665069"></a><a name="p31665069"></a>Content-Type</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p14733798"><a name="p14733798"></a><a name="p14733798"></a>发送的实体的MIME类型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p52587024"><a name="p52587024"></a><a name="p52587024"></a>是</p>
    </td>
    <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p31690579"><a name="p31690579"></a><a name="p31690579"></a>application/json</p>
    </td>
    </tr>
    </tbody>
    </table>

    请求内容示例如下：

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   示例代码中的斜体字需要替换为实际内容，详细情况请参见《统一身份认证服务API参考》。  
    >-   请求体中的regioncode，请参见[地区和终端节点](http://developer.huaweicloud.com/endpoint.html)。  

    ```
    { 
        "auth": { 
            "identity": { 
                "methods": [ 
                    "password" 
                ], 
                "password": { 
                    "user": { 
                        "name": "username", 
                        "password": "password", 
                        "domain": { 
                            "name": "domainname" 
                        } 
                    } 
                } 
            }, 
            "scope": { 
                "project": { 
                   "name": "regioncode" 
                 } 
            } 
        } 
    }
    ```

2.  <a name="li892493681217"></a>获取Token。

    请求响应成功后在响应消息头中包含的“X-Subject-Token”的值即为Token值。

    请参见《统一身份认证服务API参考》的“获取用户Token”章节。

3.  从Token的响应结构体中可以获取到对应的project\_id（部分URL需要填入project\_id）。Token响应结构体示例如下：

    ```
    { 
        "token": { 
            "expires_at": "2016-06-24T07:42:43.907000Z", 
            "issued_at": "2016-06-23T07:42:43.907000Z", 
            "methods": [ 
                "password" 
            ], 
            "project": { 
                "name": "projectname", 
                "id": "project_id", 
                "domain": { 
                    "name": "domainname", 
                    "id": "domainid", 
                    "xdomain_type": "xdomaintype", 
                    "xdomain_id": "xdomainid" 
                } 
            }, 
            "user": { 
                "domain": { 
                    "name": "domainname", 
                    "id": "domainid", 
                    "xdomain_type": "xdomaintype", 
                    "xdomain_id": "xdomainid" 
                }, 
                "id": "userid", 
                "name": "username" 
            }, 
            "catalog": [], 
            "roles": [ 
                { 
                    "name": "rolesname1", 
                    "id": "rolesid1" 
                }, 
                { 
                    "id": "rolesid2", 
                    "name": "rolesname2" 
                } 
            ] 
        } 
    }
    ```

4.  调用业务接口，在请求消息头中增加“X-Auth-Token”，“X-Auth-Token”的取值为[2.获取Token。](#li892493681217)中获取的Token。


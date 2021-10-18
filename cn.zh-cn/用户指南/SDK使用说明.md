# SDK使用说明<a name="drs_15_0006"></a>

数据订阅功能将数据库中关键业务的数据变化信息缓存并提供统一的SDK接口，方便下游业务订阅、获取、并消费。

在使用SDK消费之前，需要先在数据复制服务控制台[创建数据订阅任务](https://support.huaweicloud.com/qs-drs/drs_07_0006.html)。

当订阅任务创建完成后，使用SDK可以实时订阅订阅通道中的增量数据。目前：

1.  数据复制服务只提供JAVA版本SDK，[SDK下载地址](SDK下载地址.md)。
2.  一个订阅通道只能被一个SDK消费，如果启动多个SDK连接同一个数据订阅通道时，只能有一个SDK进程获取到数据变化信息。如果有多个下游SDK需要订阅同一个RDS的增量数据。那么需要为每个下游SDK创建一个数据订阅任务。
3.  一个下游SDK不可以订阅消费多个订阅任务。
4.  数据订阅成功后，如果不及时进行消费，新产生的数据最多保留3天。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>数据复制服务提供的JAVA版本SDK支持的开发环境为JDK1.6以上版本， 推荐使用JDK1.8版本。

## 网络类型<a name="section35314819381"></a>

目前仅支持VPC网络。

## SDK运行原理<a name="section20481840399"></a>

SDK的拉取和确认消息是两个异步的线程，拉取按照事务顺序拉取，两个线程分别独立并且遵循因果序。拉取到的消息会顺序的调用用户注册的notify函数，SDK保证每一条消息会推送一次，且只有一次。

## 导入SDK的jar包<a name="section5284144412437"></a>

SDK的jar包使用beta版本只支持通过lib直接导入， 暂时不支持maven中央仓库直接下载，后续提供maven依赖直接从中央仓库下载。

```
<dependency>
<groupId>com.huawei.hwclouds</groupId>
<artifactId>drs-subscribe-sdk</artifactId>
<version>1.0</version>
</dependency>
```

## 参数配置<a name="section746955283415"></a>

数据订阅过程中，部分参数会影响拉取数据的速度和间隔。

在启动SDK之前，您可以根据需要在“subscribe.properties“的配置文件中，对以下参数进行设置：

```
# 获取订阅数据初始延时
MESSAGE_DELAY_TIME = 1500000
# 获取订阅数据间隔时间
MESSAGE_PERIOD_TIME = 2000000
# 通知用户订阅数据到达初始延时
NOTIFY_DELAY_TIME = 2000
# 通知用户订阅数据间隔
NOTIFY_PERIOD_TIME = 1000
# 返回服务端ack消息初始延时
ACK_DELAY_TIME = 3000
# 返回服务端ack消息时间间隔
ACK_PERIOD_TIME = 5000
```

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   以上参数值为默认配置，您可以使用默认值，也可以根据实际情况自定义参数值。
>-   以上涉及到时间的单位均为微秒。

## 确认机制<a name="section35921612104518"></a>

SDK采用的是自动批量确认机制，不需要客户端程序调用确认函数，可以重复确认。

例如：客户端收到了5个batch的消息，但是服务端只收到了1，2，5三个batch的确认，因为客户端确认消息也是严格有序的，那么认为客户端已经消费到了1-5的消息，若客户端程序挂掉了，那么消费位点会从5的batch size开始。

## SDK使用模版<a name="section14870536164719"></a>

```
import com.huawei.hwclouds.drs.context.SubscribeContext;
import com.huawei.hwclouds.drs.message.ClusterMessage;
import com.huawei.hwclouds.drs.subscribe.ClusterListener;
import com.huawei.hwclouds.drs.subscribe.DefaultSubscribeClient;
import com.huawei.hwclouds.drs.subscribe.SubscribeClient;
import java.util.List;
public class MainClass {
public static void main(String[] args) throws Exception {
SubscribeContext context = new SubscribeContext();
//设置本云用户名称
context.setDomainName("username");
//设置本云用户密码
context.setPassword("userpassword");
//设置订阅通道的IP，即数据订阅页面的订阅实例IP
context.setIp("SubscribeChannelIp");
context.setUserId("userId");
SubscribeClient client =
DefaultSubscribeClient.getSubscribeClient(context);
ClusterListener clusterListener = new ClusterListener() {
@Override
//notify中定义客户端消费行为
public void notify(List<ClusterMessage> var1) throws Exception {
for (ClusterMessage message : var1) {
System.out.println("Message is " + message.toString());
}
}
};
client.addClusterListener(clusterListener);
client.start();
}
}
```


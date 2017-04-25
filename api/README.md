# API部分

## MQTT协议通信规约

本系统使用[EMQ](http://emqtt.com/)作为MQTT消息服务器

### 设备端

#### 连接到MQTT服务器

MQTT服务器可以通过TCP或TLS连接。

以设备客户端的身份连接到MQTT服务之前，必须设置MQTT连接选项。

clientID的格式为`d:<orgid>:<type-id>:<divice-mac>`

其中orgid指明了隶属于哪个应用

type-id用于标识硬件类型

divice-mac使用硬件mac地址（不带任何符号）表示

如果使用TLS，应该将协议属性设置为TLSv1.2，否则可能出现连接不上服务器的情况。

- MQTT最低版本建议是3.1，推荐使用MQTT3.1.1

#### 发布事件

可以通过这种形式发送各种事件主题：`iot/id/<clientID>/evt/<event-id>/fmt/<format>`

设置`<event-id>`可以将不同的事件类型分类，可以自己定义事件值。`<format>`设置为json。消息应编码成JSON格式，它必须包含单个名为"d"的顶级属性。

```json
{
    "d":{
        "count":2,
        "a":[
            {
                "type":"t",
                "v":20
            },
            {
                "type":"h",
                "v":42
            }
        ]
    }
}
```

#### 发布系统事件

~~当设备上线或执行任何系统操作时，应主动向服务器上报消息~~

~~上报的主题应为：`iot/type/<type-id>/id/<clientID>/mon`~~

具体参考各平台MQTT规范

如使用自有服务器，EMQ直接$SYS系统主题

#### 订阅命令

订阅命令的Topic应为以下格式：`iot/id/<clientID>/cmd/<cmd-type>/fmt/<format>`

设置`<cmd-type>`可将不同的类型分类，可以自己定义事件值。也可以使用"+"作为通配符来设置`cmd-type`，这样可以订阅各种类型命令。 `<format>`设置为json。

```json
{
  "cmd":"open a light"
}
```
### 服务端
#### 连接到MQTT服务器
IoT 服务的服务端与设备端相同，但 MQTT 连接选项格式之间存在一些差异：

clientID的格式为`d:<orgid>:<server-id>`

其中orgid指明了隶属于哪个应用

server-id是为服务设置的唯一id
#### 订阅命令
服务端可以订阅两种类型的事件：1.来自设备端的消息 2.系统生成的连接监视器消息
- 订阅设备端事件的主题应为以下格式：`iot/id/+/evt/<event-id>/fmt/<format>`
  使用+作为通配符可以订阅所有id的主题
- 订阅系统事件的主题应为以下格式：`iot/type/<type-id>/id/+/mon`
  type-id表明消息类型
  通过订阅系统事件，每次设备与MQTT服务器连接或断开，都可收到消息
#### 发布命令
发布命令的主题应为以下格式：`iot/id/<clientID>/cmd/<cmd-type>/fmt/<format>`
它应与设备端订阅主题一致。



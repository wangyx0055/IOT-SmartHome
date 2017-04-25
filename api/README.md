# API部分

## MQTT协议规约

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

可以通过这种形式发送各种事件主题：`iot/evt/<event-id>/fmt/<format>`

设置`<event-id>`可以将不同的事件类型分类，可以自己定义事件值。`<format>`设置为json。消息应编码成JSON格式，它必须包含单个名为"d"的顶级属性。

```json
{
  "d":{
    "count":2,
    "a":[
      "type":"t",
      "v":20.3
   	],[
      "type":"h",
      "v":50
    ]
  }
}
```

#### 订阅命令

订阅命令的Topic应为以下格式：`iot/cmd/<cmd-type>/fmt/<format>`

设置`<cmd-type>`可将不同的类型分类，可以自己定义事件值。也可以使用"+"作为通配符来设置`cmd-type`，这样可以订阅各种类型命令。 `<format>`设置为json。

```json
{
  "cmd":"open a light"
}
```


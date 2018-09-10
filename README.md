# 毫米智家平台接入文档

### 1. 接入地址

```
https://ai.myroome.com
```

### 2. 请求方式

```
POST
```

### 3. 签名配置

向服务器发送请求的客户端均会分配唯一的Token值，用于识别与校验数据来源。

发送请求时，需携带的header参数如下所示:

| 参数 | 描述 |
| :--- | :--- |
| signature | 签名。signature结合了分配的token参数、from来源参数，和请求中的ts时间戳参数。 |
| from | jinpai |
| ts | 时间戳。精确到秒。 |
| rand | 随机整数值 |

**签名的计算方法**

```
signature = sha1(from + rand + token + ts)
```

### 4. 请求示例
示例 token = hwSsZbfit4VGiIPBOVAgV1ktCBzx0t
```conf
POST https://ai.myroome.com HTTP/1.1
Content-Length：ContentLength
Content-Type: Application/json
hm-from: jinpai
hm-ts: 1234567890
hm-rand: 98765432
hm-signature: 6927c3c702e8593404bf6bf283583d08d52c6f4e

{"a":"upload","deviceCode":"0600000143218765","type":"collection","attr":"light", "value":87, "ts":1234567890}
```

### 5. 响应内容
 ```
 {"code":0,"msg":"ok"}
 ```

### 6. 全局返回状态码

| 返回码 | 说明 |
| :--- | :--- |
| -1 | 系统繁忙，此时请稍候再试 |
| 0 | 请求成功 |
| 1001 | 不合法的客户端 |
| 1002 | 请求校验失败 |
| 1003 | 不存在的设备ID |
| 1004 | 不合法的参数 |
| 1005 | 需要用POST请求 |
| 1006 | 需要用HTTPS请求 |
| 1007 | 消息内容为空 |



### 7. "type" 类型

| type | 说明 |
| :--- | :--- |
| ac | Auto Control, 自动控制 |
| mc | Manual Control, 手动控制 |
| collection | 自动上传 |
| app | APP 控制 |

### 8. "attr" 属性名称

| attr | 说明 |
| :--- | :--- |
| light | 光线感应 |
| pir | 红外感应 |
| smoke | 烟雾感应 |
| temperature | 温度 |
| humidity | 湿度 |

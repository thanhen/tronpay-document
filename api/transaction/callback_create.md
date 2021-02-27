## 回调类地址生成

### 说明

生成对应币种的收款地址，如果有用户向该地址付款，则系统会向商户请求接口时指定的回调地址发送通知。

> 该接口生成的地址可重复使用。如地址在不同的时间接收到多笔付款，则对于每一笔收款，系统都会发送通知消息。

### 接口地址

```bash
POST https://www.tronapi.com/api/payment/get_callback_address
```

### 接口参数

参数名 | 含义 |  验证 | 类型 | 说明
-|-|-|-|-
public_key | public key | 必填 | string(64) | 商户 public key。
coin_code | 地址关联的币种 | 必填 | string(16) | 如需要生成 USDT.TRC20 类的地址，则传入“USDT.TRC20”。完整的币种编码列表可参考：[常量参考](/api/asset/constant.md)
notify_url | 接收到付款后的通知地址 | 必填 | string(128) | 如地址接收到付款，系统会自动发送一个 post 消息到这个地址。该参数不需要 urlencode。例如：http://www.xxx.com/pay_notify。
signature | 签名串 | 必填 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(coin_code + notify_url + public key + private key))。

### 接口返回

参数名 | 含义 | 类型 | 说明
-|-|-|-
token | 官方 token | string(32) | 官方 token。
coin_code | 地址币种 | string(16) | 地址币种，原数据返回
address | 币种地址 | string(64) | 接收用户付款的数据货币地址，与 coin_code 对应。
qrcode_url | 收款码地址 | string(128) | 币种对应的收款码地址。
signature | 签名串 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(token + coin_code + address + qrcode_url + private key))。

#### 返回示例

```javascript
{
    code: 200,
    content: {
        token: 'cah23b2vh8chj5y1vb9hcvmj6f1hpw45',
        coin_code: 'FAU',
        address: 'TJ9VJZtHFYANwRzu3NBfgPSXobTih8HmNp',
        notify_url: 'https://www.tronapi.com/test/callback/notify',
        qrcode_url: 'https://www.tronapi.com/api/payment/qrcode/callback?token=cah23b2vh8chj5y1vb9hcvmj6f1hpw45',
        signature: 'a9a84b2e9ea225a71fa58202afb09822'
    }
}
```
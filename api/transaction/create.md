## 交易创建

### 说明

用于生成指定数字货币的支付数据，包括收款地址、金额、二维码等。商户可选择直接跳转至官方的收银台供用户支付，也可以使用数据自定义收银台。在用户支付成功后，系统将即时进行回调通知。

### 接口地址

```bash
POST https://www.tronapi.com/api/payment/create_transaction
```

### 接口参数

参数名 | 含义 | 验证 | 类型 | 说明
-|-|-|-|-
public_key | public key	| 必填 | string(64)	| 商户 public key。
amount | 订单金额 | 必填 | float | 精确到小数点后2位。
currency | 订单货币 | 必填 | string(3) | 订单货币单位。如货币单位为人民币，则传入“CNY”。完整的货币编码列表可参考：[常量参考](/api/asset/constant.md)
coin_code | 支付币种 | 必填 | string(16) | 支付币种。如 USDT.TRC20 支付，则传入“USDT.TRC20”。完整的币种编码列表可参考：[常量参考](/api/asset/constant.md)
notify_url | 支付成功后消息通知地址 | 必填 | string(128) | 用户支付成功后，系统会自动发送一个 post 消息到这个地址。该参数不需要 urlencode。例如：http://www.xxx.com/pay_notify。
redirect_url | 支付成功后同步跳转地址 | 选填 | string(128) | 用户支付成功后，系统会自动跳转到这个地址。该参数不要 urlencode。例如：http://www.xxx.com/pay_return。
order_id | 自定义订单号 | 必填 | string(32) | 系统在通知商户接口时，会带上这个参数。例：201710192541。
customer_id | 自定义用户编号 | 必填 | string(32) | 该参数会显示在商户后台的订单列表中，方便商户对用户支付进行对账。可以为用户名，也可以为数据库中的用户编号。例：xxx@aaa.com，xxx等。
product_name | 商品名称 | 选填 | string(32) | 该参数会显示在商户后台的订单列表中，方便订单归类。
lang | 收银台多语言 | 选填 | string(10) | 收银台多语言编码。如简体中文，则传入“zh-CN”。默认为简体中文。完整的多语言支持列表可参考：[常量参考](/api/asset/constant.md)
signature | 签名串 | 必填 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(amount + currency + coin_code + order_id + product_name + customer_id + notify_url + redirect_url + public key + private key))。

> 用户最终的支付金额，由订单金额 + 订单货币单位 + 支付币种按照实时行情转换而来。

### 接口返回

参数名 | 含义 | 类型 | 说明
-|-|-|-
token | 官方订单号 | string(32) | 可通过该字段，调用支付状态查询接口，核实用户是否支付成功。
amount | 订单金额 | float | 订单金额，原数据返回
currency | 订单货币单位 | string(3) | 订单货币单位，原数据返回
coin_code | 支付币种 | string(16) | 支付币种，原数据返回
coin_amount | 用户支付金额 | float | 用户最终支付金额，由订单金额 + 订单货币单位 + 支付币种按照实时行情转换而来。
address | 币种收款地址 | string(64) | 接收用户支付的数据货币地址，与支付币种对应。
cashier_url | 官方收银台地址 | string(128) | 官方收银台 url 地址，商户可直接跳转到该地址供用户支付。
qrcode_url | 收款码地址 | string(128) | 币种对应的收款码地址。
timeout | 订单过期时间 | int | 支付过期时间，单位秒
signature | 签名串 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(token + amount + currency + coin_code + coin_amount + address + timeout + cashier_url + qrcode_url + private key))。

### 返回示例

```javascript
{
    code: 200,
    content: {
        token: '3a4kah5f7r13hr36jkbsg88v36c2hn8w',
        amount: '100.00',
        currency: 'CNY',
        coin_code: 'FAU',
        coin_amount: '100.00',
        address: 'TAUPAXKmsBQ7Ns62zRgPAdq3AS1j1TgHCB',
        timeout: 28800,
        cashier_url: 'https://www.tronapi.com/api/payment/cashier?token=3a4kah5f7r13hr36jkbsg88v36c2hn8w&locale=zh-CN',
        qrcode_url: 'https://www.tronapi.com/api/payment/qrcode?token=3a4kah5f7r13hr36jkbsg88v36c2hn8w',
        signature: '9e65d44ec49630950ba2008f3c751691'
    }
}
```
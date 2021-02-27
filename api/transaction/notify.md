## 交易通知

### 说明

用户支付成功后，系统会自动向商户发起交易请求时指定的回调地址（```notify_url```），发送通知消息，告知该笔交易已支付成功。

### 通知地址

```bash
POST notify_url（商户在交易创建接口中指定）
```

### 通知参数
参数名 | 含义 | 类型 | 说明
-|-|-|-
order_id | 自定义订单号 | string(32) | 商户自定义订单号，原样返回。
amount | 订单金额 | float | 商户在发起交易接口指定的订单金额。
currency | 订单货币单位 | string(3) | 商户在发起交易接口指定的订单货币单位。
coin_code | 支付币种 | string(10) | 商户在发起交易接口指定的订单支付币种
coin_amount | 用户支付金额 | float | 用户最终支付的金额
signature | 签名串 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(order_id + amount + currency + coin_code + coin_amount + private key))。

商户在收到通知信息后，可返回以下内容，告知已收到回调通知：

```javascript
{
    code: 200,
    content: "ok"
}
```
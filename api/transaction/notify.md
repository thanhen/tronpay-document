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
token | 官方订单号 | string(32) | 可通过该字段，调用支付状态查询接口，核实用户是否支付成功。
order_id | 自定义订单号 | string(32) | 商户自定义订单号，原样返回。
amount | 订单金额 | string(12) | 商户在发起交易接口指定的订单金额。
currency | 订单货币单位 | string(3) | 商户在发起交易接口指定的订单货币单位。
coin_code | 支付币种 | string(10) | 商户在发起交易接口指定的订单支付币种
coin_amount | 用户支付金额 | string(12) | 用户最终支付的金额
txn_hash | 交易 hash | string(128) | 区块链交易 hash。商户可打开区块链浏览器查询交易详情。
signature | 签名串 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(token + order_id + amount + currency + coin_code + coin_amount + txn_hash + private key))。

#### 通知示例
```javascript
{
    code: 200,
    content: {
        token: '81iy0b71fxpu8g643s7v758uz8161v7d',
        order_id: '8iGDGAjsZxhEaKu9',
        amount: '120.00',
        currency: 'CNY',
        coin_code: 'FAU',
        coin_amount: '18.32',
        txn_hash: '99ece46e715b9ea19e019285ae4561c757c271e91dafc47a33b1a7a461d017b8',
        signature: 'cf3f327aaaa4b9e24c338b6827a68fde'
    }
}
```

商户在收到通知信息后，可返回以下内容，告知已收到回调通知：

```javascript
{
    code: 200,
    content: "ok"
}
```
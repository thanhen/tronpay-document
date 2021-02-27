## 回调类地址通知

### 说明

回调类地址接收到用户的付款后，系统会自动向商户指定的回调地址（```notify_url```），发送通知信息，告知地址接收到新的付款。

### 通知地址

```bash
POST notify_url（商户在回调类地址生成接口中指定）
```

### 通知参数

参数名 | 含义 | 类型 | 说明
-|-|-|-
coin_code | 币种 | string(16) | 地址对应的币种
received_amount | 接收金额 | float | 接收到的用户付款的金额
address | 接收地址 | string(64) | 接收到用户付款的地址
from | 发送地址 | string(64) | 接收到付款的发送地址
signature | 签名串 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(coin_code + received_amount + address + from + private key))。

### 通知示例

```javascript
{
    code: 200,
    content: {
        coin_code: 'FAU',
        received_amount: '10.00',
        address: 'TUM5LLTFNQDqaTpDwA9fV9PKrRv5NBpkqZ',
        from: 'TTbVyNMZvSVUHc6AKBA8iGkcS1TE2hRyEX',
        signature: 'fd87197bc3272a22a7aa0eb3fa423daa'
    }
}
```
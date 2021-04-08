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
token | 官方交易号 | string(32) | 官方为每一笔收款生成的唯一标识
coin_code | 币种 | string(16) | 地址对应的币种
received_amount | 接收金额 | float | 接收到的用户付款的金额
address | 接收地址 | string(64) | 接收到用户付款的地址
from | 发送地址 | string(64) | 接收到付款的发送地址
txn_hash | 交易 hash | string(128) | 区块链交易 hash。商户可打开区块链浏览器查询交易详情。
signature | 签名串 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(token + coin_code + received_amount + address + from + txn_hash + private key))。

### 通知示例

```javascript
{
    code: 200,
    content: {
        token: 'z5btyutpfb2n3n0bfawtj7ek057w7473',
        coin_code: 'FAU',
        received_amount: '10.00',
        address: 'TSmmqAqwQbveZMEgCWT5V2kbtttX5H9ZRe',
        from: 'TCZK8dZYj1crg8Xjs7tYxk8coqX9ybYWH8',
        txn_hash: '4bf18c804643aa665a16454ef1f1b7f1dae6790e0b0cf59d3b75643d8afffe90',
        signature: 'd7ef7bd990b55ac82af76e0c2e4d6b87'
    }
}
```
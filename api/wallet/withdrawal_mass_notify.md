## 批量提现到账通知

### 说明

商户的批量提现申请到账后，系统会自动向商户指定的回调地址（```notify_url```）发送通知消息，告知提现申请已处理完毕。

### 通知地址

```bash
POST notify_url（商户在批量提现创建接口中指定）
```

### 通知参数

参数名 | 含义 | 类型 | 说明
-|-|-|-
token | 官方 token | string(32) | 官方 token。
txn_hash | 交易 hash | string(128) | 提现操作的转账 hash。商户可打开区块链浏览器查询交易详情。
coin_code | 钱包币种 | string(16) | 钱包币种，原样返回
count | 提现数量 | int | 批量提现的数量。
rate | 商户费率 | float | 商户的交易费率。
remark | 备注信息 | string(128) | 提现备注信息，原样返回。
signature | 签名串 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(token + txn_hash + coin_code + count + rate + remark + private key))。

### 通知示例

```javascript
{
    code: 200,
    content: {
        token: '2zuu4rf9if7mk6z236tmc6h6rp63hh8h',
        txn_hash: '0xa52239ba2dc97bc4ad36056936aba4fedd2325dd69691138dc896865c795efec',
        count: 2,
        rate: 0.01,
        remark: '接口提现申请',
        signature: 'abe962d3ac6304e78eb2ba3caea170c0'
    }
}
```
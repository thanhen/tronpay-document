## 提现到账通知

### 说明

商户的提现申请到账后，系统会自动向商户指定的回调地址（```notify_url```）发送通知信息，告知提现申请已处理完毕。

### 通知地址

```bash
POST notify_url（商户在提现创建接口中指定）
```

### 通知参数

参数名 | 含义 | 类型 | 说明
-|-|-|-
token | 官方 token | string(32) | 官方 token。
txn_hash | 交易 hash | string(128) | 提现操作的转账 hash。商户可打开区块链浏览器查询交易详情。
coin_code | 钱包币种 | string(16) | 钱包币种，原样返回
address | 接收地址 | string(64) | 提现接收地址（原样返回）
amount_apply | 申请金额 | float | 提现申请金额。
amount_received | 到账金额 | float | 提现到账金额
rate | 商户费率 | float | 商户的费率
remark | 备注信息 | string(128) | 提现备注信息，原样返回。
signature | 签名串 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(token + txn_hash + coin_code + address + amount_apply + amount_received + rate + remark + private key))。

### 通知示例

```javascript
{
    code: 200,
    content: {
        token: 'yb5dkhxae1701ed570tu9gpj71w3q54t',
        txn_hash: '0xeb2e4ad7ce37c59f84d1b391ed2512d264262c12b7fc5eb596bd9807d5489c3a',
        coin_code: 'FAU',
        address: 'TYvLybkRVD1K8MMQZfcMSUhBENFwxzFn8o',
        amount_apply: '100.00',
        amount_received: '99.00',
        rate: 0.01,
        remark: '接口提现申请',
        signature: '2bdd65aed9a42d43c478897421d623ed'
    }
}
```
    
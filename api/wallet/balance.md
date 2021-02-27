## 查询钱包余额

### 说明

商户可调用该接口，查询钱包及余额信息。

### 接口地址

```bash
GET https://www.tronapi.com/api/wallet/get_balance
```

### 接口参数

参数名 | 含义 | 验证 | 类型 | 说明
-|-|-|-|-
public_key | public key | 必填 | string(64) | 商户 public key。
signature | 签名串 | 必填 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(public key + private key))。

### 返回示例

```javascript
{
    "code": 200,
    "content": [{
        "coin_code": "FAU",
        "balance": "1667.25"
    }, {
        "coin_code": "USDT.TRC20",
        "balance": "222.32"
    }]
}
```
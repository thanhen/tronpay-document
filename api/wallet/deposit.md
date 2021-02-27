## 生成收款地址

### 说明

商户可调用该接口，生成钱包对应的收款地址。

> 该接口仅用于钱包常规收款，不具有通知回调功能。

### 接口地址

```bash
GET https://www.tronapi.com/api/wallet/get_deposit_address
```

参数名 | 含义 | 验证 | 类型 | 说明
-|-|-|-|-
public_key | public key | 必填 | string(64) | 商户 public key。
coin_code | 币种 | 必填 | string(16) | 钱包对应的币种编码。如 USDT.TRC20
signature | 签名串 | 必填 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(coin_code + public key + private key))。

### 接口返回

参数名 | 含义 | 类型 | 说明
-|-|-|-|-
token | 官方 token | string(32) | 官方 token。
coin_code | 地址币种 | string(16) | 地址币种，原数据返回
balance | 地址余额 | float | 地址余额，新生成的地址余额为 0。
address | 币种地址 | string(64) | 币种对应的地址。
qrcode_url | 收款码地址 | string(128) | 币种地址对应的收款码地址。
signature | 签名串 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(token + coin_code + address + balance + qrcode_url + private key))。

#### 返回示例

```javascript
{
    "code": 200,
    "content": {
        "token": "86r50ra7nbt7g7h7xg01a5gji8296ms1",
        "coin_code": "FAU",
        "address": "TNCvXX8mUEm6QrCm2a129P9EbDSKS2J2BK",
        "balance": 0,
        "qrcode_url": "https://www.tronapi.com/api/wallet/qrcode/deposit?token=86r50ra7nbt7g7h7xg01a5gji8296ms1",
        "signature": "1976b74ff33de5cffecfd1c089e249f6"
    }
}
```
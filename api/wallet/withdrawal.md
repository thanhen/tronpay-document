## 申请提现

### 说明

商户可调用该接口，发起钱包提现申请。

### 接口地址

```bash
POST https://www.tronapi.com/api/wallet/create_withdrawal
```

### 接口参数

参数名 | 含义 | 验证 | 类型 | 说明
-|-|-|-|-
public_key | public key | 必填 | string(64) | 商户 public key。
coin_code | 钱包币种 | 必填 | string(16) | 如 USDT.TRC20。完整的币种编码列表可参考：[常量参考](/api/asset/constant.md)
coin_amount | 提现金额 | 必填 | float | 精确到小数点后2位。
address | 提现地址 | 必填 | string(64) | 提现到账的地址。
notify_url | 提现成功后通知地址 | 必填 | string(128) | 提现处理成功后，系统会自动发送一个 post 消息到这个地址。该参数不需要 urlencode。例如：http://www.xxx.com/pay_notify。
remark | 备注信息 | 选填 | string(128) | 提现备注信息。
signature | 签名串 | 必填 | string(32) | 安全校验签名串。

> signature 的生成规则为：toLowerCase(md5(coin_code + coin_amount + address + notify_url + remark + public key + private key))。

### 接口返回

参数名 | 含义 | 类型 | 说明
-|-|-|-
token | 官方 token | string(32) | 官方 token。
coin_code | 钱包币种 | string(16) | 钱包币种，原样返回。
status | 提现状态 | int | status = 0: 提现申请仍需商户安全验证。status = 1: 商户未开启提现安全验证，已进入系统处理流程。
signature | 签名串 | string(32) | 安全校验签名串。
说明

signature 的生成规则为：toLowerCase(md5(token + coin_code + status + private key))。

#### 返回示例

```javascript
{
    code: 200,
    content: {
        token: '2zuu4rf9if7mk6z236tmc6h6rp63hh8h',
        coin_code: 'FAU',
        status: 1,
        signature: 'db799f1df20d4925fbdfdbfe07cd7693'
    }
}
```
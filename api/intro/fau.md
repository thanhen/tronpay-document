## 关于测试币

为方便商户对接及开发，系统提供测试币（币种编码：FAU）的联调功能。对于通过测试币发起的接口请求，系统会自动支付并触发回调（如果接口有指定回调地址的话），不需要商户进行支付测试。

目前官方使用的测试币种信息如下：

- 币种名称：FAU
- 测试网络：shasta
- 合约地址：TW75reLDyBLu7v3uY8ED7SALek9s4Kq6D4

### 场景
调用以下接口会触发测试币的自动支付功能：

#### 交易
- 交易创建：/api/payment/create_transaction
- 回调类地址生成：/api/payment/get_callback_address

#### 钱包
- 生成收款地址：/api/wallet/get_deposit_address

> 目前测试币种自动支付的金额为：10 FAU。
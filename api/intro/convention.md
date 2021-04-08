## 接口约定

### 编码约定

数据编码统一为 utf-8。

### public key & private key

接口文档中提到的 ```public key``` & ```private key```，都是指商户 ```public key``` & ```private key```，可在网站的商户后台查看。

### 字段选填

对于接口参数标记为 ```选填``` 的字段，可传入具体的值或者空字符串。

### signature

为保障接口安全，系统端会对接收到的所有数据，使用 ```signature``` 匹配校验，防止数据被非法篡改。

> 对于 signature 的拼接规则，举个例子：如某个接口需要提交数据 public_key 和 coin_code 两个字段，且 public_key 值为 123456，coin_code 值为 FAU。根据 signature 的生成规则：toLowerCase(md5(public_key + coin_code))，则最终提交的 signature 数据为：toLowerCase(md5('123456FAU')) = 23032450e6d86f359819f017a94253a9。

### 数据提交
对于有数据提交的接口，统一使用 ```POST``` 的方式（查询接口除外）。相关 http 请求头的 content-type 字段为：
```bash
application/x-www-form-urlencoded
```
    
### 数据返回

对于有数据返回的接口，格式为 ```json```，结构如下:
```javascript
{
    code: 200,
    content: {}
}
```

> 上述数据返回结构中，当 code = 200 时代表成功状态，content 为具体的数据内容。否则为失败状态，content 为相关的错误信息。

### 区块链浏览器

> 如接口有返回 txn_hash 字段，商户可前往以下波场区块链浏览器，查询交易详细信息。

TRON 主网络：[https://tronscan.io](https://tronscan.io)

TRON 测试网：[https://shasta.tronscan.io](https://shasta.tronscan.io)
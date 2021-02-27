## 交易状态查询

### 说明

供商户主动查询交易状态。多用于商户自定义收银台的情况。

### 接口地址

```bash
GET https://www.tronapi.com/api/payment/query
```

### 接口参数
参数名 | 含义 | 类型 | 说明
-|-|-|-
token | 官方 token | string(32) | 该参数可在交易创建接口的返回数据中获取。

### 接口返回

```javascript   
{
    code: 200,
    content: "订单已支付"
}
```

> 上述接口返回内容中，当 ```code``` 值为 ```200``` 时，代表订单已支付成功。
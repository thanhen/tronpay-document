## 交易官方收银台

### 说明

商户调用 交易创建（```/api/payment/create_transaction```） 接口后，会返回如下数据：
```javascript
{
    code: 200,
    content: {
        token: '3a4kah5f7r13hr36jkbsg88v36c2hn8w',
        amount: '100.00',
        currency: 'CNY',
        coin_code: 'FAU',
        coin_amount: '100.00',
        address: 'TZCAMAFjtfUQ4KRVttuqcx3vFuXsYzRUcY',
        timeout: 28800,
        cashier_url: 'https://www.tronapi.com/api/payment/cashier?token=3a4kah5f7r13hr36jkbsg88v36c2hn8w&locale=zh-CN',
        qrcode_url: 'https://www.tronapi.com/api/payment/qrcode?token=3a4kah5f7r13hr36jkbsg88v36c2hn8w',
        signature: '9e65d44ec49630950ba2008f3c751691'
    }
}  
```
    
商户可直接从上述返回数据中，取出 ```cashier_url``` 字段，然后跳转至该地址，供用户支付。

### 收银台

跳转至 ```cashier_url``` 后，页面显示如下：

<img src="https://tronapi.com/public/home/img/pay-screen.png" width="360" alt="订单页截图">

> 对于测试币种（FAU），系统将会自动支付并触发回调。请勿扫码付款。

### 付款成功后跳转

用户在收银台支付成功后，系统会自动通知商户在创建订单时指定的回调地址（```notify_url```）。在间隔大概1秒钟后，页面会自动跳转至商户在创建订单时指定的跳转地址（```redirect_url```）。

### 跳转地址
```bash
GET redirect_url（商户在交易创建接口中指定）
```

### 跳转参数
参数名 | 含义 | 类型 | 说明
-|-|-|-
order_id | 商户自定义订单号 | string(32) | 商户可以通过 ```order_id``` 参数，查询本地数据库，确认用户是否支付成功，并给出相应的页面展示。

> 请不要将此跳转作为用户支付成功的判断条件，此行为极不安全。请根据支付成功的通知消息是否送达，来判断用户是否支付成功。
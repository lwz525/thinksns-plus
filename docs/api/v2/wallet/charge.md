# 凭据

- [凭据获取](#凭据获取)
    - [凭据取回](#凭据取回)
- 凭据列表

## 凭据获取

凭据获取用于获取用户订单凭据详细信息，其中还包含凭据取回。

```
GET /wallet/charges/{charge}
```
`{charge}` 为创建订单或者列表给出的凭据 ID

##### Header

```
Status: 200 OK
```

##### Body

```json5
{
  "id": 1, // 凭据ID
  "user_id": 1, // 凭据对应用户（不一定有，该凭据对应的用户，客户端几乎用不到的。）
  "channel": "alipay", // 支付频道
  "account": "alipay_account", // 账户，如果是系统内购买，例如购买一张图片，会和频道对应，然后给出不同的值，例如支付宝给出的是支付宝账号。微信给出的是 open_id、银联给出的是银行卡号。channel 还有我们系统内置类型，例如 user 可能对应的就是用户ID（例如转账）
  "charge_id": "ch_vvP4u1H0evPGqn9qn5mPCGS4",
  "action": 1,
  "amount": 100,
  "currency": "cny",
  "subject": "余额充值",
  "body": "账户余额充值",
  "transaction_no": "2017060879918233",
  "status": 1,
  "created_at": "2017-06-07 06:32:28",
  "updated_at": "2017-06-08 06:46:23",
  "deleted_at": null
}
```

#### 凭据取回

凭据取回，可以理解成第三发验证获取，服务器会调用第三发接口取回凭据状态，重置凭据状态，并充值用户余额。

```
GET /wallet/charges/{charge}?mode=retrieve
```

响应数据和「凭据获取」相同

> 该模式只会生效一次，之后传递则不会生效，参数不要乱传，如果非支付订单传递该参数，则会抛出 422 验证异常。


## 凭据列表
# V2Board 最全接口文档（1.6.0）

> 感谢 v2board 提供的开源项目！ 完整api请查阅开源项目 : [v2board](https://github.com/v2board/v2board)

> 本文档仅适用于1.6.0版本，1.6.1由于改动过大会等稳定后专门提出来写

**所有的GET 请求 均需要传入请求头 Authorization 值为 auth_data**

## 目录

### Passport

| URL                            | 请求   | 描述                                |
|--------------------------------|------|-----------------------------------|
| /passport/comm/config          | GET  | [获取配置](#1获取配置)       |
| /passport/auth/check           | GET  | [登入校验](#2登入校验)       |
| /passport/auth/login           | POST | [登入账号](#3登入账号)       |
| /passport/comm/sendEmailVerify | POST | [发送邮箱验证码](#4发送邮箱验证码) |
| /passport/auth/register        | POST | [注册账号](#5注册账号)       |
| /passport/auth/forget          | POST | [重置密码](#6重置密码)       |

### User

| URL                   | 请求   | 描述                         |
|-----------------------|------|----------------------------|
| /user/logout          | GET  | [登出](#1登出)        |
| /user/info            | GET  | [账号信息](#2账号信息)    |
| /user/getSubscribe    | GET  | [订阅信息](#3订阅信息)    |
| /user/resetSecurity   | GET  | [重置订阅链接](#重置订阅链接) |
| /user/getStat         | GET  | [代办事项](#5代办事项)    |
| /user/changePassword  | POST | [修改密码](#6修改密码)    |
| /user/update          | POST | [通知状态](#7通知状态)    |
| /user/transfer        | POST | [佣金划转](#8佣金划转)    |

### Plan

| URL              | 请求  | 描述                          |
|------------------|-----|-----------------------------|
| /user/plan/fetch | GET | [订阅商店列表](#1订阅商店列表) |

### Order

| URL                           | 请求   | 描述                       |
|-------------------------------|------|--------------------------|
| /user/order/fetch             | GET  | [订单列表](#1订单列表) |
| /user/order/getPaymentMethod  | GET  | [支付方式](#2支付方式) |
| /user/order/details?trade_no= | GET  | [订单详情](#3订单详情) |
| /user/order/check?trade_no=   | GET  | [订单状态](#4订单状态) |
| /user/order/save              | POST | [创建订单](#5创建订单) |
| /user/order/checkout          | POST | [结算订单](#6结算订单) |
| /user/order/cancel            | POST | [关闭订单](#7关闭订单) |

### Invite

| URL                  | 请求  | 描述                          |
|----------------------|-----|-----------------------------|
| /user/invite/fetch   | GET | [邀请码管理](#1邀请码管理) |
| /user/invite/save    | GET | [生成邀请码](#2生成邀请码) |
| /user/invite/details | GET | [邀请明细](#3邀请明细)   |

### Notice

| URL                  | 请求  | 描述                        |
|----------------------|-----|---------------------------|
| /user/notice/fetch   | GET | [公告信息](#1公告信息) |

### Ticket
| URL                | 请求 | 描述                   |
| ------------------ | ---- | ---------------------- |
| /user/ticket/fetch | GET  | [工单列表](#1工单列表) |
| /user/ticket/save  | POST | [创建工单](#2创建工单) |
| /user/ticket/reply | POST | [回复工单](#3回复工单) |
| /user/ticket/close | POST | [关闭工单](#4关闭工单) |

___

## Passport

### 1.获取配置

> `GET` /passport/comm/config

- 请求参数
  `null`

- 成功返回示例 `json`

```json
{
  "data": {
    "tos_url": "https://xxx.com",
    "is_email_verify": 0,
    "is_invite_force": 0,
    "email_whitelist_suffix": 0,
    "is_recaptcha": 0,
    "recaptcha_site_key": "xxx",
    "app_description": "Hallo!",
    "app_url": "https://xxx.com"
  }
}
```

| 参数名                    | 类型                 | 描述      |
|------------------------|--------------------|---------|
| tos_url                | string             | 条款链接    |
| is_email_verify        | number             | 邮件验证    |
| is_invite_force        | number             | 强制邀请注册  |
| email_whitelist_suffix | number or string[] | 邮件白名单后缀 |
| is_recaptcha           | number             | 人机验证    |
| recaptcha_site_key     | string             | 人机验证校验码 |
| app_description        | string             | 站点说明    |
| app_url                | string             | 站点地址    |

### 2.登入校验

> `GET` /passport/auth/check

- 请求参数
  `null`

- 成功返回示例 `json`

```json
{
  "data": {
    "is_login": false
  }
}
```

| 参数名      | 类型      | 描述   |
|----------|---------|------|
| is_login | boolean | 是否登入 |

### 3.登入账号

> `POST` /passport/auth/login

- 请求参数 `json`

```json
 {
  "email": "xxxx@xx.com",
  "password": "1234567890"
}
```

| 参数名      | 类型     | 必填  | 描述   |
|----------|--------|-----|------|
| email    | string | ✔︎  | 邮箱地址 |
| password | string | ✔︎  | 密码   |

- 成功返回示例 `json`

```json
{
  "data": {
    "token": "xxx",
    "auth_data": "xxx"
  }
}
```

| 参数名       | 类型     | 描述            |
|-----------|--------|---------------|
| token     | string | 用户 token      |
| auth_data | string | base64(邮箱:密码) |

### 4.发送邮箱验证码

> `POST` /passport/comm/sendEmailVerify

- 请求参数 `json`

```json
 {
  "email": "xxxx@xx.com"
}
```

| 参数名   | 类型     | 必填  | 描述   |
|-------|--------|-----|------|
| email | string | ✔︎  | 邮箱地址 |

- 成功返回示例 `json`

```json
{
  "data": true
}
```

| 参数名  | 类型      | 描述     |
|------|---------|--------|
| data | boolean | 是否发送成功 |

### 5.注册账号

> `POST` /passport/auth/register

- 请求参数 `json`

```json
 {
  "email": "xxxx@xx.com",
  "password": "123456789",
  "email_code": 333333,
  "invite_code": "",
  "recaptcha_data": ""
}
```

| 参数名            | 类型     | 必填  | 描述     |
|----------------|--------|-----|--------|
| email          | string | ✔︎  | 邮箱地址   |
| password       | string | ✔︎  | 密码     |
| email_code     | number | ✖︎  | 邮箱验证码  |
| invite_code    | string | ✖︎  | 邀请码    |
| recaptcha_data | string | ✖︎  | 人机验证数据 |

- 成功返回示例 `json`

```json
{
  "data": {
    "token": "xxx",
    "auth_data": "xxx"
  }
}
```

| 参数名       | 类型     | 描述            |
|-----------|--------|---------------|
| token     | string | 用户 token      |
| auth_data | string | base64(邮箱:密码) |

### 6.重置密码

> `POST` /passport/auth/forget

- 请求参数 `json`

```json
{
  "email": "xxxx@xx.com",
  "password": "123456789",
  "email_code": 333333
}
```

| 参数名        | 类型     | 必填  | 描述    |
|------------|--------|-----|-------|
| email      | string | ✔︎  | 邮箱地址  |
| email_code | number | ✔︎  | 邮箱验证码 |
| password   | string | ✔︎  | 用户密码  |

- 成功返回示例 `json`

```json
{
  "data": true
}
```

| 参数名  | 类型      | 描述     |
|------|---------|--------|
| data | boolean | 是否重置成功 |

___

## User

### 1.登出

> `GET` /user/logout

- 请求参数
  `null`

- 成功返回示例 `json`

```json
{
  "data": true
}
```

| 参数名  | 类型      | 描述     |
|------|---------|--------|
| data | boolean | 是否登出成功 |

### 2.账号信息

> `GET` /user/info

- 请求参数
  `null`

- 成功返回示例 `json`

```json
{
  "data": {
    "email": "xxxx@xx.com",
    "transfer_enable": 0,
    "last_login_at": null,
    "created_at": 1234567890,
    "banned": 0,
    "remind_expire": 0,
    "remind_traffic": 0,
    "expired_at": 0,
    "balance": 0,
    "commission_balance": 0,
    "plan_id": null,
    "discount": null,
    "commission_rate": null,
    "telegram_id": null,
    "uuid": "xxxxxx-xxxx-xxxx-xxxx-xxxxxx",
    "avatar_url": "https://xxxx.com/xxx.xxx"
  }
}
```

| 参数名                | 类型                     | 描述      |
|--------------------|------------------------|---------|
| email              | string                 | 邮箱地址    |
| transfer_enable    | number                 | 总可用流量   |
| last_login_at      | timestamp              | 最后登入时间  |
| created_at         | timestamp              | 创建时间    |
| banned             | number                 | 是否封禁使用  |
| remind_expire      | number                 | 到期邮件提醒  |
| remind_traffic     | number                 | 流量邮件提醒  |
| expired_at         | timestamp              | 过期时间    |
| balance            | number                 | 用户余额    |
| commission_balance | number                 | 佣金余额    |
| plan_id            | number - object(&plan) | 当前订阅id  |
| discount           | number                 | 消费折扣    |
| commission_rate    | number                 | 佣金率     |
| telegram_id        | number                 | 绑定TG id |
| uuid               | string                 | 唯一UUID  |
| avatar_url         | string                 | 头像地址    |

### 3.订阅信息

> `GET` /user/getSubscribe

- 请求参数
  `null`

- 成功返回示例 `json`

```json
{
  "data": {
    "plan_id": null,
    "token": "xxx",
    "expired_at": 0,
    "u": 0,
    "d": 0,
    "transfer_enable": 0,
    "email": "xxx@xxx.com",
    "subscribe_url": "https://xxx.com/api/v1/client/subscribe?token=xxx",
    "reset_day": null
  }
}
```

| 参数名             | 类型                     | 描述       |
|-----------------|------------------------|----------|
| plan_id         | number - object(&plan) | 订阅id     |
| token           | string                 | 用户 token |
| expired_at      | timestamp              | 过期时间     |
| u               | number                 | 已用上行流量   |
| d               | number                 | 已用下行流量   |
| transfer_enable | number                 | 总可用流量    |
| email           | string                 | 邮箱地址     |
| subscribe_url   | string                 | 订阅链接     |
| reset_day       | number                 | 重置日      |

### 4.重置订阅链接

> `GET` /user/resetSecurity

- 请求参数
  `null`

- 成功返回示例 `json`

```json
{
  "data": "https://xxx.com/api/v1/client/subscribe?token=xxx"
}
```

| 参数名  | 类型     | 描述   |
|------|--------|------|
| data | string | 订阅链接 |

### 5.代办事项

> `GET` /user/getStat

- 请求参数
  `null`

- 成功返回示例 `json`

```json
{
  "data": [
    0,
    0,
    0
  ]
}
```

| 参数名     | 类型     | 描述    |
|---------|--------|-------|
| data[0] | number | 待付订单  |
| data[1] | number | 代办工单  |
| data[2] | number | 待确认邀请 |

### 6.修改密码

> `POST` /user/changePassword

- 请求参数 `json`

```json
{
  "old_password": "123456789",
  "new_password": "1234567890"
}
```

| 参数名          | 类型     | 必填  | 描述  |
|--------------|--------|-----|-----|
| old_password | string | ✔︎  | 旧密码 |
| new_password | string | ✔︎  | 新密码 |

- 成功返回示例 `json`

```json
{
  "data": true
}
```

| 参数名  | 类型      | 描述     |
|------|---------|--------|
| data | boolean | 是否修改成功 |

### 7.通知状态

> `POST` /user/update

- 请求参数 `json`

```json
{
  "remind_expire": 0
}
```

| 参数名            | 类型     | 必填  | 描述     |
|----------------|--------|-----|--------|
| remind_expire  | number | ✖︎︎ | 到期邮件提醒 |
| remind_traffic | number | ✖︎  | 流量邮件提醒 |

- 成功返回示例 `json`

```json
{
  "data": true
}
```

| 参数名  | 类型      | 描述     |
|------|---------|--------|
| data | boolean | 是否修改成功 |

### 8.佣金划转

> `POST` /user/transfer

- 请求参数 `json`

```json
{
  "transfer_amount": 1000
}
```

| 参数名             | 类型     | 必填  | 描述   |
|-----------------|--------|-----|------|
| transfer_amount | number | ✔︎  | 划转金额 |

- 成功返回示例 `json`

```json
{
  "data": true
}
```

| 参数名  | 类型      | 描述     |
|------|---------|--------|
| data | boolean | 是否划转成功 |

___

## Plan

### 1.订阅商店列表

> `GET` /user/plan/fetch

- 请求参数
  `null`

- 成功返回示例 `json`

```json
{
  "data": [
    {
      "id": 1,
      "group_id": 1,
      "transfer_enable": 100,
      "name": "Plan name",
      "show": 1,
      "sort": null,
      "renew": 1,
      "content": "xxx",
      "month_price": 10,
      "quarter_price": null,
      "half_year_price": null,
      "year_price": 20000,
      "two_year_price": null,
      "three_year_price": null,
      "onetime_price": null,
      "reset_price": 1000,
      "reset_traffic_method": null,
      "created_at": 1234567890,
      "updated_at": 1234567890
    }
  ]
}
```

| 参数名                  | 类型        | 描述     |
|----------------------|-----------|--------|
| id                   | number    | 订阅id   |
| group_id             | number    | 权限组id  |
| transfer_enable      | number    | 可用流量   |
| name                 | string    | 套餐名称   |
| show                 | number    | 是否显示   |
| sort                 | string    | 分类     |
| renew                | number    | 开启续费   |
| content              | string    | 套餐描述   |
| month_price          | number    | 月付价格   |
| quarter_price        | number    | 季度价格   |
| half_year_price      | number    | 半年价格   |
| year_price           | number    | 年价格    |
| two_year_price       | number    | 两年价格   |
| three_year_price     | number    | 三年价格   |
| onetime_price        | number    | 一次性价格  |
| reset_price          | number    | 重置价格   |
| reset_traffic_method | number    | 重置流量方式 |
| created_at           | timestamp | 套餐创建时间 |
| updated_at           | timestamp | 套餐更新时间 |

___

## Order

### 1.订单列表

> `GET` /user/order/fetch

- 请求参数
  `null`

- 成功返回示例 `json`

```json
{
  "data": [
    {
      "invite_user_id": null,
      "plan_id": 1,
      "coupon_id": null,
      "payment_id": 10,
      "type": 1,
      "cycle": "month_price",
      "trade_no": "xxx",
      "callback_no": null,
      "total_amount": 10,
      "discount_amount": null,
      "surplus_amount": null,
      "refund_amount": null,
      "balance_amount": null,
      "surplus_order_ids": null,
      "status": 2,
      "commission_status": 0,
      "commission_balance": 0,
      "paid_at": null,
      "created_at": 1234567890,
      "updated_at": 1234567890,
      "plan": {
        "表关联"
      }
    }
  ]
}
```

| 参数名                | 类型                       | 描述                        |
|--------------------|--------------------------|---------------------------|
| invite_user_id     | number                   | 邀请人id                     |
| plan_id            | number                   | 订阅id                      |
| coupon_id          | number                   | 优惠券id                     |
| payment_id         | number                   | 支付方式id                    |
| type               | number                   | 订单类型 1新购2续费3升级            |
| cycle              | string                   | 订阅周期                      |
| trade_no           | string                   | 订单号                       |
| callback_no        | string                   | 退款单号                      |
| total_amount       | number                   | 总金额                       |
| discount_amount    | number                   | 折扣金额                      |
| surplus_amount     | number                   | 剩余价值                      |
| refund_amount      | number                   | 退款金额                      |
| balance_amount     | number                   | 使用余额                      |
| surplus_order_ids  | number                   | 折抵订单                      |
| status             | number                   | 订单状态 0待支付1开通中2已取消3已完成4已折抵 |
| commission_status  | number                   | 佣金状态 0待确认1发放中2有效3无效       |
| commission_balance | number                   | 佣金余额                      |
| paid_at            | timestamp                | 支付时间                      |
| created_at         | timestamp                | 创建时间                      |
| updated_at         | timestamp                | 更新时间                      |
| plan               | [关联表](/plan.md/#1订阅商店列表) | 订阅详情                      |

### 2.支付方式

> `GET` /user/order/getPaymentMethod

- 请求参数
  `null`

- 成功返回示例 `json`

```json
{
  "data": [
    {
      "id": 10,
      "name": "pay",
      "payment": "XXXPay"
    }
  ]
}
```

| 参数名     | 类型     | 描述   |
|---------|--------|------|
| id      | number | 支付id |
| name    | string | 支付名称 |
| payment | string | 支付模块 |

### 3.订单详情

> `GET` /user/order/details?trade_no={trade_no}

- 请求参数 `query`

| 参数名      | 类型     | 描述  |
|----------|--------|-----|
| trade_no | string | 订单号 |

- 成功返回示例 `json`

```json
{
  "data": {
    "id": 1275,
    "invite_user_id": null,
    "user_id": 2057,
    "plan_id": 1,
    "coupon_id": null,
    "payment_id": null,
    "type": 1,
    "cycle": "month_price",
    "trade_no": "xxx",
    "callback_no": null,
    "total_amount": 10,
    "discount_amount": null,
    "surplus_amount": null,
    "refund_amount": null,
    "balance_amount": null,
    "surplus_order_ids": null,
    "status": 0,
    "commission_status": 0,
    "commission_balance": 0,
    "paid_at": null,
    "created_at": 1234567890,
    "updated_at": 1234567890,
    "plan": {
      "表关联"
    },
    "try_out_plan_id": 0
  }
}
```

| 参数名                | 类型                       | 描述                        |
|--------------------|--------------------------|---------------------------|
| id                 | number                   | 订单id                      |
| invite_user_id     | number                   | 邀请人id                     |
| user_id            | number                   | 用户id                      |
| user_id            | number                   | 用户自增id                    |
| plan_id            | number                   | 订阅id                      |
| coupon_id          | number                   | 优惠券id                     |
| payment_id         | number                   | 支付方式id                    |
| type               | number                   | 订单类型 1新购2续费3升级            |
| cycle              | string                   | 订阅周期                      |
| trade_no           | string                   | 订单号                       |
| callback_no        | string                   | 退款单号                      |
| total_amount       | number                   | 总金额                       |
| discount_amount    | number                   | 折扣金额                      |
| surplus_amount     | number                   | 剩余价值                      |
| refund_amount      | number                   | 退款金额                      |
| balance_amount     | number                   | 使用余额                      |
| surplus_order_ids  | number                   | 折抵订单                      |
| status             | number                   | 订单状态 0待支付1开通中2已取消3已完成4已折抵 |
| commission_status  | number                   | 佣金状态 0待确认1发放中2有效3无效       |
| commission_balance | number                   | 佣金余额                      |
| paid_at            | timestamp                | 支付时间                      |
| created_at         | timestamp                | 创建时间                      |
| updated_at         | timestamp                | 更新时间                      |
| plan               | [关联表](/plan.md/#1订阅商店列表) | 订阅详情                      |
| try_out_plan_id    | number                   | 试用计划 ID                   |

### 4.订单状态

> `GET` /user/order/check?trade_no={trade_no}

- 请求参数 `query`

| 参数名      | 类型     | 描述  |
|----------|--------|-----|
| trade_no | string | 订单号 |

- 成功返回示例 `json`

```json
{
  "data": 0
}
```

| 参数名  | 类型     | 描述                   |
|------|--------|----------------------|
| data | number | 0待支付1开通中2已取消3已完成4已折抵 |

### 5.创建订单

> `POST` /user/order/save

- 请求参数 `json`

```json
{
  "cycle": "month_price",
  "plan_id": 1
}
```

| 参数名     | 类型     | 描述   |
|---------|--------|------|
| cycle   | string | 订阅周期 |
| plan_id | number | 订阅id |

- 成功返回示例 `json`

```json
{
  "data": "xxx"
}
```

| 参数名  | 类型     | 描述  |
|------|--------|-----|
| data | string | 订单号 |

### 6.结算订单

> `POST` /user/order/checkout

- 请求参数 `json`

```json
{
  "trade_no": "xxx",
  "method": 1
}
```

| 参数名      | 类型     | 描述   |
|----------|--------|------|
| trade_no | string | 订单号  |
| method   | number | 支付id |

- 成功返回示例 `json`

```json
{
  "type": 0,
  "data": "xxx"
}
```

| 参数名  | 类型     | 描述             |
|------|--------|----------------|
| type | number | 0:qrcode 1:url |
| data | string | 付款地址           |

### 7.关闭订单

> `POST` /user/order/cancel

- 请求参数 `json`

```json
{
  "trade_no": "xxx"
}
```

| 参数名      | 类型     | 描述   |
|----------|--------|------|
| trade_no | string | 订单号  |

- 成功返回示例 `json`

```json
{
  "data": true
}
```

| 参数名  | 类型      | 描述     |
|------|---------|--------|
| data | boolean | 是否关闭成功 |

___

## Invite

### 1.邀请码管理

> `GET` /user/invite/fetch

- 请求参数 `null`

- 成功返回示例 `json`

```json
{
  "data": {
    "codes": [
      {
        "id": 1,
        "user_id": 1,
        "code": "xxx",
        "status": 0,
        "pv": 0,
        "created_at": 1234567890,
        "updated_at": 1234567890
      }
    ],
    "stat": [
      0,
      0,
      0,
      15,
      0
    ]
  }
}
```

| 参数名              | 类型        | 描述     |
|------------------|-----------|--------|
| codes.id         | number    | 邀请码id  |
| codes.user_id    | number    | 用户id   |
| codes.code       | array     | 邀请码    |
| codes.status     | number    | 邀请码状态  |
| codes.pv         | number    | 访问量    |
| codes.created_at | timestamp | 创建时间   |
| codes.updated_at | timestamp | 更新时间   |
| stat[0]          | number    | 已注册用户数 |
| stat[1]          | number    | 有效的佣金  |
| stat[2]          | number    | 确认中的佣金 |
| stat[3]          | number    | 佣金比例   |
| stat[4]          | number    | 可用佣金   |

### 2.生成邀请码

> `GET` /user/invite/save

- 请求参数 `null`

- 成功返回示例 `json`

```json
{
  "data": true
}
```

| 参数名  | 类型      | 描述   |
|------|---------|------|
| data | boolean | 生成成功 |

### 3.邀请明细

> `GET` /user/invite/details

- 请求参数 `null`

- 成功返回示例 `json`

```json
{
  "id": 1,
  "commission_status": 1,
  "commission_balance": 10,
  "created_at": 1234567890,
  "updated_at": 1234567890
}
```

| 参数名                | 类型        | 描述                  |
|--------------------|-----------|---------------------|
| id                 | number    | 邀请id                |
| commission_status  | number    | 佣金状态 0待确认1发放中2有效3无效 |
| commission_balance | number    | 佣金                  |
| created_at         | timestamp | 创建时间                |
| updated_at         | timestamp | 更新时间                |

___

## Notice

### 1.公告信息

> `GET` /user/notice/fetch

- 请求参数 `null`

- 成功返回示例 `json`

```json
{
  "data": [
    {
      "id": 1,
      "title": "xxx",
      "content": "xxx",
      "img_url": null,
      "created_at": 1234567890,
      "updated_at": 1234567890
    }
  ],
  "total": 1
}
```

| 参数名        | 类型        | 描述   |
|------------|-----------|------|
| id         | number    | 公告id |
| title      | string    | 标题   |
| content    | string    | 内容   |
| img_url    | timestamp | 背景图片 |
| created_at | timestamp | 创建   |
| updated_at | timestamp | 更新时间 |
| total      | number    | 总条数  |


## Ticket

### 1.工单列表
> `GET` /user/notice/fetch

- 请求参数 `null || id`

- 成功返回示例 `json`

``` json
{
    "data": [
        {
            "id": 1,
            "user_id": 1,
            "subject": "title",
            "level": 2,
            "status": 1,
            "reply_status": 0,
            "created_at": 1234567890,
            "updated_at": 1234567890
        }
    ]
}
```

| 参数名       | 类型      | 描述                    |
| ------------ | --------- | ----------------------- |
| id           | number    | 工单id                  |
| user_id      | number    | 发起者用户id            |
| subject      | string    | 标题                    |
| level        | number    | 工单等级 0 低 1 中 2 高 |
| status       | number    | 工单状态                |
| reply_status | number    | 回复状态                |
| created_at   | timestamp | 创建时间                |
| updated_at   | timestamp | 更新时间                |

- 请求参数为 id 
- 则返回详细信息

``` json
{
    "data": {
        "id": 1,
        "user_id": 1,
        "subject": "xxx",
        "level": 0,
        "status": 1,
        "reply_status": 1,
        "created_at": 1234567890,
        "updated_at": 1234567890,
        "message": [
            {
                "id": 1,
                "user_id": 1,
                "ticket_id": 1,
                "message": "xxxxx",
                "created_at": 1234567890,
                "updated_at": 1234567890,
                "is_me": false
            }
        ]
    }
}
```

| 参数名       | 类型      | 描述                    |
| ------------ | --------- | ----------------------- |
| id           | number    | 工单id                  |
| user_id      | number    | 发起者用户id            |
| subject      | string    | 标题                    |
| level        | number    | 工单等级 0 低 1 中 2 高 |
| status       | number    | 工单状态                |
| reply_status | number    | 回复状态                |
| created_at   | timestamp | 创建时间                |
| updated_at   | timestamp | 更新时间                |
| message      | array     | 消息内容 同上           |

### 2.创建工单
> `POST` /user/ticket/save

- 请求参数 `json`

``` json
 {
  "subject": "xxxxxx",
  "level": "0",
  "message": "xxxxxx"
}
```

| 参数名  | 类型   | 必填 | 描述       |
| ------- | ------ | ---- | ---------- |
| subject | string | ✔︎    | 标题       |
| level   | number | ✔︎    | 等级 0 1 2 |
| message | string | ✔︎    | 内容       |

- 成功返回示例 `json`

``` json
{
    "data": true
}
```

| 参数名 | 类型    | 描述     |
| ------ | ------- | -------- |
| data   | boolean | 返回成功 |

- 失败返回示例 `json`

``` json
{
    "message": "xxxx"
}
```

| 参数名  | 类型   | 描述 |
| ------- | ------ | ---- |
| message | string | 原因 |

### 3.回复工单

> `POST` /user/ticket/reply

- 请求参数 `json`

```json
{
    "id": 1,
    "message": "xxxxx"
}
```

| 参数名  | 类型   | 必填 | 描述     |
| ------- | ------ | ---- | -------- |
| id      | number | ✔︎    | 工单id   |
| message | string | ✔︎    | 回复内容 |

- 成功返回示例 `json`

``` json
{
    "data": true
}
```

| 参数名 | 类型    | 描述     |
| ------ | ------- | -------- |
| data   | boolean | 返回成功 |

### 4.关闭工单

> `POST` /user/ticket/close

- 请求参数 `json`

```json
{
    "id": 1
}
```

| 参数名 | 类型   | 必填 | 描述   |
| ------ | ------ | ---- | ------ |
| id     | number | ✔︎    | 工单id |

- 成功返回示例 `json`

``` json
{
    "data": true
}
```

| 参数名 | 类型    | 描述     |
| ------ | ------- | -------- |
| data   | boolean | 返回成功 |

### 

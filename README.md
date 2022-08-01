# V2Board 最全接口文档（1.6.0）

> 感谢 v2board 提供的开源项目！ 完整api请查阅开源项目 : [v2board](https://github.com/v2board/v2board)

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
| /user/logout          | GET  | [登出](/user.md/#1登出)        |
| /user/info            | GET  | [账号信息](/user.md/#2账号信息)    |
| /user/getSubscribe    | GET  | [订阅信息](/user.md/#3订阅信息)    |
| /user/resetSecurity   | GET  | [重置订阅链接](/user.md/#重置订阅链接) |
| /user/getStat         | GET  | [代办事项](/user.md/#5代办事项)    |
| /user/changePassword  | POST | [修改密码](/user.md/#6修改密码)    |
| /user/update          | POST | [通知状态](/user.md/#7通知状态)    |
| /user/transfer        | POST | [佣金划转](/user.md/#8佣金划转)    |

### Plan

| URL              | 请求  | 描述                          |
|------------------|-----|-----------------------------|
| /user/plan/fetch | GET | [订阅商店列表](/plan.md/#1订阅商店列表) |

### Order

| URL                           | 请求   | 描述                       |
|-------------------------------|------|--------------------------|
| /user/order/fetch             | GET  | [订单列表](/order.md/#1订单列表) |
| /user/order/getPaymentMethod  | GET  | [支付方式](/order.md/#2支付方式) |
| /user/order/details?trade_no= | GET  | [订单详情](/order.md/#3订单详情) |
| /user/order/check?trade_no=   | GET  | [订单状态](/order.md/#4订单状态) |
| /user/order/save              | POST | [创建订单](/order.md/#5创建订单) |
| /user/order/checkout          | POST | [结算订单](/order.md/#6结算订单) |
| /user/order/cancel            | POST | [关闭订单](/order.md/#7关闭订单) |

### Invite

| URL                  | 请求  | 描述                          |
|----------------------|-----|-----------------------------|
| /user/invite/fetch   | GET | [邀请码管理](/invite.md/#1邀请码管理) |
| /user/invite/save    | GET | [生成邀请码](/invite.md/#2生成邀请码) |
| /user/invite/details | GET | [邀请明细](/invite.md/#3邀请明细)   |

### Notice

| URL                  | 请求  | 描述                        |
|----------------------|-----|---------------------------|
| /user/notice/fetch   | GET | [公告信息](/notice.md/#1公告信息) |

### Ticket
gugugu...

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


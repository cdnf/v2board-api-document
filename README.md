# V2Board 最全接口文档（1.6.0）

> 感谢 v2board 提供的开源项目！ 完整api请查阅开源项目 : [v2board](https://github.com/v2board/v2board)

### Passport

| URL                            | 请求   | 描述                                |
|--------------------------------|------|-----------------------------------|
| /passport/comm/config          | GET  | [获取配置](####1获取配置)       |
| /passport/auth/check           | GET  | [登入校验](####2登入校验)       |
| /passport/auth/login           | POST | [登入账号](####3登入账号)       |
| /passport/comm/sendEmailVerify | POST | [发送邮箱验证码](####4发送邮箱验证码) |
| /passport/auth/register        | POST | [注册账号](####5注册账号)       |
| /passport/auth/forget          | POST | [重置密码](####6重置密码)       |

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




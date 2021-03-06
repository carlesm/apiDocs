---
title: 验证码
last_updated: 2019-03-20
sidebar: mydoc_sidebar
permalink: code.html
folder: mydoc
---

 验证码作为注册，重置密码，找回密码的用户安全认证校验，向指定电话号码或者邮箱发送。

- 正式环境URL: ``` https://cn(区域)-api.coolkit.cn:8080/api/sms``` 

- 测试环境URL: ``` https://testapi.coolkit.cn:8080/api/sms``` 

- 请求方法： POST

- 请求参数：注意email和to不会同时存在，邮箱接收验证码只传email，电话号码接收验证码只传to

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|sendType |是  |String |发送类型：sendType:0 注册 ：只要手机号或者email格式合法并且未注册的用户就可以发送，已注册的用户再请求，不会发送验证码。 sendType:1 重置密码：要判断手机号或者邮箱是不是在Users表，不存在的不发送，应该提示账号不存在，避免用户填错了   |
|email |否  |String | 邮箱(email和to只传递其中一个，不能都不传递)    |
|to     |否  |String | 用户手机号，带国家码。格式: +8615815725225 (+86中国)    |

**响应参数:**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|error |是  |String | 错误码  |
|region |否  |String | error：301的情况下用户所属区域代码，如：中国(cn)   |

```
错误码：
0:操作成功
301:用户在其他大区，需要客户端结合region重定向,重新连接
400:参数错误
401:账号不存在
409:用户已经注册
500:服务器错误
504:发送失败
160038:发送频率高，超过限制
```

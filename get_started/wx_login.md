# 微信接入与检测注册

## 简介

我们提供位于小程序底层的微信用户接入，基于此，我们可以获取到用户在当前小程序的唯一标识（openid）和用户id（uid）等用户有关核心信息 及 访问令牌access\_token。

{% hint style="info" %}
我们采用access\_token的形式控制访问，并以此作为用户访问我们其他服务的唯一令牌

当然，在用户被记录在数据库之前，我们仍需使用openid作为判断用户身份的依据
{% endhint %}

在全局获取access\_token的方法有两种，一种针对新用户注册，它的获取方式在[用户注册](../user/register.md)章节；另一种针对已注册的用户，本节将引导你获取这类用户的access\_token，如果你还不明白如何使用access\_token，请阅读上一节[前期准备](prepare.md)

## 请求

## 接入与检测

<mark style="color:green;">`POST`</mark> `/v1/user/login`

**Headers**

| 属性           | 值                  |
| ------------ | ------------------ |
| Content-Type | `application/json` |

**Body**

| 属性   | 类型     | 描述                                       | 必填 |
| ---- | ------ | ---------------------------------------- | -- |
| code | string | <p>在app.js中</p><p>调用wx.login后返回的code</p> | 是  |

**Response**

{% tabs %}
{% tab title="有注册用户" %}
```json
{
	"success": true,
	"registered": true,
	"openid": "xxx",
	"access_token": "xxx",
	"uid": "xxx",
	"email": "xxx",
	"avatar": "xxx",
	"campus": "xxx",
	"phone": "xxx",
	"role": "xxx",
	"nickname": "xxx"
}
```
{% endtab %}

{% tab title="无注册用户" %}
```json
{
	"success": true,
	"registered": false,
	"openid": "xxx",
	"email": "",
	"avatar": "",
	"phone": "",
	"role": "",
	"nickname": ""
}
```
{% endtab %}

{% tab title="请求失败" %}
```json
{
	"success": false,
	"error": {
		"errcode": xxx,
		"errmsg": "xxx"
	},
	"registered": false
}
```
{% endtab %}
{% endtabs %}

| 属性            | 类型     | 描述     |
| ------------- | ------ | ------ |
| success       | string | 请求是否成功 |
| registered    | string | 是否注册   |
| openid        | string | 唯一用户标识 |
| access\_token | srting | 访问令牌   |
| uid           | int    | 用户id   |
| email         | string | 用户邮箱   |
| phone         | string | 用户手机号  |
| avatar        | string | 用户头像地址 |
| campus        | string | 用户所在校区 |
| nickname      | string | 用户昵称   |

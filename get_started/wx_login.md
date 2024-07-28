# 微信接入与检测注册

## 简介

我们提供位于小程序底层的微信用户接入，基于此，我们可以获取到用户在当前小程序的唯一标识（openid）和用户id（uid）等用户有关核心信息 及 访问令牌access\_token。

{% hint style="info" %}
我们采用access\_token的形式控制访问，并以此作为用户访问我们其他服务的唯一令牌
{% endhint %}

本节将引导你获取用户的access\_token。

如果你还不明白如何使用access\_token，请阅读上一节[前期准备](prepare.md)

现阶段的access\_token将仅能由此接口获取

## 请求

## 接入与检测

<mark style="color:green;">`POST`</mark> `/v1/user/login`

**Headers**

| 属性           | 值                  |
| ------------ | ------------------ |
| Content-Type | `application/json` |

**Body**

| 属性   | 类型     | 描述                     | 必填 |
| ---- | ------ | ---------------------- | -- |
| code | string | 前端调用wx.login()后返回的code | 是  |

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
	"access_token": "xxx",
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
		"errmsg": "xxx" //这里的错误信息来自微信开发文档，可按照上方错误码及链接对照理解：https://developers.weixin.qq.com/miniprogram/dev/framework/usability/PublicErrno.html
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

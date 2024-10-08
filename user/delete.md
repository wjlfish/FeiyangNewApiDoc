# 删除用户

## 简介

在需要删除一个用户时使用此接口

{% hint style="info" %}
自小程序线上版本1.0.9起，本接口已支持注销技术员自动重分配
{% endhint %}

## &#x20;请求

## 删除用户

<mark style="color:green;">`POST`</mark> `/v1/user/delete`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性     | 类型     | 描述           | 必填 |
| ------ | ------ | ------------ | -- |
| openid | string | 要注销用户的openid | 是  |

**Response**

{% tabs %}
{% tab title="删除成功" %}
```json
{
	"success": true,
	"message": "用户删除成功"
}
```
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述     |
| ------- | ------ | ------ |
| success | string | 请求是否成功 |
| message | string | 提示信息   |

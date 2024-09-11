# 更改用户信息

## 简介

在需要更改用户信息的地方使用该接口，因此他的应用场景主要有以下两个：

1. （在首次手机号验证通过后）应该强制用户填入邮箱、昵称、头像等信息，以完成注册全流程，否则保留该用户的登录状态，但是不允许其使用其他功能，直到信息全部填妥。
2. （日后用户若想更改信息）也可以直接调用该接口。本接口会自动检测未改变的值，只更新用户要求改变的部分。也就是并非所有字段都是必填值，详情可见下文body列表。

如果用户需要更改头像，同样也是调用这个接口，本接口支持接收图片地址

{% hint style="danger" %}
自小程序线上版本1.0.8起，本接口已不再支持 <mark style="color:yellow;">**手机号**</mark> 的更改，如需更改请浏览 [手机号换绑](phonechange.md)
{% endhint %}

{% hint style="warning" %}
自小程序线上版本1.1.0起，本接口将不再支持  <mark style="color:green;">**邮件**</mark> 的更改，如需更改请浏览 [绑定邮箱](newemail.md)
{% endhint %}

## &#x20;请求

## 信息更改

<mark style="color:green;">`POST`</mark> `/v1/user/setuser`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性        | 类型     | 描述                         | 必填 |
| --------- | ------ | -------------------------- | -- |
| email     | string | 用户邮箱                       |    |
| nickname  | string | 用户昵称                       |    |
| avatar    | string | 用户头像地址                     |    |
| campus    | string | 用户所在校区                     |    |
| role      | string | 用户身份                       |    |
| available | bool   | 技工接单状态                     |    |
| wants     | string | <p>用户接单意愿<br>abcde依次递增</p> |    |

**Response**

{% tabs %}
{% tab title="修改成功" %}
```json
//假如此处仅修改了用户昵称
{
	"success": true,
	"changedFields": {
		"nickname": "xxx"
	}
}
```
{% endtab %}
{% endtabs %}

| 属性            | 类型     | 描述     |
| ------------- | ------ | ------ |
| success       | string | 请求是否成功 |
| changedFields | json   | 修改的值   |

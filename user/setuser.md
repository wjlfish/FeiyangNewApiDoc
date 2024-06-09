# 更改用户信息

## 简介

在需要更改用户信息的地方使用该接口，因此他的应用场景主要有以下两个：

1. （在首次手机号验证通过后）应该强制用户填入邮箱、昵称、头像等信息，以完成注册全流程，否则保留该用户的登录状态，但是不允许其使用其他功能，直到信息全部填妥。
2. （日后用户若想更改信息）也可以直接调用该接口。本接口会自动检测未改变的值，只更新用户要求改变的部分。也就是并非所有字段都是必填值，详情可见下文body列表。

当然，被用来定位用户的openid是必填的。。。

如果用户需要更改头像，同样也是调用这个接口，本接口支持接收图片地址

{% hint style="info" %}
暂不支持手机号换绑，所以别让用户填手机号进来哦！！！
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

| 属性       | 类型     | 描述     | 必填 |
| -------- | ------ | ------ | -- |
| openid   | string | 唯一用户标识 | 是  |
| email    | string | 用户邮箱   |    |
| nickname | string | 用户昵称   |    |
| avatar   | string | 用户头像地址 |    |
| campus   | string | 用户所在校区 |    |
| role     | string | 用户身份   |    |

**Response**

{% tabs %}
{% tab title="验证通过" %}
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

{% tab title="已有用户" %}
<pre class="language-json"><code class="lang-json"><strong>{
</strong>	"status": "verification_failed",
	"success": false,
	"registered": false,
	"openid": "",
	"email": "",
	"avatar": "",
	"phone": "",
	"nickname": ""
}
</code></pre>
{% endtab %}
{% endtabs %}

| 属性            | 类型     | 描述     |
| ------------- | ------ | ------ |
| success       | string | 请求是否成功 |
| changedFields | json   | 修改的值   |

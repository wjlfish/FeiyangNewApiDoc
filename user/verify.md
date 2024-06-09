# 验证码校验

## 简介

在申请验证码后，需要使用获取到的验证码进行校验。因为在申请验证码时已经给到了一个access\_token，所以此处就不再返回access\_token，这也是我们建议你再上个环节就存储该值的原因。

## &#x20;请求

## 验证码校验

<mark style="color:green;">`POST`</mark> `/v1/user/verify`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性                 | 类型     | 描述    | 必填 |
| ------------------ | ------ | ----- | -- |
| phone              | string | 用户手机号 | 是  |
| verification\_code | int    | 验证码   | 是  |

**Response**

{% tabs %}
{% tab title="验证通过" %}
```json
{
	"status": "verified",
	"success": true,
	"registered": true,
	"openid": "xxx",
	"email": "",
	"uid": "xxx",
	"avatar": "",
	"role": "xxx",
	"phone": "xxx",
	"nickname": "NULL"
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
	"role": "",
	"phone": "",
	"nickname": ""
}
</code></pre>
{% endtab %}
{% endtabs %}

| 属性         | 类型     | 描述     |
| ---------- | ------ | ------ |
| success    | string | 请求是否成功 |
| status     | string | 验证具体状态 |
| registered | string | 是否注册   |
| openid     | string | 唯一用户标识 |
| uid        | int    | 用户id   |
| email      | string | 用户邮箱   |
| phone      | string | 用户手机号  |
| avatar     | string | 用户头像地址 |
| nickname   | string | 用户昵称   |

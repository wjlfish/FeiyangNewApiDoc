# 绑定邮箱

## 简介

此接口用于更改用户绑定的邮箱，因为邮箱的特殊性，必须通过激活邮件来确认绑定。因此以此接口来进行绑定请求的发起。

{% hint style="info" %}
此接口自小程序线上版本1.1.0起启用
{% endhint %}

## &#x20;请求

## 绑定邮箱

<mark style="color:green;">`POST`</mark> `/v1/user/newemail`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性    | 类型     | 描述   | 必填 |
| ----- | ------ | ---- | -- |
| email | string | 用户邮箱 | 是  |

**Response**

{% tabs %}
{% tab title="成功发送" %}
<pre class="language-json"><code class="lang-json"><strong>{
</strong>	"success": true,
	"status": "verification_email_sent"
}
</code></pre>
{% endtab %}

{% tab title="邮箱未改变" %}
```json
{
	"success": false,
	"status": "same_email"
}
```
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述     |
| ------- | ------ | ------ |
| success | string | 请求是否成功 |
| status  | string | 请求标识   |

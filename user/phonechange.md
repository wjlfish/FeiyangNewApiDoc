# 手机号换绑

## 简介

此接口用于更改用户绑定的手机号，因为手机号的特殊性，必须发起验证码验证。因此以此接口来进行换绑请求的发起。

接下来，需要使用

## &#x20;请求

## 注册

<mark style="color:green;">`POST`</mark> `/v1/user/newphone`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性    | 类型     | 描述    | 必填 |
| ----- | ------ | ----- | -- |
| phone | string | 用户手机号 | 是  |

**Response**

{% tabs %}
{% tab title="成功发送" %}
<pre class="language-json"><code class="lang-json"><strong>{
</strong>	"success": true,
	"status": "verification_code_sent"
}
</code></pre>
{% endtab %}

{% tab title="手机号未改变" %}
```json
{
	"success": false,
	"status": "same_phone"
}
```
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述     |
| ------- | ------ | ------ |
| success | string | 请求是否成功 |
| status  | string | 请求标识   |

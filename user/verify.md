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
	"success": true
}
```
{% endtab %}

{% tab title="验证失败" %}
<pre class="language-json"><code class="lang-json"><strong>{
</strong>	"status": "verification_failed",
	"success": false
}
</code></pre>
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述     |
| ------- | ------ | ------ |
| success | string | 请求是否成功 |
| status  | string | 验证具体状态 |

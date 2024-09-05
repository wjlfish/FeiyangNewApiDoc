# 验证码校验（换绑）

## 简介

换绑时需要以此接口来进行验证

{% hint style="info" %}
此接口自小程序线上版本1.1.0起启用
{% endhint %}

## &#x20;请求

## 验证码校验（换绑）

<mark style="color:green;">`POST`</mark> `/v1/user/phonechange_verify`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性   | 类型  | 描述  | 必填 |
| ---- | --- | --- | -- |
| code | int | 验证码 | 是  |

**Response**

{% tabs %}
{% tab title="验证通过" %}
```json
{
	"status": "phone_updated",
	"success": true
}
```
{% endtab %}

{% tab title="验证失败" %}
<pre class="language-json"><code class="lang-json"><strong>{
</strong>	"status": "bad_code",
	"success": false
}
</code></pre>
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述     |
| ------- | ------ | ------ |
| success | string | 请求是否成功 |
| status  | string | 验证具体状态 |

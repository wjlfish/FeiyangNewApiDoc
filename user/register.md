# 新用户注册

## 简介

在确认了用户未注册时，我们需要为用户做注册。每个用户和一个手机号强绑定，所以这里的注册其实附加了一个手机号验证。本接口可以绑定到获取验证码的按钮上异步执行，在向数据库中写入数据的同时，获取短信验证码。

判定用户是否注册的标识在上一节的检测注册环节已返回，即"registered": false时，本节的内容才会被使用。

2024.9.4起，此接口兼顾判断目标手机号是否为4.0系统之前就注册过的老用户，在判断该用户为老用户后，此接口会返回**Response中的**<mark style="color:orange;">**第三类**</mark>** ，**我们对老用户有特殊的处理方案，详见[#迁移用户](migration.md)

## &#x20;请求

## 注册

<mark style="color:green;">`POST`</mark> `/v1/user/register`

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
	"access_token": "xxxxxxxxxxxxxxxxxxxx"
}
</code></pre>
{% endtab %}

{% tab title="已有用户" %}
```json
{
	"success": true,
	"status": "user_exists"
}
```
{% endtab %}

{% tab title="该用户为老用户" %}
<pre class="language-json"><code class="lang-json"><strong>{
</strong>	"success": true,
	"status": "user_need_migration"
	"access_token": "xxxxxxxxxxxxxxxxxxxx"
}
</code></pre>
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述     |
| ------- | ------ | ------ |
| success | string | 请求是否成功 |
| status  | string | 请求标识   |

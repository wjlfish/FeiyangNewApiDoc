# 新用户注册

## 简介

在确认了用户未注册时，我们需要为用户做注册。每个用户和一个手机号强绑定，所以这里的注册其实附加了一个手机号验证。本接口可以绑定到获取验证码的按钮上异步执行，在向数据库中写入数据的同时，获取短信验证码。

判定用户是否注册的标识在上一节的检测注册环节已返回，即"registered": false时，本节的内容才会被使用。

由于此时该用户还未录入数据库，所以此处采用openid作为判定身份的依据。

此请求若成功，则会返回一个access\_token，在接下来校验验证码的环节就要用到我们的[标准鉴权](../get\_started/prepare.md#gnvxc)了。所以在这里我们就建议把该access\_token存入本地存储中，当然具体怎么开发还是看你啦。

## &#x20;请求

## 注册

<mark style="color:green;">`POST`</mark> `/v1/user/register`

**Headers**

| 属性           | 值                  |
| ------------ | ------------------ |
| Content-Type | `application/json` |

**Body**

| 属性     | 类型     | 描述       | 必填 |
| ------ | ------ | -------- | -- |
| phone  | string | 用户手机号    | 是  |
| openid | string | 用户openid | 是  |

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
{% endtabs %}

| 属性      | 类型     | 描述     |
| ------- | ------ | ------ |
| success | string | 请求是否成功 |
| status  | string | 请求标识   |

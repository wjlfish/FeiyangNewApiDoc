# 完成工单

## 简介

此接口用于在技术员端完成当前工单的维修

一定要注意，发起结束工单的技术员一定要对应此工单分配的技术员，否则会报错

## &#x20;请求

## 注册

<mark style="color:green;">`POST`</mark> `/v1/ticket/complete`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性        | 类型  | 描述       | 必填 |
| --------- | --- | -------- | -- |
| order\_id | int | 需要结束的工单号 | 是  |

**Response**

{% tabs %}
{% tab title="成功结单" %}
<pre class="language-json"><code class="lang-json"><strong>{
</strong>	"success": true,
	"status": "ticket_completed"
}
</code></pre>
{% endtab %}

{% tab title="工单未找到" %}
<pre class="language-json"><code class="lang-json"><strong>{
</strong>	"success": false,
	"status": "ticket not found"
}
</code></pre>
{% endtab %}

{% tab title="技术员与工单分配不对应" %}
<pre class="language-json"><code class="lang-json"><strong>{
</strong>	"success": false,
	"status": "technician does not match the ticket"
}
</code></pre>
{% endtab %}

{% tab title="未知错误" %}
```json
{
	"success": false,
	"status": "unknown_error"
}
```
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述     |
| ------- | ------ | ------ |
| success | string | 请求是否成功 |
| status  | string | 请求标识   |

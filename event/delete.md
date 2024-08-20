# 删除活动

## 简介

在需要删除一个活动时使用此接口

## &#x20;请求

## 删除活动

<mark style="color:green;">`POST`</mark> `/v1/event/delete`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性 | 类型     | 描述   | 必填 |
| -- | ------ | ---- | -- |
| id | string | 活动id | 是  |

**Response**

{% tabs %}
{% tab title="删除成功" %}
```json
{
	"success": true,
	"message": "活动删除成功"
}
```
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述     |
| ------- | ------ | ------ |
| success | string | 请求是否成功 |
| message | string | 提示信息   |

# 删除反馈

## 简介

在需要删除一个反馈时使用此接口

## &#x20;请求

## 删除反馈

<mark style="color:green;">`POST`</mark> `/v1/feedback/delete`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性 | 类型     | 描述   | 必填 |
| -- | ------ | ---- | -- |
| id | string | 问题id | 是  |

**Response**

{% tabs %}
{% tab title="删除成功" %}
```json
{
	"success": true,
	"message": "反馈删除成功"
}
```
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述     |
| ------- | ------ | ------ |
| success | string | 请求是否成功 |
| message | string | 提示信息   |

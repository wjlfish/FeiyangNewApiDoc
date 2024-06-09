# 报名活动（非大修）

## 简介

此接口用于在用户端报名一个已经创建好的活动

## &#x20;请求

## 报名活动

<mark style="color:green;">`POST`</mark> `/v1/event/regevent`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性           | 类型  | 描述   | 必填 |
| ------------ | --- | ---- | -- |
| activity\_id | int | 活动编号 | 是  |
| uid          | int | 用户id | 是  |

**Response**

{% tabs %}
{% tab title="报名成功" %}
```json
{
	"success": true
}
```
{% endtab %}

{% tab title="报名活动类型为大修" %}
```json
{
	"success": false,
	"message": "请使用大修活动报名接口"
}
```
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述      |
| ------- | ------ | ------- |
| status  | string | 是否报名成功  |
| message | string | 请求失败的原因 |

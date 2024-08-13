# 修改反馈

## 简介

此接口用于修改一个用户反馈。

此处的修改包括但不限于：

1.对某个反馈进行官方解答

2.对反馈内容的增删修改

## &#x20;请求

## 信息更改

<mark style="color:green;">`POST`</mark> `/v1/feedback/set`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性       | 类型     | 描述   | 必填 |
| -------- | ------ | ---- | -- |
| question | string | 反馈内容 |    |
| answer   | string | 回答   |    |
| status   | string | 解答状态 |    |

**Response**

{% tabs %}
{% tab title="修改成功" %}
```json
//假如此处仅修改了回答
{
	"success": true,
	"changedFields": {
		"answer": "xxx"
	}
}
```
{% endtab %}
{% endtabs %}

| 属性            | 类型     | 描述     |
| ------------- | ------ | ------ |
| success       | string | 请求是否成功 |
| changedFields | json   | 修改的值   |

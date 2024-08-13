# 新增反馈

## 简介

此接口用于新增一个用户反馈。

原则上，该接口支持最多1000字的文字反馈，请前端开发时做好字数控制。

## &#x20;请求

## 新增反馈

<mark style="color:green;">`POST`</mark> `/v1/feedback/add`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 参数名  | 类型     | 描述     |
| ---- | ------ | ------ |
| text | string | 用户反馈内容 |

**Response**

{% tabs %}
{% tab title="新增成功" %}
```json
{
	"success": true,
	"qid": "反馈问题的id"
}
```
{% endtab %}

{% tab title="注册失败" %}
```json
{
	"success": false,
	"qid": ""
}
```
{% endtab %}
{% endtabs %}

| 参数名     | 类型      | 描述      |
| ------- | ------- | ------- |
| success | boolean | 请求是否成功  |
| qid     | int     | 反馈问题的id |

####

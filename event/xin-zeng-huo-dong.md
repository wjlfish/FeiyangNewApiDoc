# 新增活动

## 简介

此接口用于在管理端创建一个新的活动

所有的活动创建接口都在这里，包括大修。但是报名接口是大修和其他活动分离的。

## &#x20;请求

## 创建活动

<mark style="color:green;">`POST`</mark> `/v1/event/create`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性                  | 类型     | 描述          | 必填 |
| ------------------- | ------ | ----------- | -- |
| name                | string | 活动名称        | 是  |
| type                | string | 讲座/例会/大修/其他 | 是  |
| description         | string | 活动描述        | 是  |
| start\_time         | string | 活动开始时间      | 是  |
| signup\_start\_time | string | 报名开始时间      | 是  |
| signup\_end\_time   | string | 报名结束时间      | 是  |

**Response**

{% tabs %}
{% tab title="创建成功" %}
```json
{
	"success": true,
	"eventid": "xxx"
}
```
{% endtab %}

{% tab title="创建失败" %}
```json
{
	"success": false,
	"eventid": ""
}
```
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述     |
| ------- | ------ | ------ |
| status  | string | 是否创建成功 |
| eventid | int    | 活动编号   |

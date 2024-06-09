# 报名活动（大修）

## 简介

此接口用于在用户端报名一个已经创建好的大修

## &#x20;请求

## 报名大修

<mark style="color:green;">`POST`</mark> `/v1/event/regrepair`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性           | 类型     | 描述       | 必填 |
| ------------ | ------ | -------- | -- |
| activity\_id | int    | 活动编号     | 是  |
| uid          | int    | 用户id     | 是  |
| name         | string | 报名者真实姓名  | 是  |
| gender       | string | 报名者性别    | 是  |
| departments  | array  | 所在部门（多选） | 是  |
| free\_times  | array  | 空闲时间（多选） | 是  |

**这里的array其实还并不特别严谨，为了方便理解，我将给出一个请求示例：**

```json
{
    "activity_id": 1,
    "user_id": 123,
    "name": "张三",
    "gender": "男",
    "departments": ["研发部", "行政部"],
    "free_times": ["08:00-10:00", "12:00-14:00", "16:00-18:00"]
}
//一个叫张三的哥们同时任职于研发部和行政部，他的空闲时间是8点到10点、12点到14点、16点到18点
```



**Response**

{% tabs %}
{% tab title="报名成功" %}
```json
{
	"success": true
}
```
{% endtab %}

{% tab title="报名活动类型不是大修" %}
```json
{
	"success": false,
	"message": "此活动不是大修活动"
}
```
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述      |
| ------- | ------ | ------- |
| status  | string | 是否报名成功  |
| message | string | 请求失败的原因 |

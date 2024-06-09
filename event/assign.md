# 分配大修点位

## 简介

此接口用于在管理端为一个已经结束报名的大修进行点位分配

此接口运用匈牙利算法，可以最高效地排列出排班表。

## &#x20;请求

## 分配点位

<mark style="color:green;">`POST`</mark> `/v1/event/assign`

**Headers**

| 属性                                                         | 值                      |
| ---------------------------------------------------------- | ---------------------- |
| Content-Type                                               | `application/json`     |
| Authorization（_<mark style="color:red;">**暂时不需要**</mark>_） | Bearer {access\_token} |

**Body**

| 属性           | 类型    | 描述       | 必填 |
| ------------ | ----- | -------- | -- |
| activity\_id | int   | 活动编号     | 是  |
| time\_slots  | array | 该活动各时间间隔 | 是  |

{% hint style="info" %}
_**time\_slots**_ 应该严格与报名时存在的所有时间间隔匹配，否则会出现该范围外的点位无法分配的情况
{% endhint %}

**为了方便理解，我将在这里给出一个请求示例：**

```json
{
    "activity_id": 1,
    "time_slots": ["08:00-10:00","10:00-12:00","12:00-14:00","14:00-16:00","16:00-18:00"]
}
//id为1的活动从早8到晚18 每隔两小时喂一个时间间隔
```

**Response**

{% tabs %}
{% tab title="分配成功" %}
```json
{
	"success": true,
	"assignment": [
		{
			"name": "xx",
			"time_slot": "08:00-10:00",
			"department": "1号位"
		},
		{
			"name": "xx",
			"time_slot": "08:00-10:00",
			"department": "现场行政"
		}
	],
	"ifxlsx": true,
	"xlsxurl": "https://fyapi2.wjlo.cc/v1/event/lists/xxx.xlsx"
}
```
{% endtab %}

{% tab title="分配失败" %}
```json
{
	"success": false
}
```
{% endtab %}
{% endtabs %}

| 属性         | 类型     | 描述             |
| ---------- | ------ | -------------- |
| status     | string | 是否报名成功         |
| assignment | array  | 具体的分配情况        |
| ifxlsx     | string | 是否成功生成对应xlsx文件 |
| xlsxurl    | url    | xlsx文件对应的url地址 |

# 大修个人改时间

## 简介

此接口用于在用户端和管理端修改一个用户在某次大修的空闲时间

这里的修改逻辑是，如果有人因为自己的原因修改了时间，那么他将退回到排队序列的最后一位。同时，我们将遍历一次还没有被分配的报名者，并顺延分配给下一位符合条件的报名者。

## &#x20;请求

## 修改时间

<mark style="color:green;">`POST`</mark> `/v1/event/repairchangetime`

**Headers**

| 属性                                                             | 值                      |
| -------------------------------------------------------------- | ---------------------- |
| Content-Type                                                   | `application/json`     |
| Authorization（_<mark style="color:red;">**暂时**</mark>**不需要**_） | Bearer {access\_token} |

**Body**

| 属性           | 类型    | 描述       | 必填 |
| ------------ | ----- | -------- | -- |
| activity\_id | int   | 活动编号     | 是  |
| free\_times  | array | 要修改的时间范围 | 是  |
| uid          | int   | 用户id     | 是  |

{% hint style="info" %}
_**free\_times**_ 应该严格与报名时存在的所有时间间隔匹配，否则会出现该范围外的点位无法分配的情况
{% endhint %}

**为了方便理解，我将在这里给出一个请求示例：**

```json
{
	"free_times": "["10:00-12:00","12:00-14:00","14:00-16:00","16:00-18:00"]",
	"activity_id": "1",
	"uid": "15"
}
//uid为15的用户除了早八起不来，其他时间都能来参加id为1的大修
```

**Response**

{% tabs %}
{% tab title="修改成功" %}
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

{% tab title="修改失败" %}
```json
{
	"success": false
}
```
{% endtab %}
{% endtabs %}

| 属性         | 类型     | 描述                |
| ---------- | ------ | ----------------- |
| status     | string | 是否修改成功            |
| assignment | array  | 修改后所有人具体的分配情况     |
| ifxlsx     | string | 是否成功生成对应xlsx文件    |
| xlsxurl    | url    | 修改后xlsx文件对应的url地址 |

# 转移/强分配工单

## 简介

此接口用于修改工单的派单状态

当前允许以下几个身份在不同情境下的修改：

1.管理员：修改任意id的工单派单状态，可强行指派或更改某个工单的分配技术员；

2.技术员：修改被分配到此技术员的工单信息。

{% hint style="info" %}
对于某个已被分配维修的工单，此接口可以修改已分配的技术员，并重新发送对应提醒

对于某个未被分配，且需要强制分配到某技术员的工单，此接口也可以实现强制分配
{% endhint %}

{% hint style="warning" %}
传入的 `order_id`和`order_hash`必须对应同一个工单
{% endhint %}

{% hint style="danger" %}
未传入tid时，该值将被默认为发起请求的用户id。在管理端调用此接口时，请务必注意<mark style="color:red;">携带tid</mark>
{% endhint %}

## &#x20;请求

## 转移/强分配工单

<mark style="color:green;">`POST`</mark> `/v1/ticket/give`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性          | 类型     | 描述          | 必填 |
| ----------- | ------ | ----------- | -- |
| order\_id   | int    | 需要更改的工单号    | 是  |
| order\_hash | string | 需要更改的工单hash | 是  |
| tid         | int    | 想要分配的技术员id  |    |

**Response**

{% tabs %}
{% tab title="未分配订单分配成功" %}
```json
{
  "success": true,
  "message": "Order assigned successfully",
  "technician_id": 1123,
  "assigned_time": "2024-09-11 11:12:36"
}
```
{% endtab %}

{% tab title="转单分配成功" %}
```json
{
  "success": true,
  "message": "Order transferred successfully",
  "new_technician_id": 1123,
  "new_assigned_time": "2024-09-11 11:12:36"
}
```
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述     |
| ------- | ------ | ------ |
| success | string | 请求是否成功 |
| message | string | 信息     |

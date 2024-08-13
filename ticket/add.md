# 新增工单

## 简介

此接口用于在用户端创建一个新的报修工单

## &#x20;请求

## 创建工单

<mark style="color:green;">`POST`</mark> `/v1/ticket/create`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性             | 类型     | 描述       | 必填 |
| -------------- | ------ | -------- | -- |
| purchase\_date | date   | 机器购买时间   | 是  |
| phone          | string | 用于联系的手机号 | 是  |
| device\_type   | string | 设备类型     | 是  |
| brand          | string | 设备品牌     | 是  |
| description    | string | 报修问题描述   | 是  |
| image          | string | 报修图片地址   |    |
| fault\_type    | string | 问题类型     | 是  |
| qq             | int    | 用户预留qq号  | 是  |
| campus         | string | 用户所在校区   | 是  |

**Response**

{% tabs %}
{% tab title="创建成功" %}
```json
{
	"success": true,
	"orderid": "xxx"
}
```
{% endtab %}

{% tab title="创建失败" %}
```json
{
	"success": false,
	"orderid": ""
}
```
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述     |
| ------- | ------ | ------ |
| status  | string | 是否创建成功 |
| orderid | int    | 工单号    |

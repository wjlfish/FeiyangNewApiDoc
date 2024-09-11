# 修改工单

## 简介

此接口用于修改某个工单的信息或状态。

当前允许以下几个身份在不同情境下的修改：

1.管理员：修改任意id的工单信息；

2.用户：修改由本人发起的工单信息；

3.技术员：修改被分配到此技术员的工单信息。

{% hint style="info" %}
自小程序线上版本1.0.9起，本接口已不再支持 <mark style="color:yellow;">**工单分配信息**</mark> 的更改，如需更改请浏览&#x20;
{% endhint %}

## &#x20;请求

## 修改工单

<mark style="color:green;">`POST`</mark> `/v1/ticket/set`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性             | 类型     | 描述       | 必填 |
| -------------- | ------ | -------- | -- |
| tid            | int    | 要修改的工单号  |    |
| purchase\_date | date   | 机器购买时间   |    |
| phone          | string | 用于联系的手机号 |    |
| device\_type   | string | 设备类型     |    |
| brand          | string | 设备品牌     |    |
| description    | string | 报修问题描述   |    |
| image          | string | 报修图片地址   |    |
| fault\_type    | string | 问题类型     |    |
| qq             | int    | 用户预留qq号  |    |
| campus         | string | 用户所在校区   |    |

**Response**

{% tabs %}
{% tab title="修改成功" %}
```json
//假如此处仅修改了校区
{
	"success": true,
	"changedFields": {
		"campus": "xxx"
	}
}
```
{% endtab %}
{% endtabs %}

| 属性            | 类型     | 描述     |
| ------------- | ------ | ------ |
| success       | string | 请求是否成功 |
| changedFields | json   | 修改的内容  |

# 头像上传

## 简介

在需要上传头像的地方使用该接口

## &#x20;请求

## 头像上传

<mark style="color:green;">`POST`</mark> `/v1/user/avatar`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性 | 类型       | 描述 | 必填 |
| -- | -------- | -- | -- |
|    | formData |    | 是  |

**Response**

{% tabs %}
{% tab title="上传成功" %}
```json
{
	"success": true,
	"data": "图片地址"
}
```
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述                         |
| ------- | ------ | -------------------------- |
| success | string | 请求是否成功                     |
| data    | string | <p>成功：图片url<br>失败：错误信息</p> |

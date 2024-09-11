# 获取活动信息

## 简介

此接口用于获取活动信息

任何身份的用户都可以获取到活动列表，前提是已通过Bearer鉴权

## &#x20;请求

## 获取活动信息

GET `/v1/status/getEvent`

### **Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

### **Body**

无

### **Response**

{% tabs %}
{% tab title="获取成功" %}
```json
{
  "success": true,
  "activities": [
    {
      "id": "1",
      "name": "测试",
      "type": "大修",
      "description": "你好你好你好",
      "poster": "https://qiniuz1.wjlo.cc/avatar/old/tmp_ae8936097a486d18b3f15445298450ab.jpg",
      "create_time": "2024-09-10 13:55:43",
      "start_time": "2024-09-11 13:55:23",
      "signup_start_time": "2024-09-12 13:55:23",
      "signup_end_time": "2024-09-11 13:55:23"
    }
  ]
}
```
{% endtab %}

{% tab title="获取失败" %}
```json
{
	"success": false,
	"message": "失败原因"
}
```
{% endtab %}
{% endtabs %}

#### 响应参数说明

| 参数名        | 类型      | 必填 | 说明     |
| ---------- | ------- | -- | ------ |
| success    | boolean | 是  | 请求是否成功 |
| activities | array   | 是  | 此活动的信息 |

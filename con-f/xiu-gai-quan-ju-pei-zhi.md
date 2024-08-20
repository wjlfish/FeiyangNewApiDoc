# 修改全局配置

## 简介

此接口用于修改全局配置

仅允许管理员身份的用户修改此配置表的信息

## &#x20;请求

## 修改工单

<mark style="color:green;">`POST`</mark> `/v1/ticket/set`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 参数名  | 类型     | 必填 | 说明        |
| ---- | ------ | -- | --------- |
| name | string | 是  | 要修改的配置的名称 |
| data | string | 是  | 要设置的配置的值  |

**Response**

{% tabs %}
{% tab title="修改成功" %}
```json
//假如此处仅修改了全局报修开关
{
    "success": true,
    "changedFields": {
        "name": "Global_Flag",
        "data": "0"
    }
}
```
{% endtab %}
{% endtabs %}

| 属性            | 类型     | 描述     |
| ------------- | ------ | ------ |
| success       | string | 请求是否成功 |
| changedFields | json   | 修改的内容  |

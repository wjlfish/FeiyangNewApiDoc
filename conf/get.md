# 获取全局配置

## 简介

此接口用于获取全局配置

任何身份的用户都可以获取到这个全局配置，前提是已通过Bearer鉴权

此接口同步运行于：`/v1/status/getConfig 及 /v1/conf/get`

## &#x20;请求

## 获取全局配置

GET `/v1/status/getConfig`

GET `/v1/conf/get`

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
    "configs": [
        {
            "id": 0,
            "name": "Global_Flag",
            "info": "全局报修开关",
            "data": "1"
        },
        {
            "id": 1,
            "name": "Global_Year",
            "info": "全局年份时间",
            "data": "2024"
        },
        // ...更多配置项
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

| 参数名     | 类型      | 必填 | 说明         |
| ------- | ------- | -- | ---------- |
| success | boolean | 是  | 请求是否成功     |
| configs | array   | 是  | 包含所有配置项的数组 |
| id      | int     | 是  | 配置项的编号     |
| name    | string  | 是  | 配置项的名称     |
| info    | string  | 是  | 配置项的描述信息   |
| data    | string  | 是  | 配置项的具体值    |

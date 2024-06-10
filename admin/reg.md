# 注册管理员

## 简介

此接口用于在管理端注册新的管理员

应该注意的是，管理员注册可在config文件的\[info]\[regadmin]开关控制

## &#x20;请求

## 注册管理员

<mark style="color:green;">`POST`</mark> `/v1/admin/reg`

**Headers**

| 属性           | 值                  |
| ------------ | ------------------ |
| Content-Type | `application/json` |

**Body**

| 参数名      | 类型     | 描述              |
| -------- | ------ | --------------- |
| username | string | 管理员用户名          |
| password | string | 密码              |
| openid   | string | 从获取接口获取的 openid |

**Response**

{% tabs %}
{% tab title="注册成功" %}
```json
{
	"success": true,
	"message": "注册成功"
}
```
{% endtab %}

{% tab title="注册失败" %}
```json
{
	"success": false,
	"message": "注册失败"
}
```
{% endtab %}
{% endtabs %}

| 参数名     | 类型      | 描述     |
| ------- | ------- | ------ |
| success | boolean | 请求是否成功 |
| message | string  | 返回的消息  |

####

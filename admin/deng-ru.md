# 登入

## 简介

此接口用于在管理端登入并换取access\_token

## &#x20;请求

## 登入

<mark style="color:green;">`POST`</mark> `/v1/admin/login`

**Headers**

| 属性           | 值                  |
| ------------ | ------------------ |
| Content-Type | `application/json` |

**Body**

| 参数名      | 类型     | 描述     |
| -------- | ------ | ------ |
| username | string | 管理员用户名 |
| password | string | 密码     |

**Response**

| 参数名           | 类型      | 描述            |
| ------------- | ------- | ------------- |
| success       | boolean | 请求是否成功        |
| access\_token | string  | access\_token |
| message       | string  | 返回的消息         |
| user          | object  | 登录成功后的用户信息    |

#### 此接口返回的access\_token必然是管理员身份用户的

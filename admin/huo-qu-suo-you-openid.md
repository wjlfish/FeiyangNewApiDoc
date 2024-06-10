# 获取所有openid

## 简介

由于管理员用户和openid强绑定，所以在注册时需要用到此接口进行openid的获取。所以执行此注册操作时必须以管理员用户的身份发起获取openid的请求。

## &#x20;请求

## 注册管理员

GET `/v1/admin/getopenids`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

Query

**Response**

| 参数名     | 类型      | 描述              |
| ------- | ------- | --------------- |
| success | boolean | 请求是否成功          |
| data    | array   | 包含所有 openid 的数组 |

# 获取技术员业绩

## 简介

此接口可在管理端获取到所有技术员的业绩，并返回完单数最多的技术员及其姓名。

此接口亦可以在用户端获取到本人的业绩。

与其他接口同理，获取所有业绩时需要以管理员用户发起请求；本人业绩需要以本人身份发起请求

## &#x20;请求

## 获取技术员业绩

GET `/v1/status/getTechworks`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

Query

| 参数名             | 类型  | 必须 | 描述                |
| --------------- | --- | -- | ----------------- |
| `technician_id` | int | 否  | 请求者的技术员ID（通过鉴权验证） |

**Response**

**1.获取全部技术员**

| 参数名                      | 类型     | 描述              |
| ------------------------ | ------ | --------------- |
| `max_id`                 | int    | 出现次数最多的技术员 ID   |
| `max_realname`           | string | 出现次数最多的技术员的真实姓名 |
| `technicians`            | array  | 包含所有有过完成工单的信息数  |
| `technicians[].tid`      | int    | 技术员 ID          |
| `technicians[].count`    | int    | 技术员完成工单数        |
| `technicians[].realname` | string | 技术员的真实姓名        |
| success                  | bool   | 请求是否成功          |

2.获取本人业绩

| 参数名      | 类型     | 描述       |
| -------- | ------ | -------- |
| success  | bool   | 请求是否成功   |
| `tid`    | int    | 技术员 ID   |
| count    | int    | 完成工单数    |
| realname | string | 技术员的真实姓名 |

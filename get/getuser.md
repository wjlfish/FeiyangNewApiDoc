# 获取用户信息

## 简介

此接口用于获取一个或多个用户的信息

此接口支持多种用户角色，通过多种方式获取用户的信息

## &#x20;请求

## 获取用户

GET `/v1/status/getUser`

### **Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

### **Body**

| 属性        | 类型     | 描述        | 必填 |
| --------- | ------ | --------- | -- |
| uid       | string | 用户 ID     | 否  |
| openid    | string | 用户 OpenID | 否  |
| phone     | string | 用户手机号     | 否  |
| email     | string | 用户邮箱      | 否  |
| campus    | string | 校区        | 否  |
| role      | string | 用户角色      | 否  |
| available | int    | 技术员可用状态   | 否  |
| page      | int    | 页码        | 否  |

默认单次最多返回10条数据

以上所有参数都非必填，page未填时，默认为第一页

这里列举了一些可能出现的请求组合，请按需注入参数：

**1. 普通用户获取自身数据**

普通用户只能获取与自身相关的数据，包括通过 `uid`、`openid`、`phone`、`email` 等参数获取自身的数据。

* **通过 `uid` 获取自身数据**
  * 请求：`GET /v1/status/getUser?uid=123`
  * 条件：`uid` 必须与 请求发起者的 相同
* **通过 `openid` 获取自身数据**
  * 请求：`GET /v1/status/getUser?openid=o_y1r1=vbi100ood1`
  * 条件：`openid` 必须与 请求发起者的 相同
* **通过 `phone` 获取自身数据**
  * 请求：`GET /v1/status/getUser?phone=123456789011`
  * 条件：`phone` 必须与 请求发起者的 相同
* **通过 `email` 获取自身数据**
  * 请求：`GET /v1/status/getUser?email=wjl@wjlo.cc`
  * 条件：`email` 必须与 请求发起者的 相同

**2. 管理员获取特定用户数据**

管理员可以根据特定条件获取用户数据，包括通过 `uid`、`openid`、`phone`、`email`、`campus`、`role`、`available` 等参数。

* **通过 `uid` 获取用户数据**
  * 请求：`GET /v1/status/getUser?uid=123`
* **通过 `openid` 获取用户数据**
  * 请求：`GET /v1/status/getUser?openid=o_y1r1=vbi100ood1`
* **通过 `phone` 获取用户数据**
  * 请求：`GET /v1/status/getUser?phone=123456789011`
* **通过 `email` 获取用户数据**
  * 请求：`GET /v1/status/getUser?email=wjl@wjlo.cc`
* **通过 `campus` 获取用户数据**
  * 请求：`GET /v1/status/getUser?campus=江安`
* **通过 `role` 获取用户数据**
  * 请求：`GET /v1/status/getUser?role=user`
* **通过 `available` 获取用户数据**
  * 请求：`GET /v1/status/getUser?available=1` 或 `GET /v1/status/getUser?available=0`

**3. 分页获取用户数据**

管理员可以分页获取用户数据，使用 `page` 参数来指定页码。

* **分页获取用户数据**
  * 请求：`GET /v1/status/getUser?page=1`
  * 请求：`GET /v1/status/getUser?page=2`

**4. 管理员根据多条件组合获取用户数据**

管理员可以组合多个查询参数来获取用户数据。

* **根据 `campus` 和 `role` 获取用户数据**
  * 请求：`GET /v1/status/getUser?campus=North&role=user&page=1`
* **根据 `available` 和 `role` 获取用户数据**
  * 请求：`GET /v1/status/getUser?available=1&role=admin&page=2`

**5. 普通用户获取自身相关数据的组合查询**

普通用户可以组合多个自身相关的查询参数，但只能获取与自身相关的数据。

* **通过 `uid` 和 `openid` 获取自身数据**
  * 请求：`GET /v1/status/getUser?uid=123&openid=o_y1r1=vbi100ood1`
* **通过 `phone` 和 `email` 获取自身数据**
  * 请求：`GET /v1/status/getUser?phone=1234567890&email=wjl@wjlo.cc`

**6. 获取全部用户数据（仅限管理员）**

管理员可以获取全部用户数据，并可以分页获取以控制服务器压力。

* **获取全部用户数据**
  * 请求：`GET /v1/status/getUser`
* **分页获取全部用户数据**
  * 请求：`GET /v1/status/getUser?page=1`
  * 请求：`GET /v1/status/getUser?page=2`
* **根据 `campus` 获取全部用户数据**
  * 请求：`GET /v1/status/getUser?campus=江安`
* **根据 `role` 获取全部用户数据**
  * 请求：`GET /v1/status/getUser?role=user`
* **根据 `available` 获取全部用户数据**
  * 请求：`GET /v1/status/getUser?available=1` 或 `GET /v1/status/getUser?available=0`
* **根据多条件组合获取全部用户数据**
  * 请求：`GET /v1/status/getUser?campus=江安&role=user&available=1&page=1`

### **Response**

除网络错误外，所有错误类型都是因为权限不足。如果你遇到了权限不足的报错，请检查权限是否完整。

对于Bearer有关的错误（401），请查阅[前期准备](../get\_started/prepare.md#accesstoken-xin-xi-chu-li)[-Access\_token 信息处理](../get\_started/prepare.md#accesstoken-xin-xi-chu-li)

{% hint style="info" %}
获取全部用户时，需要确保发起请求的用户身份为管理员
{% endhint %}

{% tabs %}
{% tab title="获取成功" %}
```json
{
  "request_type": "by_user_id_pending",
  "data": [
    {
      "id": 1,
      "user_id": 12322,
      "machine_purchase_date": "2024-06-01",
      "user_phone": "123456789",
      "device_type": "笔记本",
      "computer_brand": "华为Matebook",
      "repair_description": "请帮我请个灰",
      "repair_status": "Pending",
      "repair_image_url": "https://example.com/image.jpg",
      "fault_type": "清灰",
      "qq_number": "123456",
      "campus": "江安",
      "assigned_technician_id": 12311,
      "assigned_time": "2024-06-10 12:00:00",
      "completion_time": null
    },
    //可能还有其他工单，所以这里json我写的是逗号
  ],
  "page": 2,
  "limit": 10
}

```
{% endtab %}

{% tab title="获取失败" %}
```json
{
	"success": false,
	"requesttype": "",
	"data": "权限不足"
}
```
{% endtab %}
{% endtabs %}

#### 返回数据说明

| 属性                | 类型     | 描述        |
| ----------------- | ------ | --------- |
| success           | bool   | 请求是否成功    |
| requesttype       | string | 请求类型      |
| data              | array  | 用户数据数组    |
| data\[].id        | int    | 用户 ID     |
| data\[].name      | string | 用户名       |
| data\[].openid    | string | 用户 OpenID |
| data\[].phone     | string | 用户手机号     |
| data\[].email     | string | 用户邮箱      |
| data\[].campus    | string | 用户校区      |
| data\[].role      | string | 用户角色      |
| data\[].available | bool   | 用户可用状态    |
| page              | int    | 当前页码      |
| limit             | int    | 每页返回的数据条数 |

####


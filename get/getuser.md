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

对于Bearer有关的错误（401），请查阅[前期准备](../get_started/prepare.md#accesstoken-xin-xi-chu-li)[-Access\_token 信息处理](../get_started/prepare.md#accesstoken-xin-xi-chu-li)

{% hint style="info" %}
获取全部用户时，需要确保发起请求的用户身份为管理员
{% endhint %}

{% tabs %}
{% tab title="获取成功" %}
```json
{
	"success": true,
	"request_type": "all_users",
	"data": [
		{
			"id": "100000",
                        "openid": "system",
                        "token_expiry": "2024-12-25 22:50:38",
                        "regtime": "2024-05-01 00:00:00",
                        "nickname": "系统",
                        "realname": "系统",
                        "avatar": "https://qncdn.feiyang.ac.cn/avatar/446f09e0-1020-4178-9592-ede0fba3ac58.jpg",
                        "campus": "虚空",
                        "role": "admin",
                        "last_time": null,
                        "available": "5",
                        "wants": "c",
                        "email": "noreply@feiyang.ac.cn",
                        "temp_email": null,
                        "email_status": "verified",
                        "phone": null,
                        "status": "verified",
                        "immed": "1"
                  	"status": "verified"
		}
	]
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

<table><thead><tr><th>属性</th><th width="248">类型</th><th>描述</th></tr></thead><tbody><tr><td>success</td><td>bool</td><td>请求是否成功</td></tr><tr><td>requesttype</td><td>string</td><td>请求类型</td></tr><tr><td>data</td><td>array</td><td>用户数据数组</td></tr><tr><td>data[].id</td><td>int</td><td>用户 ID</td></tr><tr><td>data[].name</td><td>string</td><td>用户名</td></tr><tr><td>data[].openid</td><td>string</td><td>用户 OpenID</td></tr><tr><td>data[].phone</td><td>string</td><td>用户手机号</td></tr><tr><td>data[].email</td><td>string</td><td>用户邮箱</td></tr><tr><td>data[].campus</td><td>string</td><td>用户校区</td></tr><tr><td>data[].role</td><td>string</td><td>用户角色</td></tr><tr><td>data[].available</td><td>bool</td><td>用户可用状态</td></tr><tr><td>page</td><td>int</td><td>当前页码</td></tr><tr><td>limit</td><td>int</td><td>每页返回的数据条数</td></tr></tbody></table>

####


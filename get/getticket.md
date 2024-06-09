# 获取工单信息

## 简介

此接口用于获取一个或多个工单的信息

此接口支持多种用户角色，通过多种方式获取工单的信息

## &#x20;请求

## 获取工单

GET `/v1/status/getTicket`

### **Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

### **Body**

| 属性      | 类型     | 描述     | 必填 |
| ------- | ------ | ------ | -- |
| orderid | int    | 工单ID   | 否  |
| uid     | int    | 用户ID   | 否  |
| tid     | int    | 技术员ID  | 否  |
| list    | string | 工单状态过滤 | 否  |
| page    | int    | 分页页码   | 否  |

默认单次最多返回10条数据

以上所有参数都非必填，page未填时，默认为第一页

这里列举了所有可能出现的请求组合，请按需注入参数：

* **查询所有工单信息**
  * 示例请求：`GET /v1/status/getTicket`
  * 描述：查询系统中的所有工单信息
* **通过工单ID查询工单信息**
  * 请求参数：`orderid`
  * 示例请求：`GET /v1/status/getTicket?orderid=123`
  * 描述：根据指定的工单ID查询该工单的详细信息
* **通过用户ID查询工单信息**
  * 请求参数：`uid`
  * 示例请求：`GET /v1/status/getTicket?uid=456`
  * 描述：根据指定的用户ID查询与该用户相关的工单信息
* **通过技术员ID查询工单信息**
  * 请求参数：`tid`
  * 示例请求：`GET /v1/status/getTicket?tid=789`
  * 描述：根据指定的技术员ID查询与该技术员相关的工单信息
* **查询特定状态的工单信息**
  * 请求参数：`list`
  * 示例请求：`GET /v1/status/getTicket?list=pending`
  * 描述：查询系统中指定状态的工单信息，可选状态为`pending`（未完成的工单）和`done`（已完成的工单）
* **分页查询工单信息**
  * 请求参数：`page`
  * 示例请求：`GET /v1/status/getTicket?page=2`
  * 描述：分页查询工单信息，指定返回结果的页码
* **组合查询**
  * 可以组合使用以上参数，例如：
    * 查询特定用户的未完成工单：`GET /v1/status/getTicket?uid=456&list=pending`
    * 查询特定技术员的所有工单并进行分页：`GET /v1/status/getTicket?td=789&page=2`
    * 查询特定状态的所有工单：`GET /v1/status/getTicket?list=done&page=3`

### **Response**

除网络错误外，所有错误类型都是因为权限不足。如果你遇到了权限不足的报错，请检查权限是否完整。

对于Bearer有关的错误（401），请查阅[前期准备](../getin/qian-qi-zhun-bei.md#accesstoken-xin-xi-chu-li)[-Access\_token 信息处理](../getin/qian-qi-zhun-bei.md#accesstoken-xin-xi-chu-li)

{% hint style="info" %}
使用uid查询时，需要确保发起请求的用户就是uid拥有者 或 身份为管理员

使用tid查询时，需要确保发起请求的用户就是tid拥有者 或 身份为管理员

获取全部工单时，需要确保发起请求的用户身份为管理员
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

| 属性            | 类型     | 描述                                                |
| ------------- | ------ | ------------------------------------------------- |
| status        | string | 是否获取成功                                            |
| request\_type | string | 请求类型，指示返回的数据是按工单ID查询、按用户ID查询、按技术员ID查询、获取所有工单中的哪一种 |
| data          | array  | 包含工单信息的数组，每个元素包含工单的详细信息                           |
| page          | int    | 当前页码                                              |
| limit         | int    | 每页的记录数                                            |

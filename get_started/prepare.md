# 前期准备

## 开发准备 <a href="#b75bc" id="b75bc"></a>

在使用该API的能力开发应用前，请注意：

1. 调用服务端接口时，需使用 HTTPS 协议、JSON 数据格式、UTF-8 编码，POST 请求请在 HTTP Header 中设置 Content-Type:application/json。
2. **API接口**域名为：https://focapi.feiyang.ac.cn
3. **公共访问**域名为：https://focapp.feiyang.ac.cn/public

**API接口**域名是对接api时普遍使用的域名，在本文档的其他部分，除特殊情况外，此域名被认为是默认域名，给出的对应接口需与此接口域名组合使用。

**公共访问**域名是用于用户访问公共资源的域名，一般是在前端被直接访问或调用的内容。包括但不限于图片、网页静态资源及部分可供浏览器直接点击的网页。对接此api时，你大概率用不上这个域名，但是需要注意与API接口域名的区分。

## 安全注意 <a href="#qsd6q" id="qsd6q"></a>

access\_token 代表调用接口的授权凭证，不要泄露给他人，滥用会触发风控。在我们的理想开发中，access\_token是在每一次请求中被携带的header参数。access\_token的权限极高，对于某个普通用户，拥有其access\_token则代表在该token的有效时间内，你有权限修改该用户的全部信息及内容（包括注销该账户）；对于管理员用户，其access\_token的泄露更是灾难级的，严重时可能导致本系统完全崩溃。所以请开发者在使用access\_token时严格遵循鉴权要求。

## 接口身份校验（鉴权） <a href="#gnvxc" id="gnvxc"></a>

API 的 HTTP 调用，需在 Header 中传递 Authorization 参数，值为 Bearer + 空格 + access\_token。

示例：

```
curl --location --request POST 'API接口域名/v1/user/setuser' \
--header 'Authorization: Bearer access_token' \
--header 'Content-Type: application/json' \
--data-raw '{
    "phone": "18000000000",
    "verification_code": "666666"
}'
```

## 接口成功/失败判断 <a href="#wigh4" id="wigh4"></a>

所有 API 使用 HTTP 状态码 2xx 标识成功响应。失败响应会返回非 2xx HTTP 状态码，并统一返回错误信息，建议开发者日志记录，以方便排查问题。具体错误信息在每个接口的文档中都有阐释，此处就不举例介绍了。

## Access\_token 信息处理&#x20;

access\_token的有效期是一小时，在这一小时内，你可以发起无数次请求。对于状态正常的access\_token，我们的接口都可以正常处理请求。在access\_token状态异常时，你会收到服务器返回的401状态码并伴随错误消息，具体会分为以下几类：

1. 在Header中未收到Authorization的字段，访问接口会得到以下报错：

```json
{
	"error": "Unauthorized for no Authorization"
}
```

2. 设置了Authorization，但Authorization中不包含Bearer的内容，访问接口会得到以下报错：

```json
{
	"error": "Unauthorized for no Bearer"
}
```

3. 在50次请求满或一小时时间到后，访问接口会得到以下报错：

```json
{
	"error": "token_expired"
}
```

如果你遇到了第3种或其他的报错，说明该access\_token已经失效。你需要重新通过 [接入接口](wx\_login.md) 获取新的access\_token。

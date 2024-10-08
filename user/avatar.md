# 头像上传

## 简介

在需要上传头像的地方使用该接口

## &#x20;请求

## 头像上传

<mark style="color:green;">`POST`</mark> `/v1/user/avatar`

**Headers**

| 属性            | 值                      |
| ------------- | ---------------------- |
| Content-Type  | `application/json`     |
| Authorization | Bearer {access\_token} |

**Body**

| 属性 | 类型       | 描述 | 必填 |
| -- | -------- | -- | -- |
|    | formData |    | 是  |

这里的上传方式可能不太便于理解，我将给出一个js示例：（假设点击某#uploadButton按钮）

```javascript
// 获取文件输入元素
const fileInput = document.querySelector('#avatarInput');

// 监听文件上传事件
document.querySelector('#uploadButton').addEventListener('click', () => {
    const file = fileInput.files[0];
    if (file) {
        const formData = new FormData();
        formData.append('file', file);

        // 调用上传接口
        fetch(app-globalData.rootApiUrl+ "/v1/user/avatar", {
            method: 'POST',
            body: formData,
            headers: {
                'Authorization': 'Bearer ' + token,
            }
        })
        .then(response => response.json())
        .then(data => {
            if (data.success) {
                console.log('上传成功:', data.data);
            } else {
                console.error('上传失败:', data.Data);
            }
        })
        .catch(error => {
            console.error('请求错误:', error);
        });
    } else {
        console.error('请先选择文件');
    }
});
```

**Response**

{% tabs %}
{% tab title="上传成功" %}
```json
{
	"success": true,
	"data": "图片地址"
}
```
{% endtab %}
{% endtabs %}

| 属性      | 类型     | 描述                         |
| ------- | ------ | -------------------------- |
| success | string | 请求是否成功                     |
| data    | string | <p>成功：图片url<br>失败：错误信息</p> |

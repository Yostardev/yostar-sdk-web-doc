# Yostar Account 文档

| 归档日期 | 版本 | 说明 | 作者 | 审批人 |
| :---: | :---: | :---: |  :---: | :---: |
| 2019-2-20 | V1.0.0 | 初稿 |   |   |

### 安装
```html
<script src="js/yo_acc.js"></script>
```

#### Js 使用 
```javascript
var Yo = windows.Yo;
```

### Api 请求方式
```html
Yo.api(params, callback)
```
### 请求 params 参数
| Api | params参数 | 类型 | 说明 |
| :---: | :---: | :---: | :---: |
| Yo.request(params, callback) | account | string | 电子邮箱  |
| Yo.submit(params, callback)  | account | string | 电子邮箱  |
|                              | code    | string | 验证码    |
| Yo.debug(params, callback)   | uid     | string | 用户id    |
|                              | token   | string | 用户token |



### 返回 callbackResult 参数

| callbackResult参数 | 类型 | 说明 | Api |
| :---: | :---: | :---: | :---: | 
| code | number | 返回code  | Yo.request<br> |
| data | object | 返回数据  | Yo.request |
| message  | string | 提示信息    | Yo.request |

### 返回 callbackResult.code 参数
| code | 说明 |
| :---: | :---: | 
| 20000 | 成功 | 
| 30001 | account错误 |
| 50003 | account邮箱验证频率过快 |
| 50004 | account被封 |
| 50016 | account验证码验证失败 |
| 50009 | account验证码到达失败限制 |
| 50005 | uid,Token验证失败 |

### 返回 callbackResult.data 参数

| callbackResult参数 | 类型 | 说明 | Api |
| :---: | :---: | :---: | :---: | 
| uid | string | 返回uid数据  | Yo.submit, Yo.debug |
| account | string | 返回account数据  | Yo.submit, Yo.debug |
| token  | string | 返回token数据    | Yo.submit, Yo.debug |



### 请求 api 样例
```javascript
  let account = 'test@gmail.com';
  let data0 = await Yo.request({
    account: account
  });
  if (data0.code != 20000) {
    return console.error(data0);
  } else {
    console.log(' > SUCCESS');
  }
```

### 服务端验证 uid, token
> ```
> 发送uid,token到 https://uc.yo-star.com:3020/account/debug_token
> 返回 callbackResult
> ```
```bash
样例
curl --request POST \
  --url https://uc.yo-star.com:3020/account/debug_token \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --data 'uid=11912523927&token=11912523927-S8jvAb56gAQ5XKozEdVTMiQGHYwfQvZgixMSLq2XbX6C8uNySpdiuTjdmZwMdQCBxkjTYjXkDuBzzUlyK11UVg'
```

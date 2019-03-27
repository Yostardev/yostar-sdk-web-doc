# Majsoul应用接口

> [测试服务器地址](#测试服务器地址)  
> [安装示例](#安装示例)  
> [Twitter登录请求](#Twitter登录请求)  
> [Facebook登录请求](#Facebook登录请求)  
> [Google登录请求](#Google登录请求)  
> [Yostar账号登录请求](#Yostar账号登录请求)  
> [执行登录](#执行登录)  
> [验证uid,accessToken](#验证uid,accessToken)  
> [正式部署](#正式部署)  


## 测试服务器地址
* 服务器地址 [https://passporttest.mahjongsoul.com](https://passporttest.mahjongsoul.com)
* 浏览器Javascript文件 yo_acc.stg_ja.js  
* 令牌文件服务器地址 [https://pt01.mul-pay.jp/ext/js/token.js](https://pt01.mul-pay.jp/ext/js/token.js)
* ShopID: tshop00037465


## 安装示例
```javascript
/**
    window.Yo
*/
<script src="${服务器地址}/js/${浏览器Javascript文件}"></script>
/**
    window.Multipayment
*/
<script src="${令牌文件服务器地址}"></script>
```


## Twitter登录请求
```javascript
Yo.twitterAuth({
    redirect_uri: this.redirect_uri,
    openNewWindow: this.openNewWindow > 0
});
```
请求方法： Yo.twitterAuth  

|     参数      |  类型  |           说明           |
| :-----------: | :----: | :----------------------: |
| redirect_uri  | 字符串 | 登录返回跳转地址不带参数 |
| openNewWindow |  整数  |      是否新窗口打开      |
返回值地址栏GET参数：  

| 参数  |  类型  |   说明    |
| :---: | :----: | :-------: |
|  uid  | 字符串 |  用户uid  |
| token | 字符串 | 登录token |


## Facebook登录请求
```javascript
Yo.facebookAuth({
    redirect_uri: this.redirect_uri,
    openNewWindow: this.openNewWindow > 0
});
```
请求方法： Yo.facebookAuth  

|     参数      |  类型  |           说明           |
| :-----------: | :----: | :----------------------: |
| redirect_uri  | 字符串 | 登录返回跳转地址不带参数 |
| openNewWindow |  整数  |      是否新窗口打开      |
返回值地址栏GET参数：  

| 参数  |  类型  |   说明    |
| :---: | :----: | :-------: |
|  uid  | 字符串 |  用户uid  |
| token | 字符串 | 登录token |

> Facebook登录测试账号：  
> 登录名：epmyazwbux_1553655623@tfbnw.net  
> 密码：txODzEUfJqTq6Ssa  


## Google登录请求
```javascript
Yo.googleAuth({
    redirect_uri: this.redirect_uri,
    openNewWindow: this.openNewWindow > 0
});
```
请求方法： Yo.googleAuth  

|     参数      |  类型  |           说明           |
| :-----------: | :----: | :----------------------: |
| redirect_uri  | 字符串 | 登录返回跳转地址不带参数 |
| openNewWindow |  整数  |      是否新窗口打开      |
返回值地址栏GET参数：  

| 参数  |  类型  |   说明    |
| :---: | :----: | :-------: |
|  uid  | 字符串 |  用户uid  |
| token | 字符串 | 登录token |


## Yostar账号登录请求
* 请求验证
```javascript
Yo.request({
    account: 'test@example.com'
}).then(function(data) {
    // data.result
})
```
请求方法： Yo.request  

|  参数   |  类型  | 说明  |
| :-----: | :----: | :---: |
| account | 字符串 | 邮箱  |

返回值:  

|  参数  | 类型  |                           说明                            |
| :----: | :---: | :-------------------------------------------------------: |
| result | 整数  | 0：成功，<br>50003:邮箱发送频率上限,<br>50004:account被封 |

* 提交验证
```javascript
Yo.submit({
    account: 'test@example.com',
    code: '112233',
}).then(function(data) {
    // data.result
    // data.uid
    // data.token
})
```
请求方法：Yo.submit  

|  参数   |  类型  |    说明    |
| :-----: | :----: | :--------: |
| account | 字符串 |    邮箱    |
|  code   | 字符串 | 邮箱验证码 |
返回值:  

|  参数  |  类型  |                                 说明                                 |
| :----: | :----: | :------------------------------------------------------------------: |
| result |  整数  | 0：成功，<br>50016：失败,超时，或验证码不一致,<br>50009:失败次数过多 |
|  uid   | 字符串 |                               用户uid                                |
| token  | 字符串 |                              登录token                               |


## 执行登录
请求方法：Yo.login  

| 参数  |  类型  |       说明       |
| :---: | :----: | :--------------: |
|  uid  | 字符串 | uid(用户id,唯一) |
| token | 字符串 |    登录token     |

返回值:  

|    参数     |  类型  |                                                  说明                                                   |
| :---------: | :----: | :-----------------------------------------------------------------------------------------------------: |
|   result    |  整数  | 0：成功，<br>1:验证失败，uid和token不匹配,<br>2:IP访问被限制,<br>~~3:设备号被封禁,~~<br>4:该UID已被封禁 |
| accessToken | 字符串 |                              每次登录生成的accessToken，用于支付及其他请求                              |


## 验证uid,accessToken
请求地址: ${服务器地址}/user/check  
请求方法: POST    

|    参数     |  类型  |         说明          |
| :---------: | :----: | :-------------------: |
|     uid     | 字符串 |          uid          |
| accessToken | 字符串 | 登录获取的accessToken |
返回值:  

| 参数  |  类型  |            说明             |
| :---: | :----: | :-------------------------: |
| state |  整数  |       1：成功,99:失败       |
|  msg  | 字符串 | SUCCESS:成功, INVALID：失败 |



## 正式部署
* 服务器地址 [https://passport.mahjongsoul.com](https://passport.mahjongsoul.com)
* 浏览器Javascript文件 yo_acc.prod_ja.js  
* 令牌文件服务器地址 [https://p01.mul-pay.jp/ext/js/token.js](https://p01.mul-pay.jp/ext/js/token.js)
* ShopID: tshop00037465


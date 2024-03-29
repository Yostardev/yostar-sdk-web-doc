# Majsoul应用接口

<div style="display:none;">
<!-- https://yostardev.github.io/yostar-sdk-web-doc/#/ZH/YostarSDKWebDoc -->
</div>

| 日期         | 版本      | 说明                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|:-----------|:--------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 2021-11-05 | v1.01   | 新增 执行登录 返回值:5；新增 删除用户；新增 恢复等待删除的用户                                                                                                                                                                                                                                                                                                                                                                                                     |
| 2022-01-27 | v2.1.61 | 新增:获取问卷                                                                                                                                                                                                                                                                                                                                                                                                                                |
| 2022-07-12 | v2.1.65 | 新增:[日服PayPay支付](#日服PayPay支付) ,邮件语言新增支持kr表示韩语, 增加备注[日服Paypal支付](#日服Paypal支付)、[日服Au支付](#日服Au支付)、[日服Docomo支付](#日服Docomo支付)、[日服Softbank支付](#日服Softbank支付)                                                                                                                                                                                                                                                                                  |
| 2022-08-26 | v2.1.66 | <div style="font-weight:bold;">是否需要调用游戏实名认证需要Web端游戏判断是否韩服；</div>增加[执行登录](#执行登录)接口返回值kr_kmc_status; 增加[日服通用创建订单参数](#日服通用创建订单参数)返回值result （韩服创建订单时出现错误返回） ；<br/> 增加[当前账号韩国实名认证信息](#当前账号韩国实名认证信息)；增加[发起韩国实名认证](#发起韩国实名认证)；<br/> 增加[韩服信用卡Stripe渠道支付](#韩服信用卡Stripe渠道支付)；增加[韩服Paypal支付](#韩服Paypal支付);<br/> 增加[Twitter韩国登录请求](#Twitter韩国登录请求); 增加[Facebook韩国登录请求](#Facebook韩国登录请求)；增加[Google韩国登录请求](#Google韩国登录请求)                            |
| 2022-11-22 | v2.2.0  | 韩服创建订单新增realMoney参数,对应返回code=90005, 获取问卷增加参数 gameNotifyURL                                                                                                                                                                                                                                                                                                                                                                             |
| 2023-03-03 | v2.4.0  | 增加创建日美韩服订单的参数[operation_description](#operation_description) <br/>日服增加创建银行直接支付，新增：<br/> [银行绑定发送SMS验证](#银行绑定发送SMS验证)<br/>[银行绑定提交SMS验证](#银行绑定提交SMS验证)<br/>[银行绑定信息添加](#银行绑定信息添加)<br/>[银行绑定信息获取银行列表](#银行绑定信息获取银行列表)<br/>[发起银行绑定用户跳转页面](#发起银行绑定用户跳转页面)<br/>[银行绑定获取手机号银行信息](#银行绑定获取手机号银行信息)<br/>[发送解绑银行短信验证码](#发送解绑银行短信验证码)<br/>[验证短信验证码解绑银行](#验证短信验证码解绑银行)<br/>[银行绑定账号创建订单](#银行绑定账号创建订单)<br/>[银行绑定账号支付订单时发送短信验证码](#银行绑定账号支付订单时发送短信验证码)<br/> |

> [测试服务器地址](#测试服务器地址)  
> [安装示例](#安装示例)  
> [Twitter登录请求](#Twitter登录请求)  
> [Twitter日本登录请求](#Twitter日本登录请求)  
> [Twitter韩国登录请求](#Twitter韩国登录请求)  
> [Facebook登录请求](#Facebook登录请求)  
> [Facebook韩国登录请求](#Facebook韩国登录请求)  
> [Google登录请求](#Google登录请求)  
> [Google韩国登录请求](#Google韩国登录请求)  
> [Google日本登录请求](#Google日本登录请求)  
> [Yostar账号登录请求](#Yostar账号登录请求)  
> [Yostar邮箱账号绑定已有账号请求流程](#Yostar邮箱账号绑定已有账号请求流程)  
> [Yostar邮箱账号解绑](#Yostar邮箱账号解绑)  
> [通用跳转登录返回参数](#通用跳转登录返回参数)  
> [执行登录](#执行登录)  
> [执行登录v2](#执行登录v2)  
> [验证uid,accessToken](#验证uid,accessToken)  
> [删除用户](#删除用户)  
> [恢复等待删除的用户](#恢复等待删除的用户)  
> [获取问卷](#获取问卷)
> [当前账号韩国实名认证信息](#当前账号韩国实名认证信息)
> [发起韩国实名认证](#发起韩国实名认证)



> [支付流程图](#支付流程图)


> [银行绑定发送SMS验证](#银行绑定发送SMS验证)
> [银行绑定提交SMS验证](#银行绑定提交SMS验证)
> [银行绑定信息添加](#银行绑定信息添加)
> [银行绑定信息获取银行列表](#银行绑定信息获取银行列表)
> [发起银行绑定用户跳转页面](#发起银行绑定用户跳转页面)
> [银行绑定获取手机号银行信息](#银行绑定获取手机号银行信息)
> [发送解绑银行短信验证码](#发送解绑银行短信验证码)
> [验证短信验证码解绑银行](#验证短信验证码解绑银行)
> [银行绑定账号创建订单](#银行绑定账号创建订单)
> [银行绑定账号支付订单时发送短信验证码](#银行绑定账号支付订单时发送短信验证码)

> [日服浏览器CreditCard支付](#日服浏览器CreditCard支付)  
> [日服Paypal支付](#日服Paypal支付)  
> [日服Au支付](#日服Au支付)  
> [日服Docomo支付](#日服Docomo支付)  
> [日服Softbank支付](#日服Softbank支付)  
> [日服PayPay支付](#日服PayPay支付)  
> [日服WebMoney支付](#日服WebMoney支付)  
> [日服浏览器CreditCard支付2020软银](#日服浏览器CreditCard支付2020软银)  
> [日服Paypal支付2020软银](#日服Paypal支付2020软银)  
> [日服Au支付2020软银](#日服Au支付2020软银)  
> [日服Docomo支付2020软银](#日服Docomo支付2020软银)  
> [日服Softbank支付2020软银](#日服Softbank支付2020软银)  
> [日服通用创建订单参数](#日服通用创建订单参数)  
> [日服支付通知](#日服支付通知)

> [美服Paypal支付](#美服Paypal支付)  
> [美服MasterCard支付](#美服MasterCard支付)  
> [美服Visa支付](#美服Visa支付)  
> [美服JCB支付](#美服JCB支付)  
> [美服支付宝支付](#美服支付宝支付)

> [美服信用卡Stripe渠道支付](#美服信用卡Stripe渠道支付)  
> [美服支付宝Stripe渠道支付](#美服支付宝Stripe渠道支付)

> [美服通用创建订单参数](#美服通用创建订单参数)  
> [美服支付通知](#美服支付通知)

> [韩服信用卡Stripe渠道支付](#韩服信用卡Stripe渠道支付)
> [韩服Paypal支付](#韩服Paypal支付)

> [Yo.execOrder额外参数](#Yo.execOrder额外参数)

> [通用查询订单](#通用查询订单)  
> [正式部署](#正式部署)

> [其他返回值](#其他返回值)



## 测试服务器地址
通用：
* 服务器地址 [https://passporttest.mahjongsoul.com](https://passporttest.mahjongsoul.com)
* 浏览器Javascript文件 yo_acc.stg_ja.js

日服：
* 令牌文件服务器地址 [https://pt01.mul-pay.jp/ext/js/token.js](https://pt01.mul-pay.jp/ext/js/token.js)
* 令牌文件服务器地址，新地址，具有提高的响应速度 [https://stg.static.mul-pay.jp/ext/js/token.js](https://stg.static.mul-pay.jp/ext/js/token.js)
* ShopID: tshop00037465

美服：
* checkoutShopperUrl：[https://checkoutshopper-test.adyen.com](https://checkoutshopper-test.adyen.com)



## 安装示例
```javascript
/**
 window.Yo
 */
<script src="${服务器地址}/js/${浏览器Javascript文件}"></script>

/**
 日服信用卡支付：
 window.Multipayment
 */
<script src="${令牌文件服务器地址}"></script>

/**
 美服信用卡支付：
 window.AdyenCheckout
 */
<link rel="stylesheet" href="<%= checkoutShopperUrl %>/checkoutshopper/sdk/2.1.0/adyen.css" />
<script src="<%= checkoutShopperUrl %>/checkoutshopper/sdk/2.1.0/adyen.js"></script>
```


## Twitter登录请求
```javascript
Yo.twitterAuth({
   redirect_uri: this.redirect_uri,
   openNewWindow: this.openNewWindow > 0
});
Yo.twitterAuth({
   redirect_uri: this.redirect_uri_2,
   openNewWindow: this.openNewWindow > 0,
   version: 2,
});
```
请求方法： Yo.twitterAuth

|     参数      |  类型  |                说明                 |
| :-----------: | :----: | :---------------------------------: |
| redirect_uri  | 字符串 |      登录返回跳转地址不带参数       |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |
|    version    |  整数  | 可选，版本号，取值：2  ，缺省值：1  |

返回值，见 [通用跳转登录返回参数](#通用跳转登录返回参数)

## Twitter韩国登录请求
请求方法： Yo.twitterKrAuth  
参数与 [Twitter登录请求](#Twitter登录请求) 相同

## Twitter日本登录请求
```javascript
Yo.twitterJaAuth({
    redirect_uri: this.redirect_uri,
    openNewWindow: this.openNewWindow > 0
});
Yo.twitterJaAuth({
    redirect_uri: this.redirect_uri_2,
    openNewWindow: this.openNewWindow > 0,
    version: 2,
});
```
请求方法： Yo.twitterJaAuth

参数说明见[Twitter登录请求](#Twitter登录请求)

返回值，见 [通用跳转登录返回参数](#通用跳转登录返回参数)

## Facebook登录请求
```javascript
Yo.facebookAuth({
    redirect_uri: this.redirect_uri,
    openNewWindow: this.openNewWindow > 0
});
Yo.facebookAuth({
    redirect_uri: this.redirect_uri_2,
    openNewWindow: this.openNewWindow > 0,
    version: 2,
});
```
请求方法： Yo.facebookAuth

|     参数      |  类型  |           说明           |
| :-----------: | :----: | :----------------------: |
| redirect_uri  | 字符串 | 登录返回跳转地址不带参数 |
| openNewWindow |  整数  |      是否新窗口打开      |
|    version    |  整数  | 可选，版本号，取值：2  ，缺省值：1  |

返回值，见 [通用跳转登录返回参数](#通用跳转登录返回参数)

> Facebook登录测试账号：  
> 登录名：epmyazwbux_1553655623@tfbnw.net  
> 密码：txODzEUfJqTq6Ssa

## Facebook韩国登录请求
请求方法： Yo.facebookKrAuth  
参数与 [Facebook登录请求](#Facebook登录请求) 相同


## Google登录请求
```javascript
Yo.googleAuth({
    redirect_uri: this.redirect_uri,
    openNewWindow: this.openNewWindow > 0
});
Yo.googleAuth({
    redirect_uri: this.redirect_uri_2,
    openNewWindow: this.openNewWindow > 0,
    version: 2,
});
```
请求方法： Yo.googleAuth

|     参数      |  类型  |           说明           |
| :-----------: | :----: | :----------------------: |
| redirect_uri  | 字符串 | 登录返回跳转地址不带参数 |
| openNewWindow |  整数  |      是否新窗口打开      |
|    version    |  整数  | 可选，版本号，取值：2  ，缺省值：1  |

返回值，见 [通用跳转登录返回参数](#通用跳转登录返回参数)

## Google韩国登录请求
请求方法： Yo.googleKrAuth  
参数与 [Google登录请求](#Google登录请求) 相同


## Google日本登录请求
```javascript
Yo.googleJaAuth({
    redirect_uri: this.redirect_uri,
    openNewWindow: this.openNewWindow > 0
});
Yo.googleJaAuth({
    redirect_uri: this.redirect_uri_2,
    openNewWindow: this.openNewWindow > 0,
    version: 2,
});
```
请求方法： Yo.googleJaAuth

参数说明见[Google登录请求](#Google登录请求)

返回值，见 [通用跳转登录返回参数](#通用跳转登录返回参数)


## Yostar账号登录请求
* 请求验证
```javascript
Yo.request({
    account: 'test@example.com',
    lang: 'en',
}).then(function(data) {
    // data.result
})
```
请求方法： Yo.request

|  参数   |  类型  |           说明           |
| :-----: | :----: | :----------------------: |
| account | 字符串 |           邮箱           |
|  lang   | 字符串 | 邮件语言：ja，en，kr; 缺省en |
|    version    |  整数  | 可选，版本号，取值：2  ，缺省值：1  |

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
| result |  整数  | 0：成功，<br>50016：失败,超时，或验证码不一致,<br>50009:失败次数过多,<br>50004:账户被封禁 |
|  uid   | 字符串 |                               用户uid                                |
| token  | 字符串 |                              登录token                               |



## Yostar邮箱账号绑定已有账号请求流程

> 注：此账号不能有绑定的Yostar, 绑定信息见[执行登录](#执行登录), [执行登录v2](#执行登录v2) 返回值

* 请求验证  
  请求方法： Yo.request   
  见 [Yostar账号登录请求](#Yostar账号登录请求)

* 获取Yostar绑定参数

```javascript
Yo.authSubmit({
    account: 'test@example.com',
    code: '112233',
}).then(function(data) {
    // data.result
    // data.yostar_uid
    // data.yostar_token
    // data.yostar_account
})
```

请求方法： Yo.authSubmit

|  参数   |  类型  |    说明    |
| :-----: | :----: | :--------: |
| account | 字符串 |    邮箱    |
|  code   | 字符串 | 邮箱验证码 |

返回值:

|  参数  |  类型  |                                 说明                                 |
| :----: | :----: | :------------------------------------------------------------------: |
| result |  整数  | 0：成功，<br>50016：失败,超时，或验证码不一致,<br>50009:失败次数过多,<br>50004:账户被封禁 |
|  yostar_uid   | 字符串 |     邮箱用户id(result=0时返回)     |
| yostar_token  | 字符串 |     邮箱用户token(result=0时返回)  |
| yostar_account  | 字符串 |   邮箱用户账号(result=0时返回,<br>绑定时的参数名是yostar_username)   |


* 绑定Yostar请求1

```javascript
Yo.linkYo({
    accessToken: this.loginInfo.accessToken,
    yostar_uid: this.loginInfo.yostar_uid,
    yostar_token: this.loginInfo.yostar_token,
    yostar_username: this.loginInfo.yostar_username,
}).then(function(data) {
    // data.result
})
```

请求方法： Yo.linkYo

|  参数   |  类型  |    说明    |
| :-----: | :----: | :--------: |
| accessToken | 字符串 |    登录生成的accessToken，用于支付及其他请求    |
|  yostar_uid   | 字符串 |     邮箱用户id    |
| yostar_token  | 字符串 |     邮箱用户token  |
| yostar_username  | 字符串 |   邮箱用户账号  |

返回值:

|  参数  |  类型  |                    说明                           |
| :----: | :----: | :------------------------------------------------------------------: |
| result |  整数  | 0：成功，<br>1：此账号或提供的yostar账号已经绑定过其它的账号,<br>2：提供的yostar的token及uid错误,<br>1000：accessToken错误 |

* 绑定Yostar请求2(覆盖绑定提供的Yostar邮箱账号,提供的Yostar邮箱账号原uid被替换)

```javascript
Yo.relinkYo({
    uid: this.loginInfo.uid,
    token: this.loginInfo.token,
    yostar_uid: this.loginInfo.yostar_uid,
    yostar_token: this.loginInfo.yostar_token,
    yostar_username: this.loginInfo.yostar_username,
}).then(function(data) {
    // data.result
})
```

请求方法： Yo.relinkYo

|  参数   |  类型  |    说明    |
| :-----: | :----: | :--------: |
|  uid   | 字符串 |    用户uid           |
| token  | 字符串 |  登录token       |
|  yostar_uid   | 字符串 |     邮箱用户id    |
| yostar_token  | 字符串 |     邮箱用户token  |
| yostar_username  | 字符串 |   邮箱用户账号  |

返回值:

|  参数  |  类型  |                    说明                           |
| :----: | :----: | :------------------------------------------------------------------: |
| result |  整数  | 0：成功，<br>1：提供的此账号已经绑定过其它的Yostar邮箱账号,<br>2：提供的yostar的token及uid错误,<br>3：验证失败，uid和token不匹配 |



## Yostar邮箱账号解绑

请求方法： Yo.unlinkYo

|  参数   |  类型  |    说明    |
| :-----: | :----: | :--------: |
| accessToken  | 字符串 |  登录生成的accessToken，用于支付及其他请求       |
|  yostar_uid   | 字符串 |     邮箱用户id    |
| yostar_token  | 字符串 |     邮箱用户token  |
| yostar_username  | 字符串 |   邮箱用户账号  |

返回值:

|  参数  |  类型  |                    说明                           |
| :----: | :----: | :------------------------------------------------------------------: |
| result |  整数  | 0：成功，<br>1：提供的此账号没有绑定过Yostar邮箱账号,<br>2：提供的yostar的yostar_token及yostar_uid验证错误,<br>3：不可解绑，该项目环境需要至少绑定一个<br>1000：accessToken错误 |  




## 通用跳转登录返回参数

返回值地址栏GET参数：

| 参数  |  类型  |   说明    |
| :---: | :----: | :-------: |
|  uid  | 字符串 |  用户uid，跳转请求参数version默认时返回  |
| token | 字符串 | 登录token，跳转请求参数version默认时返回 |
| codetoken | 字符串 | 参数codetoken，跳转请求参数version=2时返回   |


## 执行登录
请求方法：Yo.login

| 参数  |  类型  |       说明       |
| :---: | :----: | :--------------: |
|  uid  | 字符串 | uid(用户id,唯一) |
| token | 字符串 |    登录token     |

返回值:

|    参数     |  类型  |                                                                                        说明                                                                                        |
| :---------: | :----: |:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|   result    |  整数  | 0：成功，<br>1:验证失败，uid和token不匹配,<br>~~2:IP访问被限制,~~<br>~~3:设备号被封禁,~~<br>4:该UID已被封禁,<br>5:该UID已被用户请求删除，同时返回reborn_before_ms长整数，到达此时间戳（时间戳单位毫秒）才删除， current_timestamp_ms 返回当前时间戳(单位毫秒) |
| reborn_before_ms | 数字 |                                                                           删除时间戳(单位毫秒)，如果result=5，就返回该值                                                                           |
| current_timestamp_ms | 数字 |                                                                           当前时间戳(单位毫秒)，如果result=5，就返回该值                                                                           |
| accessToken | 字符串 |                                                                           每次登录生成的accessToken，用于支付及其他请求                                                                           |
| twitter_username | 字符串 |                                                                                如果玩家已经绑定过tw了，就返回该值                                                                                |
| twitter_id | 字符串 |                                                                                如果玩家已经绑定过tw了，就返回该值                                                                                |
| facebook_username | 字符串 |                                                                                如果玩家已经绑定过fb了，就返回该值                                                                                |
| facebook_uid | 字符串 |                                                                                如果玩家已经绑定过fb了，就返回该值                                                                                |
| yostar_username | 字符串 |                                                                              如果玩家已经绑定过yostar了，就返回该值                                                                              |
| yostar_uid | 字符串 |                                                                              如果玩家已经绑定过yostar了，就返回该值                                                                              |
| google_username | 字符串 |                                                                              如果玩家已经绑定过google了，就返回该值                                                                              |
| google_id | 字符串 |                                                                              如果玩家已经绑定过google了，就返回该值                                                                              |
|  kr_kmc_status         |  数字   |                                            如果玩家登录成功result=0,返回kr_kmc_status该值,国账号的实名认证状态，登录成功时返回 2.1.66版本新增。取值范围 1：已实名，2：未实名，3：实名已过期                                             |


```javascript
// 示例
AccountLogin: function () {
    return Yo.login({
        uid: this.uid,
        token: this.token,
        //deviceId,
    }).then(data0 => {
        console.log(data0);
        this.loginInfo = data0;
    }).catch(console.log)
}
```

## 执行登录v2
请求方法：Yo.loginV2

| 参数  |  类型  |       说明       |
| :---: | :----: | :--------------: |
|  codetoken  | 字符串 | 登录参数，有效次数：1 |

返回值:

|    参数     |  类型  |                                                  说明                                                   |
| :---------: | :----: | :-----------------------------------------------------------------------------------------------------: |
|   result    |  整数  | 0：成功，<br>1:验证失败，uid和token不匹配,<br>4:该UID已被封禁，<br>14：codetoken无效或过期 |
|  uid  | 字符串 | uid(用户id,唯一) |
| token | 字符串 |    登录token     |
| accessToken | 字符串 |                              每次登录生成的accessToken，用于支付及其他请求                              |

```javascript
// 示例
if (this.codetoken) {
    return Yo.loginV2({
        codetoken: this.codetoken, // 有效次数一次
    }).then(data0 => {
        console.log(data0);
        if (data0 && data0.uid) {
            this.uid = data0.uid
        }
        if (data0 && data0.token) {
            this.token = data0.token
        }
        this.codetoken = '';
        this.loginInfo = data0;
    });
}
```



## 验证uid,accessToken
请求地址: ${服务器地址}/user/check  
请求方法: POST

|    参数     |  类型  |         说明          |
| :---------: | :----: | :-------------------: |
|     uid     | 字符串 |          uid          |
| accessToken | 字符串 | 登录获取的accessToken |
| twitter_username | 字符串 | 如果玩家已经绑定过tw了，就返回该值 |
| twitter_id | 字符串 | 如果玩家已经绑定过tw了，就返回该值 |
| facebook_username | 字符串 | 如果玩家已经绑定过fb了，就返回该值 |
| facebook_uid | 字符串 | 如果玩家已经绑定过fb了，就返回该值 |
| yostar_username | 字符串 | 如果玩家已经绑定过yostar了，就返回该值 |
| yostar_uid | 字符串 | 如果玩家已经绑定过yostar了，就返回该值 |
| google_username | 字符串 | 如果玩家已经绑定过google了，就返回该值 |
| google_id | 字符串 | 如果玩家已经绑定过google了，就返回该值 |

返回值:

| 参数  |  类型  |            说明             |
| :---: | :----: | :-------------------------: |
| state |  整数  |       1：成功,99:失败       |
|  msg  | 字符串 | SUCCESS:成功, INVALID：失败 |



## 删除用户

请求方法：Yo.destroy

| 参数  |  类型  |       说明       |
| :---: | :----: | :--------------: |
|  uid  | 字符串 | uid(用户id,唯一) |
| token | 字符串 |    登录token     |
| accessToken | 字符串 |    登录获取的accessToken     |

返回值:

|    参数     |  类型  |                                                  说明                                                   |
| :---------: | :----: | :-----------------------------------------------------------------------------------------------------: |
|   result    |  整数  | 0：成功，<br>1:验证失败，uid,token和accessToken不匹配,<br>2:已发送过删除请求，忽略 |


```javascript
// 示例
Yo.destroy({
    uid: this.uid,
    token: this.token,
    accessToken: this.loginInfo.accessToken
}).then(data0 => {
    console.log(data0.result);
});
```


## 恢复等待删除的用户

请求方法：Yo.reborn

| 参数  |  类型  |       说明       |
| :---: | :----: | :--------------: |
|  uid  | 字符串 | uid(用户id,唯一) |
| token | 字符串 |    登录token     |

返回值:

|    参数     |  类型  |                                                  说明                                                   |
| :---------: | :----: | :-----------------------------------------------------------------------------------------------------: |
|   result    |  整数  | 0：成功,<br>1:验证失败，uid,token不匹配,<br>2:撤销删除失败,已删除,<br>3:撤销删除失败,没有删除记录 |


```javascript
// 示例

Yo.reborn({
    uid: this.uid,
    token: this.token,
}).then(data0 => {
    console.log(data0.result);
});
```

## 获取问卷

请求方法：Yo.survey

|       参数       |  类型  |  是否必填   |        说明         |
|:--------------:| :----: |:---:|:-----------------:|
|  accessToken   | 字符串 |  必填   | 登录获取的accessToken  |
|    activity    | 字符串 |   必填  |       问卷id        |
|     gameid     | 字符串 |   必填  |       游戏id        |
| gameNotifyURL  | 字符串 |   选填  | 完成后通知回调地址,最大长度100 |

返回值:

|    参数     |  类型  |                                                  说明                                                   |
| :---------: | :----: | :-----------------------------------------------------------------------------------------------------: |
|   result    |  整数  | 0：成功,<br>1:问卷不存在，获取问卷失败,<br>1000:accessToken验证错误 |
| wj_url | 字符串 | result=0时返回问卷地址 |


```javascript
// 示例

Yo.survey({
    accessToken: this.loginInfo.accessToken,
    activity: "134415018", // 问卷id，获取方式为可由邮件等，由运营配置
    gameid: "112233", // 游戏id，相同问卷id不可重复提交问卷
}).then(data0 => {
    console.log(data0);
    if (data0.result === 0) {
        // window.open(data0.wj_url)
    }
});
```

## 当前账号韩国实名认证信息

请求方法：Yo.kmcInfo

| 参数  |  类型  |       说明       |
| :---: | :----: | :--------------: |
|  accessToken  | 字符串 | 登录获取的accessToken |

返回值:

|     参数    |  类型  |                       说明                        |
|:----------:|:----:|:-----------------------------------------------:|
|   result   |  整数  |  0：成功,<br> 1:不需要实名认证,<br> 1000:accessToken验证错误  |
| kmc_status |  整数  | 当前uid实名验证的状态，1：已实名， 2：未实名， 3：实名已过期。当值为1时代表已验证，不要再次发起实名验证 |
| kmc_request_id | 字符串  |                 忽略，请求实名认证的连接参数                  |


```javascript
// 示例

Yo.kmcInfo({
   accessToken: this.loginInfo.accessToken,
}).then(data0 => {
   console.log(data0.result);
   console.log(data0.kmc_status);
});
```

## 发起韩国实名认证
请求方法：Yo.kmcStart

| 参数  |  类型  |       说明       |
| :---: | :----: | :--------------: |
|  accessToken  | 字符串 | 登录获取的accessToken |

返回值:

|     参数    |  类型  |                       说明                        |
|:----------:|:----:|:-----------------------------------------------:|
|   result   |  整数  |  0：成功,<br> 1:不需要实名认证,<br> 1000:accessToken验证错误  |
| kmc_status |  整数  | 当前uid实名验证的状态，1：已实名， 2：未实名， 3：实名已过期。当值为1时代表已验证，不要再次发起实名验证 |
| kmc_request_id | 字符串  |                 忽略，请求实名认证的连接参数                  |

> 注：仅当返回值的result=0、kmc_status!=1时，会自动通过JavaScript打开弹出的新窗口跳转到韩国实名认证页面

```javascript
// 示例

Yo.kmcStart({
   accessToken: this.loginInfo.accessToken,
}).then(data0 => {
   console.log(data0.result);
   console.log(data0.kmc_status);
});
```

## 支付流程图
* 流程图地址 [https://swimlanes.io/u/OoyQdIV0O](https://swimlanes.io/u/OoyQdIV0O)




## 银行绑定发送SMS验证
请求方法：Yo.smsRequest
*  浏览器执行订单：
```javascript
Yo.smsRequest({
    accessToken: this.loginInfo.accessToken,
    countryCallingCode: this.countryCallingCode,
    mobile: this.mobile,
})
```

请求参数:

|      参数               | 类型  |         说明          |
|:---------------------:|:---:|:-------------------:|
|      accessToken      | 字符串 |  登录获取的accessToken   |
|  countryCallingCode   | 字符串 | 以加号开头的国家号码，例如+86，+1 |
|        mobile         | 字符串 |  在国际前缀后所拨的号码，由数字组成  |


返回值:

|  参数  | 类型  |                                           说明                                           |
| :----: |:---:|:--------------------------------------------------------------------------------------:|
| result | 整数  | 0：成功，<br>1：手机号已绑定,<br>2:发送频率过快（需求最多1次/分钟）,<br>3：短信发送平台接口调用异常,<br> 1000:accessToken验证错误 |
|   requestId   | 字符串 |                                      验证请求id（成功返回）                                      |



## 银行绑定提交SMS验证
请求方法：Yo.smsValidate
*  浏览器执行订单：
```javascript
Yo.smsValidate({
    requestId: this.requestId,
    smsCode: this.BankDirectInfo.sms_code,
})
```

请求参数:

|    参数     | 类型  |      说明      |
|:---------:|:---:|:------------:|
| requestId | 字符串 |  绑定操作的请求id   |
|  smsCode  | 字符串 | 绑定操作收到的手机验证码 |

返回值:

|  参数  | 类型  |                                        说明                                        |
| :----: |:---:|:--------------------------------------------------------------------------------:|
| result | 整数  | 0：成功，<br>1：请求id不存在,<br>2:验证码过期(需求10分钟过期),<br>3：验证码验证失败 |



## 银行绑定信息添加
请求方法：Yo.addBankDirectInfo
*  浏览器执行订单：
```javascript
Yo.addBankDirectInfo({
    requestId: this.requestId,
    lastName: this.BankDirectInfo.lastName,
    firstName: this.BankDirectInfo.firstName,
    dateOfBirth: this.BankDirectInfo.dateOfBirth,
})
```

请求参数:

|    参数     |  类型  |                                                     说明                                                      |
|:---------:|:----:|:-----------------------------------------------------------------------------------------------------------:|
| requestId | 字符串  |                                                  绑定操作的请求id                                                  |
|  lastName  | 字符串  | 账户持有人（姓,仅限日语片假名,需要接入时前端直接校验,参考[wanakana.isKatakana](https://github.com/WaniKani/WanaKana)），长度限制 双字节 60 字节  |
|  firstName  | 字符串  |      账户持有人（名,仅限日语片假名,需要前端接入时前端直接校验,参考[wanakana.isKatakana](https://github.com/WaniKani/WanaKana)），长度限制 双字节 60 字节      |
|  dateOfBirth  | 字符串  |                                              出生日期，YYYYMMDD 格式                                               |

返回值:

|  参数  | 类型  |                              说明                              |
| :----: |:---:|:------------------------------------------------------------:|
| result | 整数  | 0：成功<br>1：请求id不存在<br>2:短信sms未验证<br>3：出生日期格式错误<br/>4：银行卡信息错误 |


## 银行绑定信息获取银行列表
请求方法：Yo.availableBankDirect
*  浏览器执行订单：
```javascript
Yo.availableBankDirect({
}).then(data => {
    console.log(data)
})
```

返回值:

|        参数        | 类型  |       说明       |
|:----------------:|:---:|:--------------:|
|      result      | 整数  | 0：成功<br>1：获取失败 |
|       bank       | 数组  |  获取成功时返回，银行列表  |
| bank[n].BankCode | 字符串  |  银行编码，半角4位长度   |
|   bank[n].Logo   | 字符串  | 银行图标的网络URL地址   |
|   bank[n].Name   | 字符串  |    銀行名（全角）     |


## 发起银行绑定用户跳转页面
请求方法：Yo.startBankDirectRegist
*  浏览器执行订单：
```javascript
Yo.startBankDirectRegist({
    requestId: this.requestId,
    bankCode: this.BankDirectInfo.bankCode,
}).then(data => {
    console.log(data)
})
```

请求参数:

|    参数     |  类型  |                       说明                       |
|:---------:|:----:|:----------------------------------------------:|
| requestId | 字符串  |                   绑定操作的请求id                    |
|  bankCode  | 字符串  | 银行编码，半角4位长度，方法[银行绑定信息获取银行列表](#银行绑定信息获取银行列表)获取 |

返回值:

|  参数  | 类型  |                                                    说明                                                    |
| :----: |:---:|:--------------------------------------------------------------------------------------------------------:|
| result | 整数  | 0：等待用户银行信息注册完成，需要调用<br/>[银行绑定获取手机号银行信息](#银行绑定获取手机号银行信息)展示最终绑定注册结果<br>1：请求id不存在<br>2:银行卡信息【[银行绑定信息添加](#银行绑定信息添加)】未提交<br>3：发起GMO注册API错误 |


## 银行绑定获取手机号银行信息
请求方法：Yo.mobileBankDirectInfo
*  浏览器执行订单：
```javascript
Yo.mobileBankDirectInfo({
    accessToken: this.loginInfo.accessToken,
}).then(data => {
    console.log(data)
})
```

请求参数:

|      参数    |  类型  |       说明         |
|:------------:|:----:|:-------------------:|
| accessToken | 字符串 |  登录获取的accessToken   |


返回值:

|          参数          |      类型      |                     说明                      |
|:--------------------:|:------------:|:-------------------------------------------:|
|        result        |      整数      | 0：成功<br/>1：获取GMO接口错误<br/>1000：accessToken错误 |
| country_calling_code | 字符串（注册成功时返回） |             以加号开头的国家号码，例如+86，+1             |
|        mobile        | 字符串（注册成功时返回） |              在国际前缀后所拨的号码，由数字组成              |
|     mobile_full      | 字符串（注册成功时返回） |                   完整的手机号                    |
|      bank_name       | 字符串（注册成功时返回） |                 注册的银行名（全角）                  |
|         logo         | 字符串（注册成功时返回） |                银行图标的网络URL地址                 |


## 发送解绑银行短信验证码
请求方法：Yo.smsUnlinkRequest
*  浏览器执行订单：
```javascript
Yo.smsUnlinkRequest({
    accessToken: this.loginInfo.accessToken,
}).then(data => {
    console.log(data)
})
```

请求参数:

|      参数    |  类型  |       说明         |
|:------------:|:----:|:-------------------:|
| accessToken | 字符串 |  登录获取的accessToken   |

返回值:

|    参数     | 类型  |                                           说明                                            |
|:---------:|:---:|:---------------------------------------------------------------------------------------:|
|  result   | 整数  | 0：成功，<br>1：未绑定银行信息,<br>2:发送频率过快（需求最多1次/分钟）,<br>3：短信发送平台接口调用异常,<br> 1000:accessToken验证错误 |
| requestId | 字符串 |                                      验证请求id（成功返回）                                       |


## 验证短信验证码解绑银行
请求方法：Yo.removeMobileBankDirectInfo
*  浏览器执行订单：
```javascript
Yo.removeMobileBankDirectInfo({
    requestId: this.requestId,
    smsCode: this.BankDirectInfo.sms_code,
}).then(data => {
    console.log(data)
})
```

请求参数:

|    参数     |  类型  |                 说明                 |
|:---------:|:----:|:----------------------------------:|
| requestId | 字符串 | [发送解绑银行短信验证码](#发送解绑银行短信验证码)返回的请求id |
| smsCode   | 字符串 |               短信验证码                |

返回值:

|    参数    | 类型  |            说明                  |
|:--------:|:---:|:------------------------------:|
| result   | 整数  | 0：成功，<br>1：未找到解绑请求<br>2:验证短信失败 |


## 银行绑定账号创建订单
*  服务器创建订单（服务器创建）：  
   请求地址：${服务器地址}/gm/bankdirect/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)


## 银行绑定账号支付订单时发送短信验证码
请求方法：Yo.smsOrderRequest
*  浏览器执行订单：
```javascript
Yo.smsOrderRequest({
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
}).then(data => {
    console.log(data)
})
```

请求参数:

|    参数     |  类型  |                说明                |
|:---------:|:----:|:--------------------------------:|
| accessToken | 字符串 |         登录获取的accessToken         |
| orderId   | 字符串 | [银行绑定账号创建订单](#银行绑定账号创建订单)创建的订单id |


返回值:

|    参数    | 类型  |                                               说明                                                |
|:--------:|:---:|:-----------------------------------------------------------------------------------------------:|
|  result   | 整数  | 0：成功，<br>1：未绑定银行信息,<br>2：订单未找到,<br>3:发送频率过快（需求最多1次/分钟）,<br>4：短信发送平台接口调用异常,<br> 1000:accessToken验证错误 |


## 验证短信验证码并执行支付
请求方法：Yo.smsOrderValidateAndExec
*  浏览器执行订单：
```javascript
Yo.smsOrderValidateAndExec({
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    smsCode: this.BankDirectInfo.sms_code,
}).then(data => {
    console.log(data)
})
```

请求参数:

|    参数     |  类型  |                        说明                         |
|:---------:|:----:|:-------------------------------------------------:|
| accessToken | 字符串 |                 登录获取的accessToken                  |
| orderId   | 字符串 |         [银行绑定账号创建订单](#银行绑定账号创建订单)创建的订单id          |
| smsCode   | 字符串 | [银行绑定账号支付订单时发送短信验证码](#银行绑定账号支付订单时发送短信验证码)收到的短信验证码 |

返回值:

|    参数    | 类型  |                                                                       说明                                                                        |
|:--------:|:---:|:-----------------------------------------------------------------------------------------------------------------------------------------------:|
|  result   | 整数  | 0：成功，服务器可通过[通用查询订单](#通用查询订单)查询结果，<br>1：未绑定银行信息,<br>2：订单未找到,<br>3：订单未发送验证短信<br/>4:订单发送验证短信不存在,<br>5：短信验证失败,<br/>6：支付失败,<br> 1000:accessToken验证错误 |




## 日服浏览器CreditCard支付
*  获取信用卡token令牌
```javascript
let that = this;
window.Multipayment.init("tshop00037465");
Multipayment.getToken(
    {
        cardno: "4111111111111111",
        expire: "1901",
        securitycode: "123",
        holdername: "Holdername"
    }, function (response) {
        if (response.resultCode != "000") {
            window.alert('Error occurred during purchase process')
        } else {
            // 获取的信用卡token令牌
            that.cardInfo.creditcardToken = response.tokenObject.token
        }
    }
);
```

> Multipayment.init(ShopID);   
> Multipayment.getToken( cardObject , callback )

请求参数cardObject：

|     参数     |  类型  |                                                                                     说明                                                                                      |
| :----------: | :----: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|    cardno    | 字符串 |                                                                                必填，信用卡号                                                                                 |
|    expire    | 字符串 |                                                                      必填，过期日期，格式为YYMM或YYYYMM                                                                       |
| securitycode | 字符串 |                                                                              选填，安全吗，3-4位                                                                              |
|  holdername  | 字符串 | 选填，持有人，字符类型：(half-width) <br>  Numeric characters/alphabets <br>(Uppercase/Lowercase)/<br>" " (Space), "," (Comma), "."(Period), “-” <br>(Hyphen), “/”(Slash) |

Multipayment.getToken返回JSON：

|    参数     |  类型  |        说明        |
| :---------: | :----: | :----------------: |
| resultCode  | 字符串 | 返回码,"000"：成功 |
| tokenObject |  JSON  |  返回码成功时有效  |

tokenObject参数：

|       参数        |  类型  |               说明                |
| :---------------: | :----: | :-------------------------------: |
|       token       | 字符串 |     信用卡交易使用的token令牌     |
|   toBeExpiredAt   | 字符串 | 过期时间，格式yyyy-mm-dd-HH-MM-SS |
|   maskedCardNo    | 字符串 |             加*的卡号             |
| isSecurityCodeSet | 布尔值 |            安全码设置             |

*  服务器创建订单：   
   请求地址：${服务器地址}/gm/cdcard/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)

*  浏览器执行订单：
```javascript
// Example
Yo.execOrder({
    type: 'CreditCard',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    token: this.cardInfo.creditcardToken,
    orderId: this.orderId,
    cardNo: this.cardInfo.cardNo,
    openNewWindow: this.openNewWindow > 0,
})
```
请求参数：

|    参数     |  类型  |                    说明                    |
| :---------: | :----: | :----------------------------------------: |
|    type     | 字符串 |             CreditCard:信用卡              |
|    lang     | 字符串 |                  ja:日本                   |
| accessToken | 字符串 |           登录获取的accessToken            |
|    token    | 字符串 | 信用卡获取的response.tokenObject.token令牌 |
|   orderId   | 字符串 |           创建订单的返回的订单号           |
|   cardNo    | 字符串 |         用户输入的信用卡号，记录用         |

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)


## 日服Paypal支付
*  服务器创建订单：  
   请求地址：${服务器地址}/gm/pp/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)
*  浏览器执行订单：
```javascript
Yo.execOrder({
    type: 'Paypal',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    itemName: this.itemName,
    openNewWindow: this.openNewWindow > 0,
})
```
请求参数

|     参数      |  类型  |                说明                 |
| :-----------: | :----: | :---------------------------------: |
|     type      | 字符串 |            Paypal:Paypal            |
|     lang      | 字符串 |               ja:日本               |
|  accessToken  | 字符串 |        登录获取的accessToken        |
|    orderId    | 字符串 |       创建订单的返回的订单号        |
|   itemName    | 字符串 |             订单商品名              |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)
> 备注: 由于接入渠道限制，相同订单号仅能第一次成功跳转到支付页面

## 日服Au支付
*  服务器创建订单：  
   请求地址：${服务器地址}/gm/au/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)
*  浏览器执行订单：
*
```javascript
Yo.execOrder({
    type: 'Au',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    itemName: this.itemName,
    openNewWindow: this.openNewWindow > 0,
})
```

请求参数

|     参数      |  类型  |                说明                 |
| :-----------: | :----: | :---------------------------------: |
|     type      | 字符串 |                Au:Au                |
|     lang      | 字符串 |               ja:日本               |
|  accessToken  | 字符串 |        登录获取的accessToken        |
|    orderId    | 字符串 |       创建订单的返回的订单号        |
|   itemName    | 字符串 |             订单商品名              |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |
> 注：Au支付参数 itemName 所有字符必须是全角双字节字符

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)
> 备注: 由于接入渠道限制，相同订单号仅能第一次成功跳转到支付页面


## 日服Docomo支付
*  服务器创建订单：  
   请求地址：${服务器地址}/gm/dcm/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)
*  浏览器执行订单：

```javascript
Yo.execOrder({
    type: 'Docomo',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    openNewWindow: this.openNewWindow > 0,
})
```

请求参数:

|     参数      |  类型  |                说明                 |
| :-----------: | :----: | :---------------------------------: |
|     type      | 字符串 |            Docomo:Docomo            |
|     lang      | 字符串 |               ja:日本               |
|  accessToken  | 字符串 |        登录获取的accessToken        |
|    orderId    | 字符串 |       创建订单的返回的订单号        |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)
> 备注: 由于接入渠道限制，相同订单号仅能第一次成功跳转到支付页面


## 日服Softbank支付
*  服务器创建订单：  
   请求地址：${服务器地址}/gm/sb/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)
*  浏览器执行订单：

```javascript
Yo.execOrder({
    type: 'Softbank',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    openNewWindow: this.openNewWindow > 0,
})
```
请求参数

|     参数      |  类型  |                说明                 |
| :-----------: | :----: | :---------------------------------: |
|     type      | 字符串 |          Softbank:Softbank          |
|     lang      | 字符串 |               ja:日本               |
|  accessToken  | 字符串 |        登录获取的accessToken        |
|    orderId    | 字符串 |       创建订单的返回的订单号        |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)
> 备注: 由于接入渠道限制，相同订单号仅能第一次成功跳转到支付页面


## 日服PayPay支付
*  服务器创建订单：  
   请求地址：${服务器地址}/gm/paypay/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)
*  浏览器执行订单：

```javascript
Yo.execOrder({
    type: 'PayPay',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    openNewWindow: this.openNewWindow > 0,
})
```
请求参数

|     参数      |  类型  |                说明                 |
| :-----------: | :----: | :---------------------------------: |
|     type      | 字符串 |          PayPay:PayPay          |
|     lang      | 字符串 |               ja:日本               |
|  accessToken  | 字符串 |        登录获取的accessToken        |
|    orderId    | 字符串 |       创建订单的返回的订单号        |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)
> 备注: 由于接入渠道限制，相同订单号仅能第一次成功跳转到支付页面



## 日服WebMoney支付
*  服务器创建订单：  
   请求地址：${服务器地址}/wm/wm/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)
*  浏览器执行订单：

```javascript
Yo.execOrder({
    type: 'WebMoney',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    openNewWindow: this.openNewWindow > 0,
    itemName: this.itemName
})
```
请求参数

|     参数      |  类型  |                说明                 |
| :-----------: | :----: | :---------------------------------: |
|     type      | 字符串 |          WebMoney:WebMoney          |
|     lang      | 字符串 |               ja:日本               |
|  accessToken  | 字符串 |        登录获取的accessToken        |
|    orderId    | 字符串 |       创建订单的返回的订单号        |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |
| itemName      | 字符串 |             订单商品名             |

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)


## 日服浏览器CreditCard支付2020软银
*  服务器创建订单：  
   请求地址：${服务器地址}/sbp/cdcard/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)
*  浏览器执行订单：
```javascript
Yo.execOrder({
    type: 'CreditCard$SBPayment',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    itemName: this.itemName,
    openNewWindow: this.openNewWindow > 0,
})
```
请求参数

|     参数      |  类型  |                说明                 |
| :-----------: | :----: | :---------------------------------: |
|     type      | 字符串 |   CreditCard$SBPayment:CreditCard    |
|     lang      | 字符串 |               ja:日本               |
|  accessToken  | 字符串 |        登录获取的accessToken        |
|    orderId    | 字符串 |       创建订单的返回的订单号        |
|   itemName    | 字符串 |             订单商品名              |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)


## 日服Paypal支付2020软银
*  测试账号及密码(可以用美服创建的沙盒账号)：test1@yo-star.com
*  服务器创建订单：  
   请求地址：${服务器地址}/sbp/pp/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)
*  浏览器执行订单：
```javascript
Yo.execOrder({
    type: 'Paypal$SBPayment',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    itemName: this.itemName,
    openNewWindow: this.openNewWindow > 0,
})
```
请求参数

|     参数      |  类型  |                说明                 |
| :-----------: | :----: | :---------------------------------: |
|     type      | 字符串 |       Paypal$SBPayment:Paypal        |
|     lang      | 字符串 |               ja:日本               |
|  accessToken  | 字符串 |        登录获取的accessToken        |
|    orderId    | 字符串 |       创建订单的返回的订单号        |
|   itemName    | 字符串 |             订单商品名              |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)


## 日服Au支付2020软银
*  服务器创建订单：  
   请求地址：${服务器地址}/sbp/au/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)
*  浏览器执行订单：
*
```javascript
Yo.execOrder({
    type: 'Au$SBPayment',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    itemName: this.itemName,
    openNewWindow: this.openNewWindow > 0,
})
```

请求参数

|     参数      |  类型  |                说明                 |
| :-----------: | :----: | :---------------------------------: |
|     type      | 字符串 |            Au$SBPayment:Au            |
|     lang      | 字符串 |               ja:日本               |
|  accessToken  | 字符串 |        登录获取的accessToken        |
|    orderId    | 字符串 |       创建订单的返回的订单号        |
|   itemName    | 字符串 |             订单商品名              |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)


## 日服Docomo支付2020软银
*  服务器创建订单：  
   请求地址：${服务器地址}/sbp/dcm/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)
*  浏览器执行订单：

```javascript
Yo.execOrder({
    type: 'Docomo$SBPayment',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    openNewWindow: this.openNewWindow > 0,
})
```

请求参数:

|     参数      |  类型  |                说明                 |
| :-----------: | :----: | :---------------------------------: |
|     type      | 字符串 |     Docomo$SBPayment:Docomo        |
|     lang      | 字符串 |               ja:日本               |
|  accessToken  | 字符串 |        登录获取的accessToken        |
|    orderId    | 字符串 |       创建订单的返回的订单号        |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)


## 日服Softbank支付2020软银
*  测试账号及密码：08032116661 pass08032116661
*  服务器创建订单：  
   请求地址：${服务器地址}/sbp/sb/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)
*  浏览器执行订单：

```javascript
Yo.execOrder({
    type: 'Softbank$SBPayment',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    openNewWindow: this.openNewWindow > 0,
})
```
请求参数

|     参数      |  类型  |                说明                 |
| :-----------: | :----: | :---------------------------------: |
|     type      | 字符串 |     Softbank$SBPayment:Softbank     |
|     lang      | 字符串 |               ja:日本               |
|  accessToken  | 字符串 |        登录获取的accessToken        |
|    orderId    | 字符串 |       创建订单的返回的订单号        |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)


## 日服通用创建订单参数
* 请求参数：

| 参数                                                              | 类型   | 是否必填 | 说明                                                           |
|:----------------------------------------------------------------|:-----|:-----|:-------------------------------------------------------------|
| accessToken                                                     | 字符串  | 必填   | 执行登录后返回的accessToken                                          |
| amount                                                          | 字符串  | 必填   | 金额，日服金额为正整数字符串                                               |
| extraData                                                       | 字符串  | 必填   | 保留，填订单额外信息                                                   |
| redirect_uri                                                    | 字符串  | 必填   | 订单完成后跳转GET地址，可带参数                                            |
| notifyUrl                                                       | 字符串  | 必填   | 订单完成时POST通知地址，见[日服支付通知](#日服支付通知)                             |
| sign                                                            | 字符串  | 必填   | 验证参数                                                         |
| itemName                                                        | 字符串  | 必填   | 商品名，美服必填，韩服必填，日服忽略                                           |
| <span id="realMoney">realMoney</span>                           | 字符串  | 选填   | 韩服必填，韩服传递<b>韩元定价*1000</b>，美服日服不填                             |
| <span id="operation_description">operation_description</span>   | 字符串  | 选填   | 自定义参数，给运营查看的描述值，目前需求是填入当前用户的国家和使用的IP地址，不参与sign签名验证，长度限制255以内 |
> 美服,日服: sign生成方式为请求参数accessToken，amount，extraData，redirect_uri，notifyUrl和KEY依次拼接后的MD5值，
KEY的值为'111111'  
> <b>韩服</b>: sign生成方式为请求参数accessToken，amount，extraData，redirect_uri，notifyUrl，realMoney和KEY依次拼接后的MD5值，
KEY的值为'111111'

> 当redirect_uri传值为'Yo://CloseWindow'时（区分大小写），支付完成后关闭窗口，不跳转GET地址

* 返回JSON：

| 参数    | 类型   | 说明                                                                                                                 |
|:--------|:-------|:-------------------------------------------------------------------------------------------------------------------|
| orderId | 字符串 | 订单id                                                                                                               |
| rdToken | 字符串 | 订单rdToken                                                                                                          |
| code    | 整数   | 创建失败时返回，<br>90001：未执行购买成功的订单过多，<br>90002：sign验证失败,<br>90005：该订单支付超过当月所拥有韩服账号实名认证的限额                                |
| result  | 整数   | 1：未实名，需要韩服实名认证； 2：实名已过期，需要韩服重新实名认证； <br/> 1000：创建失败时返回，accessToken已被新登录刷新，需要重新登录（例如日服美服都先后登录），重新登录见 [执行登录](#执行登录); |

限制用户每小时创建未执行购买成功的订单超过60，则不返回orderId和rdToken，创建订单失败

## 日服支付通知
请求地址：日服创建订单时参数 ${notifyUrl}  
请求方式：POST  
'content-type': 'application/x-www-form-urlencoded'  
通知参数：

|   参数    |  类型  |         说明          |
| :-------: | :----: | :-------------------: |
|  orderId  | 字符串 |        订单id         |
| extraData | 字符串 | 订单创建时的extraData |

收到请求后，使用orderId查询订单状态，见[日服通用查询订单](#通用查询订单)   
响应内容：
* 字符串 success 或者其他, 程序执行完后必须打印输出 “success” (不包含引号，不能加入换行符，缩进符等不可见字符)。如果商户反馈给Yostar的字符不是这7个字符,Yostar服务器会不断重发通知,一般情况下,24 小时以内完成12次通知。
* 程序执行完成后,该页面不能执行页面跳转。如果执行页面跳转,Yostar会收不到 success 字符,会被Yostar服务器判定为该页面程序运行出现异常, 而重发处理结果通知
* 该方式的调试与运行必须在服务器上,即互联网上能访问


## 美服Paypal支付
*  服务器创建订单：  
   请求地址：${服务器地址}/direct/pp/createOrder  
   请求方式：POST  
   请求参数：见 [美服通用创建订单参数](#美服通用创建订单参数)
*  浏览器执行订单：

```javascript
Yo.execOrder({
    type: 'Paypal',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    openNewWindow: this.openNewWindow > 0,
})
```

请求参数

|     参数      |  类型  |                说明                 |
| :-----------: | :----: | :---------------------------------: |
|     type      | 字符串 |            Paypal:Paypal            |
|     lang      | 字符串 |               en:美国               |
|  accessToken  | 字符串 |        登录获取的accessToken        |
|    orderId    | 字符串 |       创建订单的返回的订单号        |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)

> 测试账号及密码：test1@yo-star.com

## 美服MasterCard支付
> 见[美服信用卡支付](#美服信用卡支付)


## 美服MasterCard支付
> 见[美服信用卡支付](#美服信用卡支付)  
> 测试卡号 2222 4000 7000 0005    03/30   737

## 美服Visa支付
> 见[美服信用卡支付](#美服信用卡支付)  
> 测试卡号 4000 1600 0000 0004    03/30   737

## 美服JCB支付
> 见[美服信用卡支付](#美服信用卡支付)  
> 测试卡号 3569 9900 1009 5841    03/30   737

## 美服信用卡支付
1.  获取Adyen信用卡支付渠道originKey  
    请求方法Yo.generateOriginKey

|     参数     |  类型  |                                     说明                                     |
| :----------: | :----: | :--------------------------------------------------------------------------: |
| originDomain | 字符串 | 输入信用卡信息的页面地址，不带子目录，不带结尾/，例：https://www.example.com |


```javascript
// 示例
// let originDomain = window.location.href.replace(window.location.search, '').replace(window.location.pathname, '')
String.prototype.reverse = String.prototype.reverse || function() {
  return this.split('').reverse().join('')
}
let originDomain = window.location.href.replace(window.location.search, '').reverse().replace(window.location.pathname.reverse(), '').reverse()

Yo.generateOriginKey({ originDomain: originDomain }, (err, data) => {
    if (err) {
        console.error(err);
    } else {
        let originKey = data.originKeys[originDomain]
        // save originKey
        this.Adyen.originKey = originKey;
    }
});
```


2.  获取信用卡加密后的信息(Adyen):
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <link rel="stylesheet" href="<%= checkoutShopperUrl %>/checkoutshopper/sdk/2.1.0/adyen.css" />
  <script src="<%= checkoutShopperUrl %>/checkoutshopper/sdk/2.1.0/adyen.js"></script>
</head>
<body>
<div id="card"></div>
</body>
<script>
    // 只需执行一次
  const configuration = {
    locale: "en_US",
    originKey: "pub.v2.8015531734320675.aHR0cHM6Ly93ZWwtMzAzMS5uZ3Jvay5pbw.Te_bLogFtSvXgEdJs8S3J33c4zsJkzl2jzfhiQ7MDcY",
    loadingContext: "<%= checkoutShopperUrl %>/checkoutshopper/"
  };
  const checkout = new AdyenCheckout(configuration);

  const card = checkout.create("card", {
    onChange: handleOnChange
  }).mount("#card");
  let that = this;

  function handleOnChange(state, component) {
    //console.log(state);
    //console.log(component);
    state.isValid // true or false.
    state.data
    /* for example:
     {type: "scheme",
        encryptedCardNumber: "adyenjs_0_1_18$MT6ppy0FAMVMLH...",
        encryptedExpiryMonth: "adyenjs_0_1_18$MT6ppy0FAMVMLH...",
        encryptedExpiryYear: "adyenjs_0_1_18$MT6ppy0FAMVMLH...",
        encryptedSecurityCode: "adyenjs_0_1_18$MT6ppy0FAMVMLH..."}
    */
    if (state.isValid) {
      let { encryptedCardNumber, encryptedExpiryMonth, encryptedExpiryYear, encryptedSecurityCode } = state.data;
      //console.log(encryptedCardNumber, encryptedExpiryMonth, encryptedExpiryYear, encryptedSecurityCode)
      // todo: save encryptedCardNumber, encryptedExpiryMonth, encryptedExpiryYear, encryptedSecurityCode & submit Yo.execOrder({ ... })
    } else {
        that.Adyen.encryptedCardNumber = '';
        that.Adyen.encryptedExpiryMonth = '';
        that.Adyen.encryptedExpiryYear = '';
        that.Adyen.encryptedSecurityCode = '';
    }
  }
</script>
</html>
```


3.  服务器创建订单：  
    请求地址：${服务器地址}/ay/mc/createOrder  
    请求方式：POST    
    请求参数：见 [美服通用创建订单参数](#美服通用创建订单参数)


4.    浏览器执行订单：
```javascript
Yo.execOrder({
    type: 'Adyen.CreditCard',
    lang: 'en',
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    encryptedCardNumber: this.Adyen.encryptedCardNumber,
    encryptedExpiryMonth: this.Adyen.encryptedExpiryMonth,
    encryptedExpiryYear: this.Adyen.encryptedExpiryYear,
    encryptedSecurityCode: this.Adyen.encryptedSecurityCode,
    openNewWindow: this.openNewWindow > 0,
})
```
请求参数：

|         参数          |  类型  |                   说明                   |
| :-------------------: | :----: | :--------------------------------------: |
|         type          | 字符串 | 必填，'Adyen.CreditCard'，美服信用卡支付 |
|         lang          | 字符串 |             必填，'en'，美服             |
|      accessToken      | 字符串 |    必填，执行登录后返回的accessToken     |
|        orderId        | 字符串 |       必填，订单创建时获取的订单号       |
|  encryptedCardNumber  | 字符串 |          必填，加密后的信用卡号          |
| encryptedExpiryMonth  | 字符串 |        必填，加密后的信用卡过期月        |
|  encryptedExpiryYear  | 字符串 |        必填，加密后的信用卡过期年        |
| encryptedSecurityCode | 字符串 |        必填，加密后的信用卡安全码        |


## 美服支付宝支付
1.  服务器创建订单：  
    请求地址：${服务器地址}/ay/al/createOrder  
    请求方式：POST    
    请求参数：见 [美服通用创建订单参数](#美服通用创建订单参数)

2.  浏览器执行订单：  
    执行方法：Yo.execOrder

```javascript
Yo.execOrder({
    type: 'Adyen.Alipay',
    lang: 'en',
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    openNewWindow: this.openNewWindow > 0,
})
```  

请求参数：

|     参数      |  类型  |                 说明                 |
| :-----------: | :----: | :----------------------------------: |
|     type      | 字符串 | 必填，'Adyen.Alipay'，美服支付宝支付 |
|     lang      | 字符串 |           必填，'en'，美服           |
|  accessToken  | 字符串 |  必填，执行登录后返回的accessToken   |
|    orderId    | 字符串 |     必填，订单创建时获取的订单号     |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow  |

> 测试账号： sandbox_forex1@alipay.com	   111111


## 美服信用卡Stripe渠道支付

1.  服务器创建订单：  
    请求地址：${服务器地址}/stripe/card/createOrder  
    请求方式：POST    
    请求参数：见 [美服通用创建订单参数](#美服通用创建订单参数)


2.    浏览器执行订单：
```javascript
Yo.execOrder({
    type: 'Stripe.CreditCard',
    lang: 'en',
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    openNewWindow: this.openNewWindow > 0,
})
```
请求参数：

|         参数          |  类型  |                   说明                   |
| :-------------------: | :----: | :--------------------------------------: |
|         type          | 字符串 | 必填，'Stripe.CreditCard'，美服信用卡Stripe支付 |
|         lang          | 字符串 |             必填，'en'，美服             |
|      accessToken      | 字符串 |    必填，执行登录后返回的accessToken     |
|        orderId        | 字符串 |       必填，订单创建时获取的订单号       |
|    openNewWindow      |  整数  |   是否新窗口打开，取值!!openNewWindow    |

> 测试卡号 VISA 4242424242424242 (CVC任意数字，日期任意将来日期)  
> 测试卡号 Mastercard 5555555555554444 (CVC任意数字，日期任意将来日期)  
> 测试卡号 JCB 3566002020360505 (CVC任意数字，日期任意将来日期)  
> 参考文档地址 https://stripe.com/docs/testing#cards


## 美服支付宝Stripe渠道支付

1.  服务器创建订单：  
    请求地址：${服务器地址}/stripe/ali/createOrder  
    请求方式：POST    
    请求参数：见 [美服通用创建订单参数](#美服通用创建订单参数)


2.    浏览器执行订单：
```javascript
Yo.execOrder({
    type: 'Stripe.Alipay',
    lang: 'en',
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    openNewWindow: this.openNewWindow > 0,
})
```
请求参数：

|         参数          |  类型  |                   说明                   |
| :-------------------: | :----: | :--------------------------------------: |
|         type          | 字符串 | 必填，'Stripe.Alipay'，美服支付宝Stripe支付 |
|         lang          | 字符串 |             必填，'en'，美服             |
|      accessToken      | 字符串 |    必填，执行登录后返回的accessToken     |
|        orderId        | 字符串 |       必填，订单创建时获取的订单号       |
|    openNewWindow      |  整数  |   是否新窗口打开，取值!!openNewWindow    |

> 测试环境 输入任意，按页面提示操作测试


## 美服通用创建订单参数
> 参考[日服通用创建订单参数](#日服通用创建订单参数)

## 美服支付通知
与[日服支付通知](#日服支付通知)相同



## 韩服信用卡Stripe渠道支付
1.  服务器创建订单：  
    请求地址：${服务器地址}/stripekr/card/createOrder  
    请求方式：POST    
    请求参数：见 [美服通用创建订单参数](#美服通用创建订单参数)

2.    浏览器执行订单：
```javascript
Yo.execOrder({
    type: 'Stripe.CreditCard',
    lang: 'kr',
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    openNewWindow: this.openNewWindow > 0,
})
```
请求参数：

|         参数          |  类型  |                  说明                  |
| :-------------------: | :----: |:------------------------------------:|
|         type          | 字符串 | 必填，'Stripe.CreditCard'，美服信用卡Stripe支付 |
|         lang          | 字符串 |              必填，'kr'，韩服              |
|      accessToken      | 字符串 |        必填，执行登录后返回的accessToken        |
|        orderId        | 字符串 |            必填，订单创建时获取的订单号            |
|    openNewWindow      |  整数  |      是否新窗口打开，取值!!openNewWindow       |

> 测试卡号 VISA 4242424242424242 (CVC任意数字，日期任意将来日期)  
> 测试卡号 Mastercard 5555555555554444 (CVC任意数字，日期任意将来日期)  
> 测试卡号 JCB 3566002020360505 (CVC任意数字，日期任意将来日期)  
> 参考文档地址 https://stripe.com/docs/testing#cards



## 韩服Paypal支付
> PayPal不支持韩元单位，货币单位使用美元 https://developer.paypal.com/reference/currency-codes/
*  服务器创建订单：  
   请求地址：${服务器地址}/directkr/pp/createOrder  
   请求方式：POST  
   请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)
*  浏览器执行订单：

```javascript
Yo.execOrder({
   type: 'Paypal',
   lang: 'kr',
   accessToken: this.loginInfo.accessToken,
   orderId: this.orderId,
   openNewWindow: this.openNewWindow > 0,
})
```

请求参数

|     参数      |  类型  |            说明             |
| :-----------: | :----: |:-------------------------:|
|     type      | 字符串 |       Paypal:Paypal       |
|     lang      | 字符串 |           kr:韩国           |
|  accessToken  | 字符串 |     登录获取的accessToken      |
|    orderId    | 字符串 |        创建订单的返回的订单号        |
| openNewWindow |  整数  | 是否新窗口打开，取值!!openNewWindow |

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)

> 测试账号及密码：test1@yo-star.com


## Yo.execOrder额外参数
| Yo.execOrder额外参数 | 类型  |      说明      |
| :------------------: | :---: | :------------: |
|  popupWindowOptions  | JSON  | 弹出式窗口参数 |

| popupWindowOptions参数 |  类型  |                                                                       说明                                                                       |
| :--------------------: | :----: | :----------------------------------------------------------------------------------------------------------------------------------------------: |
|    isUsePopupWindow    |  布尔  |                                             是否使用弹出式窗口。如果值为否，则使用判断openNewWindow                                              |
|   popupWindowParams    | 字符串 | window.open参数3， 默认值为"height=600, width=800, top=30%,left=30%, toolbar=no, menubar=no, scrollbars=no, resizable=no,location=no, status=no" |


```javascript
// 示例代码：
Yo.execOrder({
   type: 'Paypal',
   lang: this.payweblang,
   accessToken: this.accessTokenTest || this.loginInfo.accessToken,
   orderId: this.orderId,
   itemName: this.itemName,
   openNewWindow: this.openNewWindow > 0,
   popupWindowOptions: {
      isUsePopupWindow: true,
      popupWindowParams: "height=600, width=800, top=30%,left=30%, toolbar=no, menubar=no, scrollbars=no, resizable=no,location=no, status=no",
   },
})
```  



## 通用查询订单
请求地址：${服务器地址}/pm/info  
请求方式：POST

|  参数   |  类型  |                    说明                    |
| :-----: | :----: |:----------------------------------------:|
| orderId | 字符串 |                   订单id                   |
| rdToken | 字符串 | 订单rdToken（[日服通用创建订单参数](#日服通用创建订单参数)返回参数） |

返回JSON:

| 参数  | 类型  |             说明             |
| :---: | :---: | :--------------------------: |
| state | 整数  |  1：订单成功，其他：不成功   |
| data  | JSON  | 订单信息，~~state为1时有效~~ |

返回JSON的data参数：

|   参数    |  类型  |                 说明                 |
| :-------: | :----: | :----------------------------------: |
|  orderId  | 字符串 |                订单id                |
|  amount   | 字符串 |         订单生成时的amount值         |
| extraData | 字符串 |       订单生成时的extraData值        |
|  errCode  | 字符串 |  最后一次发生错误时的错误码（日本）  |
|  errInfo  | 字符串 | 最后一次发生错误时的错误编号（日本） |


## 正式部署
通用：
* 服务器地址 [https://passport.mahjongsoul.com](https://passport.mahjongsoul.com)
* 浏览器Javascript文件 yo_acc.prod_ja.js

日服：
* 令牌文件服务器地址 [https://p01.mul-pay.jp/ext/js/token.js](https://p01.mul-pay.jp/ext/js/token.js)
* 令牌文件服务器地址，新地址，具有提高的响应速度 [https://static.mul-pay.jp/ext/js/token.js](https://static.mul-pay.jp/ext/js/token.js)
* ShopID: 9200000213740

美服：
* checkoutShopperUrl：[https://checkoutshopper-live.adyen.com](https://checkoutshopper-live.adyen.com)


限制：
*  由于账号安全原因，正式服，第三方登录，限制redirect_uri域名为  
   [game.mahjongsoul.com](game.mahjongsoul.com)  
   [mahjongsoul.game.yo-star.com](mahjongsoul.game.yo-star.com)  
   [gcustest.mahjongsoul.com](gcustest.mahjongsoul.com)  
   [gcjptest.mahjongsoul.com](gcjptest.mahjongsoul.com)  
   [tournament.mahjongsoul.com](tournament.mahjongsoul.com)  
   [mahjongsoul.tournament.yo-star.com](mahjongsoul.tournament.yo-star.com)  
   [mjjpgs.mahjongsoul.com](mjjpgs.mahjongsoul.com)  
   [mjusgs.mahjongsoul.com](mjusgs.mahjongsoul.com)  
   [mjengs.mahjongsoul.com](mjengs.mahjongsoul.com)

* ~~由于正式服第三方支付限制，Yo.generateOriginKey({ originDomain: originDomain }，originDomain 只能控制台手动生成，现在只能取值  
  https://mahjongsoul.game.yo-star.com   
  http://gcustest.mahjongsoul.com  
  如果需要取其他值，需提前通知美服支付管理员生成与配置~~


## 其他返回值

| 参数  | 类型  |             说明             |
| :---: | :---: | :--------------------------: |
| result | 整数  |  -1：参数缺少，参数长度不合法   |


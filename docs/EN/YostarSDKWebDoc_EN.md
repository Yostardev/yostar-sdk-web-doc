# Majsoul应用接口

> [测试服务器地址](#测试服务器地址)  
> [安装示例](#安装示例)  
> [Twitter登录请求](#Twitter登录请求)  
> [Facebook登录请求](#Facebook登录请求)  
> [Google登录请求](#Google登录请求)  
> [Yostar账号登录请求](#Yostar账号登录请求)  
> [执行登录](#执行登录)  
> [验证uid,accessToken](#验证uid,accessToken)  

> [支付流程图](#支付流程图) 

> [日服浏览器CreditCard支付](#日服浏览器CreditCard支付)  
> [日服Paypal支付](#日服Paypal支付)  
> [日服Au支付](#日服Au支付)  
> [日服Docomo支付](#日服Docomo支付)  
> [日服Softbank支付](#日服Softbank支付)  
> [日服通用创建订单参数](#日服通用创建订单参数)  
> [日服支付通知](#日服支付通知)  

> [美服Paypal支付](#美服Paypal支付)  
> [美服MasterCard支付](#美服MasterCard支付)  
> [美服Visa支付](#美服Visa支付)  
> [美服JCB支付](#美服JCB支付)  
> [美服支付宝支付](#美服支付宝支付)  
> [美服通用创建订单参数](#美服通用创建订单参数)  
> [美服支付通知](#美服支付通知)  

> [通用查询订单](#通用查询订单)  
> [正式部署](#正式部署)  


## 测试服务器地址
通用：
* 服务器地址 [https://passporttest.mahjongsoul.com](https://passporttest.mahjongsoul.com)
* 浏览器Javascript文件 yo_acc.stg_ja.js    

日服：  
* 令牌文件服务器地址 [https://pt01.mul-pay.jp/ext/js/token.js](https://pt01.mul-pay.jp/ext/js/token.js)
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
    // window.csf
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


## 支付流程图
* 流程图地址 [https://swimlanes.io/u/OoyQdIV0O](https://swimlanes.io/u/OoyQdIV0O)


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
    itemName: this.itemName
})
```
请求参数  

|    参数     |  类型  |          说明          |
| :---------: | :----: | :--------------------: |
|    type     | 字符串 |     Paypal:Paypal      |
|    lang     | 字符串 |        ja:日本         |
| accessToken | 字符串 | 登录获取的accessToken  |
|   orderId   | 字符串 | 创建订单的返回的订单号 |
|  itemName   | 字符串 |       订单商品名       |
返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)


## 日服Au支付
*  服务器创建订单：  
    请求地址：${服务器地址}/gm/au/createOrder  
    请求方式：POST  
    请求参数：见 [日服通用创建订单参数](#日服通用创建订单参数)  
*  浏览器执行订单：
```javascript
Yo.execOrder({
    type: 'Au',
    lang: this.payweblang,
    accessToken: this.loginInfo.accessToken,
    orderId: this.orderId,
    itemName: this.itemName
})
```
请求参数  

|    参数     |  类型  |          说明          |
| :---------: | :----: | :--------------------: |
|    type     | 字符串 |         Au:Au          |
|    lang     | 字符串 |        ja:日本         |
| accessToken | 字符串 | 登录获取的accessToken  |
|   orderId   | 字符串 | 创建订单的返回的订单号 |
|  itemName   | 字符串 |       订单商品名       |
> 注：Au支付参数 itemName 所有字符必须是全角双字节字符    

返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)


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
})
```
请求参数  

|    参数     |  类型  |          说明          |
| :---------: | :----: | :--------------------: |
|    type     | 字符串 |     Docomo:Docomo      |
|    lang     | 字符串 |        ja:日本         |
| accessToken | 字符串 | 登录获取的accessToken  |
|   orderId   | 字符串 | 创建订单的返回的订单号 |
返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)


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
})
```
请求参数  

|    参数     |  类型  |          说明          |
| :---------: | :----: | :--------------------: |
|    type     | 字符串 |   Softbank:Softbank    |
|    lang     | 字符串 |        ja:日本         |
| accessToken | 字符串 | 登录获取的accessToken  |
|   orderId   | 字符串 | 创建订单的返回的订单号 |
返回：
用户浏览器跳转到支付页面，完成后返回 redirect_uri，见[日服通用创建订单参数](#日服通用创建订单参数)



## 日服通用创建订单参数
* 请求参数：  

|     参数     |  类型  |                             说明                              |
| :----------: | :----: | :-----------------------------------------------------------: |
| accessToken  | 字符串 |               必填，执行登录后返回的accessToken               |
|    amount    | 字符串 |              必填，金额，日服金额为正整数字符串               |
|  extraData   | 字符串 |                  必填，保留，填订单额外信息                   |
| redirect_uri | 字符串 |             必填，订单完成后跳转GET地址，可带参数             |
|  notifyUrl   | 字符串 | 必填，订单完成时POST通知地址，见[日服支付通知](#日服支付通知) |
|     sign     | 字符串 |                        必填，验证参数                         |
|   itemName   | 字符串 |                  商品名，美服必填，日服忽略                   |
> sign生成方式为请求参数accessToken，amount，extraData，redirect_uri，notifyUrl和KEY依次拼接后的MD5值，
KEY的值为'111111'

* 返回JSON：  
  
|  参数   |  类型  |                                     说明                                     |
| :-----: | :----: | :--------------------------------------------------------------------------: |
| orderId | 字符串 |                                    订单id                                    |
| rdToken | 字符串 |                                 订单rdToken                                  |
|  code   |  整数  | 创建失败时返回，<br>90001：未执行购买成功的订单过多，<br>90002：sign验证失败 |
限制用户每小时创建未执行购买成功的订单超过60，则不返回orderId和rdToken，创建订单失败

## 日服支付通知
请求地址：日服创建订单时参数 ${notifyUrl}  
请求方式：POST  
'content-type': 'application/x-www-form-urlencoded'  
通知参数：  

|  参数   |  类型  |  说明  |
| :-----: | :----: | :----: |
| orderId | 字符串 | 订单id |
    
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
    orderId: this.orderId
})
```
请求参数  

|    参数     |  类型  |          说明          |
| :---------: | :----: | :--------------------: |
|    type     | 字符串 |     Paypal:Paypal      |
|    lang     | 字符串 |        en:美国         |
| accessToken | 字符串 | 登录获取的accessToken  |
|   orderId   | 字符串 | 创建订单的返回的订单号 |
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
let originDomain = window.location.href.replace(window.location.search, '').replace(window.location.pathname, '')
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


2.  获取信用卡加密后的信息(Adyen)  
```html
<!-- 示例代码 -->
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
<!-- 
    请求参数：

|     参数     |  类型  |                             说明                              |
| :----------: | :----: | :-----------------------------------------------------------: |
| accessToken  | 字符串 |               必填，执行登录后返回的accessToken               |
|    amount    | 字符串 |              必填，金额，日服金额为正整数字符串               |
|  extraData   | 字符串 |                  必填，保留，填订单额外信息                   |
| redirect_uri | 字符串 |             必填，订单完成后跳转GET地址，可带参数             |
|  notifyUrl   | 字符串 | 必填，订单完成时POST通知地址，见[美服支付通知](#美服支付通知) |

|         sign          | 字符串 |                        必填，验证参数                         |
|       itemName        | 字符串 |                    必填，商品名，美服必填                     |
|  encryptedCardNumber  | 字符串 |                    必填，加密后的信用卡号                     |
| encryptedExpiryMonth  | 字符串 |                  必填，加密后的信用卡过期月                   |
|  encryptedExpiryYear  | 字符串 |                  必填，加密后的信用卡过期年                   |
| encryptedSecurityCode | 字符串 |                  必填，加密后的信用卡安全码                   | 


> sign生成方式为请求参数accessToken，amount，extraData，redirect_uri，notifyUrl和KEY依次拼接后的MD5值，
KEY的值为'111111'
-->

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
})
```
请求参数：

|         参数          |  类型  |                 说明                 |
| :-------------------: | :----: | :----------------------------------: |
|         type          | 字符串 | 必填，'Adyen.Alipay'，美服支付宝支付 |
|         lang          | 字符串 |           必填，'en'，美服           |
|      accessToken      | 字符串 |  必填，执行登录后返回的accessToken   |
|        orderId        | 字符串 |     必填，订单创建时获取的订单号     |

> 测试账号： sandbox_forex1@alipay.com	   111111

## 美服通用创建订单参数
> 参考[日服通用创建订单参数](#日服通用创建订单参数)  

## 美服支付通知
与[日服支付通知](#日服支付通知)相同  

## 通用查询订单
请求地址：${服务器地址}/pm/info  
请求方式：POST  

|  参数   |  类型  |    说明     |
| :-----: | :----: | :---------: |
| orderId | 字符串 |   订单id    |
| rdToken | 字符串 | 订单rdToken |
返回JSON:  

| 参数  | 类型  |           说明           |
| :---: | :---: | :----------------------: |
| state | 整数  |   1：订单成功，其他：不成功   |
| data  | JSON  | 订单信息，state为1时有效 |
返回JSON的data参数：  

|   参数    |  类型  |          说明           |
| :-------: | :----: | :---------------------: |
|  orderId  | 字符串 |         订单id          |
|  amount   | 字符串 |  订单生成时的amount值   |
| extraData | 字符串 | 订单生成时的extraData值 |


## 正式部署
通用：
* 服务器地址 ~~[https://passport.mahjongsoul.com](https://passport.mahjongsoul.com)~~（待定）
* 浏览器Javascript文件 yo_acc.prod_ja.js  
  
日服：  
* 令牌文件服务器地址 [https://p01.mul-pay.jp/ext/js/token.js](https://p01.mul-pay.jp/ext/js/token.js)
* ShopID: ~~tshop00037465~~（待定）

美服：  
* checkoutShopperUrl：~~[https://checkoutshopper-live.adyen.com](https://checkoutshopper-live.adyen.com)~~（待定）


# Yostar Account Document

| Date | Verions | Description | Author | Editor |
| :---: | :---: | :---: |  :---: | :---: |
| 2019-2-20 | V1.0.0 | first edition |   |   |

### install
```html
<script src="js/yo_acc.js"></script>
```

#### Js Usage 
```javascript
var Yo = windows.Yo;
```

### Api Request Method
```html
Yo.api(params, callback)
```
### Request params
| Api | params | type | description |
| :---: | :---: | :---: | :---: |
| Yo.request(params, callback) | account | string | email  |
| Yo.submit(params, callback)  | account | string | email  |
|                              | code    | string | verification code    |
| Yo.debug(params, callback)   | uid     | string | user id    |
|                              | token   | string | user token |



### Return callbackResult Params

| callbackResult | type | description | Api |
| :---: | :---: | :---: | :---: | 
| code | number | return code  | Yo.request<br> |
| data | object | return data  | Yo.request |
| message  | string | message    | Yo.request |

### Return callbackResult.code 
| code | description |
| :---: | :---: | 
| 20000 | SUCCESS | 
| 30001 | account error |
| 50003 | account verification frequency limit |
| 50004 | account banned |
| 50016 | account verification failed |
| 50009 | account verification count limit |
| 50005 | uid,Token not match |

### Return callbackResult.data

| callbackResult | type | description | Api |
| :---: | :---: | :---: | :---: | 
| uid | string | uid data | Yo.submit, Yo.debug |
| account | string | account data  | Yo.submit, Yo.debug |
| token  | string | token data | Yo.submit, Yo.debug |



### Request api Sample
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

### Server uid, token Verification
> ```
> Send uid,token to https://uc.yo-star.com:3020/account/debug_token
> Return callbackResult
> ```
```bash
Sample
curl --request POST \
  --url https://uc.yo-star.com:3020/account/debug_token \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --data 'uid=11912523927&token=11912523927-S8jvAb56gAQ5XKozEdVTMiQGHYwfQvZgixMSLq2XbX6C8uNySpdiuTjdmZwMdQCBxkjTYjXkDuBzzUlyK11UVg'
```

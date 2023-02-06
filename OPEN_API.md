# exPay 开放接口文档 


## 一、充值下单接口
​    
### 1 接口名称  

发起充值订单接口    

### 2 接口描述    

- 发起充值订单接口  
- 提供充值信息生成


### 3 请求地址  

`{apiAddress}/api/orderPayment`  

### 4 请求方式  

**POST**  

### 5 请求参数  

#### 5.1 Header 参数  

| 参数名       | 必选 | 类型/参数值      | 说明         |
| ------------ | ---- | ---------------- | ------------ |
| Content-Type | 是   | application/json | 请求参数类型 |

#### 5.2 Body 参数  

| 参数名    | 必选 | 类型   | 限制条件        | 说明     |
| --------- | ---- | ------ | --------------- | -------- |
| merchantId   | 是   | string | 1 < length < 60 | 商户ID |
| orderTime  | 是   | Long | 无 | 下单时间     |
| notifyUrl | 是   | string | 无      | 进行通知充值到账的接口   |
| userId | 否   | string | 无      | 用户ID   |
| userIp | 否   | string | 无      | 用户IP   |
| amount | 是   | decimal | 无      | 充值金额   |
| model | 否   | integer | 1信息2收银台      | 充值模式 默认为收银台模式   |
| merchantOrderId | 是   | string | 1 < length < 60      | 商户订单号   |
| sign | 是   | string | 无      | 签名   |


**sign生成方式**:  
**注意事项**: sign无需参与签名


 ```
    下单参数根据参数名英文字母顺序排序, 使用&PARAMNAME=格式进行拼接, 最后拼接apikey(直接拼接), 生成加密前字符串
    
    例:amount=10000&merchantId=merchant001&merchantOrderId=042df7ed222e4f50900340189b55f8d2&notifyUrl=http://www.baidu.com&orderTime=1673256454056&userId=MOCK&userIp=127.0.0.1faasfasda
    
    然后使用MD5进行加密, 生成最终sign
    
 ```


### 6 返回示例  

```json
信息模式:

{
    "code": 200,  // 状态码
    "message": "成功",  // 提示信息
    "data":{  //返回内容
        "paymentOrderId":"MENT23421302514946852",
        "merchantOrderId":"9ac1d56d3ceb4072bc277cf7d44a54ff",
        "amount":100,
        "createTime":"2023-01-11 01:48:35",
        "bankAccountNumber":"8888888888888889",
        "bankName":"中国农业银行",
        "bankSimpleName":"ABC"
    } 
}
-----------------------------------------------
收银台模式:

{
    "code": 200,  // 状态码
    "message": "成功",  // 提示信息
    "data": 'https://domain.one/toPay?pat=2141f1snj94712hkj'
}
```

### 7 回调参数
```
{
        "paymentOrderId":"MENT22102935311674803",
        "merchantOrderId":"3dfc325ac6714ba586d1029fc66d15a4",
        "merchantId":"merchant001",
        "amount":100.16,
        "orderTime":null,
        "userId":null,
        "userIp":null,
        "state":3,
        "sign":"39492F1684741D7A05569A75E69DFA2A"
    } 

```


## 二、提款下单接口

### 1 接口名称  

发起提款订单接口

### 2 接口描述    

- 发起提款订单接口  
- 提供提款信息生成


### 3 请求地址  

`{apiAddress}/api/orderWithdraw`  

### 4 请求方式  

**POST**  

### 5 请求参数  

#### 5.1 Header 参数  

| 参数名       | 必选 | 类型/参数值      | 说明         |
| ------------ | ---- | ---------------- | ------------ |
| Content-Type | 是   | application/json | 请求参数类型 |

#### 5.2 Body 参数  

| 参数名    | 必选 | 类型   | 限制条件        | 说明     |
| --------- | ---- | ------ | --------------- | -------- |
| merchantId   | 是   | string | 1 < length < 60 | 商户ID |
| orderTime  | 是   | Long | 无 | 下单时间     |
| notifyUrl | 是   | string | 无      | 进行通知充值到账的接口   |
| userId | 否   | string | 无      | 用户ID   |
| userIp | 否   | string | 无      | 用户IP   |
| amoutn | 是   | decimal | 无      | 提款金额   |
| merchantOrderId | 是   | string | 1 < length < 60      | 商户订单号   |
| withdrawBankAccountNumber | 是   | string | 1 < length < 60      | 提款银行账户号   |
| withdrawBank | 是   | integer | 参考 post https://client.expay.one/api/bankAccount/findAllBank      | 提款银行   |
| withdrawBankAccountName | 是   | string | 1 < length < 60      | 提款银行账户姓名   |
| sign | 是   | string | 无      | 签名   |


**sign生成方式**:  
**注意事项**: sign无需参与签名


 ```
    下单参数根据参数名英文字母顺序排序, 使用&PARAMNAME=格式进行拼接, 最后拼接apikey(直接拼接), 生成加密前字符串
    
    例:amount=1001&merchantId=merchant001&merchantOrderId=9e78e96322e040ea90f57893c652a6a2&notifyUrl=http://www.baidu.com&orderTime=1673504476112&userId=MOCK&userIp=127.0.0.1&withdrawBank=1&withdrawBankAccountName=王某人&withdrawBankAccountNumber=77777777777777777faasfasda
    
    然后使用MD5进行加密, 生成最终sign
    
 ```


### 6 返回示例  

```json
{
    "code": 200,  // 状态码
    "message": "成功",  // 提示信息
    "data":null 
}
```

## 三、充值查单接口

### 1 接口名称  

充值查单接口

### 2 接口描述    

- 提供商户号和充值订单号进行查单


### 3 请求地址  

`{apiAddress}/api/getPaymentOrder`  

### 4 请求方式  

**POST**  

### 5 请求参数  

#### 5.1 Header 参数  

| 参数名       | 必选 | 类型/参数值      | 说明         |
| ------------ | ---- | ---------------- | ------------ |
| Content-Type | 是   | application/json | 请求参数类型 |

#### 5.2 Body 参数  

| 参数名    | 必选 | 类型   | 限制条件        | 说明     |
| --------- | ---- | ------ | --------------- | -------- |
| merchantId   | 是   | string | 1 < length < 60 | 商户ID |
| merchantOrderId | 是   | string | 1 < length < 60      | 商户订单号   |
| sign | 是   | string | 无      | 签名   |


**sign生成方式**:  
**注意事项**: sign无需参与签名


 ```
    下单参数根据参数名英文字母顺序排序, 使用&PARAMNAME=格式进行拼接, 最后拼接apikey(直接拼接), 生成加密前字符串
    
    例:merchantId=merchant001&merchantOrderId=3dfc325ac6714ba586d1029fc66d15a4
    
    然后使用MD5进行加密, 生成最终sign
    
 ```


### 6 返回示例  

```json
{
    "code": 200,  // 状态码
    "message": "成功",  // 提示信息
    "data":{
        "paymentOrderId":"MENT22102935311674803",
        "merchantOrderId":"3dfc325ac6714ba586d1029fc66d15a4",
        "merchantId":"merchant001",
        "amount":100.16,
        "orderTime":null,
        "userId":null,
        "userIp":null,
        "state":3,
        "sign":"39492F1684741D7A05569A75E69DFA2A"
    } 
}
```
​    
## 四、提款查单接口

### 1 接口名称  

提款查单接口

### 2 接口描述    

- 提供商户号和提款订单号进行查单


### 3 请求地址  

`{apiAddress}/api/getWithdrawOrder`  

### 4 请求方式  

**POST**  

### 5 请求参数  

#### 5.1 Header 参数  

| 参数名       | 必选 | 类型/参数值      | 说明         |
| ------------ | ---- | ---------------- | ------------ |
| Content-Type | 是   | application/json | 请求参数类型 |

#### 5.2 Body 参数  

| 参数名    | 必选 | 类型   | 限制条件        | 说明     |
| --------- | ---- | ------ | --------------- | -------- |
| merchantId   | 是   | string | 1 < length < 60 | 商户ID |
| merchantOrderId | 是   | string | 1 < length < 60      | 商户订单号   |
| sign | 是   | string | 无      | 签名   |


**sign生成方式**:  
**注意事项**: sign无需参与签名


 ```
    下单参数根据参数名英文字母顺序排序, 使用&PARAMNAME=格式进行拼接, 最后拼接apikey(直接拼接), 生成加密前字符串
    
    例:merchantId=merchant001&merchantOrderId=9e78e96322e040ea90f57893c652a6a2faasfasda
    
    然后使用MD5进行加密, 生成最终sign
    
 ```


### 6 返回示例  

```json
{
    "code": 200,  // 状态码
    "message": "成功",  // 提示信息
    "data":{
        "withdrawOrderId":"DRAW23421304476623774",
        "merchantOrderId":"9e78e96322e040ea90f57893c652a6a2",
        "merchantId":"merchant001",
        "amount":1001.00,
        "orderTime":1673504476,
        "userId":"MOCK",
        "userIp":"127.0.0.1",
        "state":0,
        "sign":"83FA6AC685D32299701114B740C82FC7"
    } 
}
```

####  状态码  


 状态码 | 类型   
| ---- | ---- | 
| 200 | 成功 |  
| 202 | 未知错误 |
| 202 | 失败 |  

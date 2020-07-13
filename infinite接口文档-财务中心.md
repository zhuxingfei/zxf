# INFINITE平台 软件需求


**简介**:INFINITE平台 软件需求


**HOST**:localhost:8081


**联系人**: 王鹏超


**Version**:1.0.0


**接口路径**:/v2/api-docs?group=财务中心


[TOC]






# 财务中心


## in币余额


**接口地址**:`/api/finance/inCoinsBalance`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**:获取in币余额


#### 请求

无



#### 响应


**响应状态**:


| 业务码 | 说明 | 备注 |
| -------- | -------- | ----- |
|General.Success|接口调用成功||
|General.Failure|接口调用失败||
|General.InternalServerError|服务器异常||
|General.RpcServerError|Rpc服务异常||
|General.TokenExpired|账户Token已超时||
|General.TokenInvalid|账户Token无效||
|General.Unauthorized|请求未授权||


**响应业务码-General.Success**:


**响应参数**:


| 参数名称                                       | 参数说明       | 类型           | 备注 |
| ---------------------------------------------- | -------------- | -------------- | ---- |
| code                                           | 业务代码       | string         |      |
| data                                           | 承载数据       |                |      |
| &emsp;&emsp;&emsp;&emsp;balance                | in币余额  (单位:分)     | long     |      |
| msg                                            | 返回消息       | string         |      |

**响应示例**:

```javascript
{
	"code": "General.Success",
	"data": {
	    "balance": 8585
	}
	"msg": "接口调用成功"
}
```



**响应业务码-General.TokenInvalid**:


**响应参数**:


| 参数名称 | 参数说明 | 类型 | 备注 |
| -------- | -------- | ----- |----- |
|code|业务代码|string||
|data|承载数据|object||
|msg|返回消息|string||


**响应示例**:
```javascript
{
    "code": "General.ParameterInvalid",
    "data": {
        "Account not logged in"
    },
    "msg": "Account not logged in"
}
```





## in币余额收支明细列表


**接口地址**:`/api/finance/getInCoinsDetailList`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**: 获取三个月内in币余额收支明细列表

**请求参数**:


| 参数名称  | 参数说明 | 必输项描述 | 数据类型       | 备注 |
| --------- | -------- | ---------- | -------------- | ---- |
| orderType  | 订单类型 （orderType.sysGive、orderType.userRecharge，若不传则查询全部类型）  | N           | String |      |

**请求示例**:


```javascript
{
	"orderType": "orderType.sysGive"
}
```



#### 响应


**响应状态**:


| 业务码 | 说明 | 备注 |
| -------- | -------- | ----- |
|General.Success|接口调用成功||
|General.Failure|接口调用失败||
|General.InternalServerError|服务器异常||
|General.RpcServerError|Rpc服务异常||
|General.TokenExpired|账户Token已超时||
|General.TokenInvalid|账户Token无效||
|General.Unauthorized|请求未授权||
|General.ParameterInvalid|参数校验失败||
|General.NotFound|NotFound||


**响应业务码-General.Success**:

**响应参数**:


| 参数名称              | 参数说明 | 类型 | 备注 |
| --------------------- | -------- | ----- |----- |
|code                   |业务代码|string|| 
|&emsp;&emsp;resultSet|结果集|array||
|&emsp;&emsp;&emsp;&emsp;transactionCode|交易编号|string(255)||
|&emsp;&emsp;&emsp;&emsp;orderCode|关联订单|string(255)||
|&emsp;&emsp;&emsp;&emsp;orderType|订单类型|string(255)||
|&emsp;&emsp;&emsp;&emsp;createDatetime|创建时间|string(date-time)||
|&emsp;&emsp;&emsp;&emsp;dynamicType|金额变动类型|string(255)||
|&emsp;&emsp;&emsp;&emsp;dynamicAmount|金额变动金额(单位：分)|long||
|&emsp;&emsp;&emsp;&emsp;currentBalance|变动后余额(单位：分)|long||
|msg                    |返回消息|string||

**数据字典**:


| 参数名称                | 参数值                    | 描述     | 默认值 | 分类代码       |
| ----------------------- | ----------------          | ------   | ------ | -------------- |
| &emsp;&emsp;dynamicType | dynamicType.expend             | 出账     |        | sys.db.infiniteOrder |
|                         | dynamicType.income               | 入账     |        |                |
| &emsp;&emsp;orderType   | orderType.userRecharge       | 用户充值 |        | sys.db.infiniteOrder |
|                         | orderType.sysGive        | 系统赠送 |        |                |

**响应示例**:

```javascript
{
	"code": "General.Success",
	"data": {
		"resultSet": [
			{
				"transactionCode": "3113523513121653132",
				"orderCode": "3113523513121653132",
				"bizType": "orderType.sysGive",
				"createDatetime": "2020-04-28 12:12:12",
				"dynamicType": "Type.income",
				"dynamicAmount": 500,
				"currentBalance": 999898
			}
		]
	},
	"msg": "接口调用成功"
}
```



**响应业务码-General.TokenInvalid**:


**响应参数**:


| 参数名称 | 参数说明 | 类型 | 备注 |
| -------- | -------- | ----- |----- |
|code|业务代码|string||
|data|承载数据|object||
|msg|返回消息|string||


**响应示例**:
```javascript
{
    "code": "General.ParameterInvalid",
    "data": {
        "Account not logged in"
    },
    "msg": "Account not logged in"
}
```



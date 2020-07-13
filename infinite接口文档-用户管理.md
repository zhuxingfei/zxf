# infinite平台 接口文档

**简介**:infinite平台 接口文档


**HOST**:localhost:8081


**联系人**: liucheng


**Version**:1.0.0

**接口路径**:/v2/api-docs?group=用户管理






























[TOC]






# 用户管理


## 登录


**接口地址**:`/api/user/login`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**: 账号密码登录，邮箱密码登录，前端保存Token，并在后面的所有API请求中,带到Header中去,key=Authorization

用户同时登陆infinite，gitea两个平台


#### 请求


**请求参数**:


| 参数名称                    | 参数说明     | 必输项描述 | 数据类型    | 备注               |
| --------------------------- | ------------ | ---------- | ----------- | ------------------ |
| &emsp;&emsp;email           | 邮箱         | O          | string(255) | 邮箱验证码登录必输 |
| &emsp;&emsp;username        | 用户名       | O          | string(255) | 用户名密码登录必输 |
| &emsp;&emsp;password        | 密码         | Y          | string(32)  | 用户名密码登录必输 |
| &emsp;&emsp;enableKeepLogin | 记住登录状态 | N          | boolean     |                    |


**数据字典**:


| 参数名称                    | 参数值 | 描述                       | 默认值 | 分类代码 |
| --------------------------- | ------ | -------------------------- | ------ | ------ |
| &emsp;&emsp;enableKeepLogin | keepLogin.enable  | 不记住登录状态,默认token   | √      | sys.db.sysUser |
| &emsp;&emsp;                | keepLogin.disable   | 记住登录状态,保留7天token |        ||



**请求示例-用户名密码登录**:


```javascript
{
	"username": "admin",
	"password": "888888",
	"enableKeepLogin ": "keepLogin.disable"
}
```


**请求示例-邮箱验证码登录**:


```javascript
{
	"email": "test@qq.com",
	"password": "888888",
	"enableKeepLogin ": "keepLogin.enable"
}
```


#### 响应


**响应状态**:


| 业务码                      | 说明          | 备注 |
| --------------------------- | ------------- | ---- |
| General.Success             | 接口调用成功  |      |



| General.Failure             | 接口调用失败  |      |
| General.InternalServerError | 服务器异常    |      |
| General.RpcServerError      | Rpc服务异常   |      |
| General.GiteaServerError    | Gitea服务异常 |      |
| General.ParameterInvalid    | 参数校验失败  |      |
| Account.VerifyError         | 账户检验失败  |      |


**响应业务码-General.Success**:


**响应参数**:


| 参数名称                   | 参数说明          | 类型              | 备注                |
| -------------------------- | ----------------- | ----------------- | ------------------- |
| code                       | 业务代码          | string            |                     |
| data                       | 承载数据          | object            |                     |
| &emsp;&emsp;accessToken    | infinite准入token | string(128)       |                     |
| &emsp;&emsp;giteaToken     | gitea准入token    | string(128)       |                     |
| &emsp;&emsp;storageToken   | 存储准入token     | string(128)       |                     |
| &emsp;&emsp;createDatetime | 创建时间          | string(date-time) | yyyy-MM-dd HH:mm:ss |
| &emsp;&emsp;nickname       | 昵称              | string(255)       |                     |
| &emsp;&emsp;accountId      | 账号ID            | string(14)        |                     |
| &emsp;&emsp;username       | 用户名            | string(255)       |                     |
| &emsp;&emsp;email          | 邮箱地址          | string(255)       |                     |
| &emsp;&emsp;mobile         | 安全手机          | string(11)        |                     |
| &emsp;&emsp;emailVerified  | 邮箱是否验证      | string(1)         |                     |
| &emsp;&emsp;loginIp        | 登陆IP            | string(255)       |                     |
| &emsp;&emsp;loginDevice    | 登陆设备          | string(255)       |                     |
| &emsp;&emsp;status         | 状态              | integer(11)       |                     |
| &emsp;&emsp;updateDatetime | 更新时间          | string(date-time) | yyyy-MM-dd HH:mm:ss |
| &emsp;&emsp;userId         | 用户id            | long              |                     |
| msg                        | 返回消息          | string            |                     |


**数据字典**:


| 参数名称 | 参数值 | 描述 | 默认值 | 分类代码 |
| ------------------------- | ------ | -------- | ------ |
| &emsp;&emsp;emailVerified | email.verified | 未验证   | sys.db.sysUser |
| &emsp;&emsp;              | email.unUerified | 已验证   |        |
| &emsp;&emsp;              |        |          |        |
| &emsp;&emsp;status        | status.normal | 正常     | sys.db.sysUser |
| &emsp;&emsp;              | status.pause | 暂停使用 |        |
| &emsp;&emsp;              | status.lock | 锁定     |        |
| &emsp;&emsp;              | status.stop | 停用     |        |
| &emsp;&emsp;              | status.delete | 已删除   |        |


**响应示例**:


```javascript
{
	"code": "General.Success",
	"data": {
		"accessToken": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxIiwiZXhwIjoxNTgzOTg3NDU1fQ.WrYlBu1mOZMQtPg8KWGEbiMBdYa-RCKLm_fORvAEg24",
        "giteaToken": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxIiwiZXhwIjoxNTgzOTg3NDU1fQ.WrYlBu1mOZMQtPg8KWGEbiMBdYa-RCKLm_fORvAEg24",
        "storageToken": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxIiwiZXhwIjoxNTgzOTg3NDU1fQ.WrYlBu1mOZMQtPg8KWGEbiMBdYa-RCKLm_fORvAEg24",
		"createDatetime": "1970-01-01 12:00:00",
		"nickname": "测试",
        "accountId": "20042908291234",
		"username": "admin"
		"email": "test@qq.com",
		"mobile": "18625160000",
		"emailVerified": "email.verified",
		"iconUrl": "https://i.picsum.photos/id/1005/100/100.jpg",
		"loginIp": "[2020-04-29 08:38:23.132] IP地址 129.0.1.22",
		"loginDevice": "MAC: 00-D0-F8-00-00-01",
		"status": "status.normal",
		"updateDatetime": "1970-01-01 12:00:00",
		"userId": "676803719341408300"
	},
	"msg": "接口调用成功"
}
```


**响应业务码-Account.VerifyError**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "Account.VerifyError",
	"data": {},
	"msg": "账户检验失败"
}
```


## 注销


**接口地址**:`/api/user/logout`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**:根据head中(key=Authorization)的值注销用户

用户同时注销infinite，gitea两个平台登录状态


#### 请求


**请求参数**:


暂无


#### 响应


**响应状态**:


| 业务码                      | 说明            | 备注      |
| --------------------------- | --------------- | --------- |
| General.Success             | 接口调用成功    |           |
| General.Failure             | 接口调用失败    |           |
| General.InternalServerError | 服务器异常      |           |
| General.RpcServerError      | Rpc服务异常     |           |
| General.GiteaServerError    | Gitea服务异常   |           |
| General.TokenExpired        | 账户Token已超时 |           |
| General.TokenInvalid        | 账户Token无效   |           |
| General.ParameterInvalid    | 参数校验失败    | token为空 |


**响应业务码-General.Success**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.Success",
	"data": {},
	"msg": "接口调用成功"
}
```


**响应业务码-General.ParameterInvalid**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.ParameterInvalid",
	"data": {},
	"msg": "参数校验失败"
}
```


## 发送邮件验证码


**接口地址**:`/api/user/emailVerifyCode`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**: 向目标邮箱发送验证码


#### 请求


**请求参数**:


| 参数名称          | 参数说明 | 必输项描述 | 数据类型    | 备注 |
| ----------------- | -------- | ---------- | ----------- | ---- |
| &emsp;&emsp;email | 邮箱     | Y          | string(255) |      |


**请求示例**:


```javascript
{
	"email": "test@qq.com"
}
```


#### 响应


**响应状态**:


| 业务码                      | 说明         | 备注 |
| --------------------------- | ------------ | ---- |
| General.Success             | 接口调用成功 |      |
| General.Failure             | 接口调用失败 |      |
| General.InternalServerError | 服务器异常   |      |
| General.RpcServerError      | Rpc服务异常  |      |
| General.ParameterInvalid    | 参数校验失败 |      |


**响应业务码-General.Success**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:

```javascript
{
	"code": "General.Success",
	"data": {},
	"msg": "接口调用成功"
}
```


**响应业务码-General.ParameterInvalid**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.ParameterInvalid",
	"data": {},
	"msg": "参数校验失败"
}
```


## 注册


**接口地址**:`/api/user/registerIndividual`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**: 使用用户名邮箱和密码在gitea，infinite和存储三个平台创建账号


#### 请求


**请求参数**:


| 参数名称             | 参数说明 | 必输项描述 | 数据类型    | 备注 |
| -------------------- | -------- | ---------- | ----------- | ---- |
| &emsp;&emsp;username | 用户名   | Y          | string(255) |      |
| &emsp;&emsp;email    | 邮箱     | Y          | string(255) |      |
| &emsp;&emsp;password | 密码     | Y          | string(32)  |      |


**请求示例**:


```javascript
{
	"username": "admin",
	"email": "test@qq.com",
	"password": "1qazxsw2"
}
```


#### 响应


**响应状态**:


| 业务码                      | 说明          | 备注 |
| --------------------------- | ------------- | ---- |
| General.Success             | 接口调用成功  |      |
| General.Failure             | 接口调用失败  |      |
| General.InternalServerError | 服务器异常    |      |
| General.RpcServerError      | Rpc服务异常   |      |
| General.GiteaServerError    | Gitea服务异常 |      |
| General.ParameterInvalid    | 参数校验失败  |      |
| General.UserRepeat          | 用户名已存在  |      |
| General.EmailRepeat         | 邮箱已被使用  |      |


**响应业务码-General.Success**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.Success",
	"data": {},
	"msg": "接口调用成功"
}
```


**响应业务码-General.ParameterInvalid**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.ParameterInvalid",
	"data": {},
	"msg": "参数校验失败"
}
```


## 用户信息


**接口地址**:`/api/user/getUserDetail`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**: 根据head中(key=Authorization)的值确认登陆状态，再由用户标识获取用户信息


#### 请求


**请求参数**:


无


#### 响应


**响应状态**:


| 业务码                      | 说明            | 备注      |
| --------------------------- | --------------- | --------- |
| General.Success             | 接口调用成功    |           |
| General.Failure             | 接口调用失败    |           |
| General.InternalServerError | 服务器异常      |           |
| General.RpcServerError      | Rpc服务异常     |           |
| General.TokenExpired        | 账户Token已超时 |           |
| General.TokenInvalid        | 账户Token无效   |           |
| General.ParameterInvalid    | 参数校验失败    | token为空 |


**响应业务码-General.Success**:


**响应参数**:


| 参数名称                   | 参数说明     | 类型              | 备注                |
| -------------------------- | ------------ | ----------------- | ------------------- |
| code                       | 业务代码     | string            |                     |
| data                       | 承载数据     | object            |                     |
| &emsp;&emsp;createDatetime | 创建时间     | string(date-time) | yyyy-MM-dd HH:mm:ss |
| &emsp;&emsp;nickname       | 昵称         | string(255)       |                     |
| &emsp;&emsp;accountId      | 账号ID       | string(14)        |                     |
| &emsp;&emsp;username       | 用户名       | string(255)       |                     |
| &emsp;&emsp;email          | 邮箱地址     | string(255)       |                     |
| &emsp;&emsp;mobile         | 安全手机     | string(11)        |                     |
| &emsp;&emsp;emailVerified  | 邮箱是否验证 | string(1)         |                     |
| &emsp;&emsp;loginIp        | 登陆IP       | string(255)       |                     |
| &emsp;&emsp;loginDevice    | 登陆设备     | string(255)       |                     |
| &emsp;&emsp;status         | 状态         | integer(11)       |                     |
| &emsp;&emsp;updateDatetime | 更新时间     | string(date-time) | yyyy-MM-dd HH:mm:ss |
| &emsp;&emsp;userId         | 用户id       | long              |                     |
| msg                        | 返回消息     | string            |                     |


**数据字典**:


| 参数名称                  | 参数值 | 描述     | 默认值 |
| ------------------------- | ------ | -------- | ------ |
| &emsp;&emsp;emailVerified | 1      | 未验证   |        |
| &emsp;&emsp;              | 2      | 已验证   |        |
| &emsp;&emsp;              |        |          |        |
| &emsp;&emsp;status        | 1      | 正常     |        |
| &emsp;&emsp;              | 2      | 暂停使用 |        |
| &emsp;&emsp;              | 3      | 锁定     |        |
| &emsp;&emsp;              | 4      | 停用     |        |
| &emsp;&emsp;              | 5      | 已删除   |        |


**响应示例**:


```javascript
{
	"code": "General.Success",
	"data": {
		"createDatetime": "1970-01-01 12:00:00",
		"nickname": "测试",
        "accountId": "20042908291234",
		"username": "admin"
		"email": "test@qq.com",
		"mobile": "18625160000",
		"emailVerified": 0,
		"iconUrl": "https://i.picsum.photos/id/1005/100/100.jpg",
		"loginIp": "[2020-04-29 08:38:23.132] IP地址 129.0.1.22",
		"loginDevice": "MAC: 00-D0-F8-00-00-01",
		"status": "1",
		"updateDatetime": "1970-01-01 12:00:00",
		"userId": 676803719341408300
	},
	"msg": "接口调用成功"
}
```


**响应业务码-General.ParameterInvalid**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.ParameterInvalid",
	"data": {},
	"msg": "参数校验失败"
}
```


## 修改资料


**接口地址**:`/api/user/editUser`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**: 更新infinite和gitea中用户个人信息


头像上传走文件上传接口后，更新个人资料时，提供头像链接更新头像


#### 请求


**请求参数**:


| 参数名称               | 参数说明 | 必输项描述 | 数据类型     | 备注 |
| ---------------------- | -------- | ---------- | ------------ | ---- |
| &emsp;&emsp;nickname   | 账号昵称 | Y          | string(255)  |      |
| &emsp;&emsp;avatarUrl  | 头像链接 | Y          | string(255) |      |
| &emsp;&emsp;description | 个人简介 | Y          | string(50)   |      |
| &emsp;&emsp;website    | 个人网站 | Y          | string(50)   |      |
| &emsp;&emsp;location   | 所在地区 | Y          | string(50)   |      |


**请求示例**:


```javascript
{
	"nickname": "测试",
	"avatarUrl": "https://i.picsum.photos/id/1005/100/100.jpg",
    "description": "小菜鸟",
    "website": "http://www.baidu.com",
    "location": "China"
}
```


#### 响应


**响应状态**:


| 业务码                      | 说明         | 备注 |
| --------------------------- | ------------ | ---- |
| General.Success             | 接口调用成功 |      |
| General.Failure             | 接口调用失败 |      |
| General.InternalServerError | 服务器异常   |      |
| General.RpcServerError      | Rpc服务异常  |      |
| General.ParameterInvalid    | 参数校验失败 |      |


**响应业务码-General.Success**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.Success",
	"data": {},
	"msg": "接口调用成功"
}
```


**响应业务码-General.ParameterInvalid**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.ParameterInvalid",
	"data": {},
	"msg": "参数校验失败"
}
```


## 重置密码


**接口地址**:`/api/user/resetUserPassword`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**: 忘记密码时，通过邮箱和邮箱验证码重置用户infinite和gitea密码


#### 请求


**请求参数**:


| 参数名称               | 参数说明 | 必输项描述 | 数据类型    | 备注 |
| ---------------------- | -------- | ---------- | ----------- | ---- |
| &emsp;&emsp;email      | 邮箱     | Y          | string(255) |      |
| &emsp;&emsp;password   | 密码     | Y          | string(32)  |      |
| &emsp;&emsp;verifyCode | 验证码   | Y          | string(16)  |      |


**请求示例**:


```javascript
{
	"email": "test@qq.com",
	"password": "1qazxsw2",
	"verifyCode": "1234"
}
```


#### 响应


**响应状态**:


| 业务码                      | 说明         | 备注 |
| --------------------------- | ------------ | ---- |
| General.Success             | 接口调用成功 |      |
| General.Failure             | 接口调用失败 |      |
| General.InternalServerError | 服务器异常   |      |
| General.RpcServerError      | Rpc服务异常  |      |
| General.GiteaServerError    | Gitea服务异常|      |
| General.ParameterInvalid    | 参数校验失败 |      |


**响应业务码-General.Success**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.Success",
	"data": {},
	"msg": "接口调用成功"
}
```


**响应业务码-General.ParameterInvalid**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.ParameterInvalid",
	"data": {},
	"msg": "参数校验失败"
}
```


## 更换邮箱


**接口地址**:`/api/user/modifyUserEmail`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**: 更换infinite和gitea的登录邮箱信息


#### 请求


**请求参数**:


| 参数名称          | 参数说明 | 必输项描述 | 数据类型    | 备注 |
| ----------------- | -------- | ---------- | ----------- | ---- |
| &emsp;&emsp;password |密码     | Y          | string(16) |      |
| &emsp;&emsp;oriEmail | 原邮箱     | Y          | string(255) |      |
| &emsp;&emsp;email | 新邮箱 | Y | string(255) | |
| &emsp;&emsp;verifyCode| 验证码     | Y          | string(16) |      |


**请求示例**:


```javascript
{
	"password": "***",
	"oriEmail": "test@qq.com",
	"email": "test1@qq.com",
	"verifyCode": "asdasv"
}
```


#### 响应


**响应状态**:


| 业务码                      | 说明           | 备注 |
| --------------------------- | -------------- | ---- |
| General.Success             | 接口调用成功   |      |
| General.Failure             | 接口调用失败   |      |
| General.InternalServerError | 服务器异常     |      |
| General.RpcServerError      | Rpc服务异常    |      |
| General.GiteaServerError    | Gitea服务异常  |      |
| General.ParameterInvalid    | 参数校验失败    |      |
| Account.VerifyCodeError     | 验证码检验失败  |      |
| General.ParameterRepeat     | 参数重复       |      |
| General.EmailRepeat         | 邮箱已被使用   |      |


**响应业务码-General.Success**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.Success",
	"data": {},
	"msg": "接口调用成功"
}
```


**响应业务码-General.ParameterInvalid**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.ParameterInvalid",
	"data": {},
	"msg": "参数校验失败"
}
```


## 密码修改


**接口地址**:`/api/user/modifyUserPassword`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**: 登陆情况下的旧密码更新为新密码


#### 请求


**请求参数**:


| 参数名称                | 参数说明 | 必输项描述 | 数据类型   | 备注                               |
| ----------------------- | -------- | ---------- | ---------- | ---------------------------------- |
| &emsp;&emsp;oriPassword | 原密码   | Y          | string(32) |                                    |
| &emsp;&emsp;password    | 新密码   | Y          | string(32) | 密码规则：8-16位数字和英文字符组合 |


**请求示例**:


```javascript
{
	"password": "123456q",
	"oriPassword": "2wsxza1"
}
```


#### 响应


**响应状态**:


| 业务码                      | 说明         | 备注 |
| --------------------------- | ------------ | ---- |
| General.Success             | 接口调用成功 |      |
| General.Failure             | 接口调用失败 |      |
| General.InternalServerError | 服务器异常   |      |
| General.RpcServerError      | Rpc服务异常  |      |
| General.GiteaServerError    | Gitea服务异常|      |
| General.ParameterInvalid    | 参数校验失败 |      |
| General.ParameterRepeat     | 参数重复     |      |


**响应业务码-General.Success**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.Success",
	"data": {},
	"msg": "接口调用成功"
}
```


**响应业务码-General.ParameterInvalid**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.ParameterInvalid",
	"data": {},
	"msg": "参数校验失败"
}
```


## 账号注销


**接口地址**:`/api/user/deleteUser`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**: 注销gitea，infinite和存储三个平台账号信息


#### 请求


**请求参数**:


| 参数名称             | 参数说明 | 必输项描述 | 数据类型   | 备注 |
| -------------------- | -------- | ---------- | ---------- | ---- |
| &emsp;&emsp;password | 密码     | Y          | string(32) |      |


**请求示例**:


```javascript
{
	"password": "123456q"
}
```


#### 响应


**响应状态**:


| 业务码                      | 说明         | 备注 |
| --------------------------- | ------------ | ---- |
| General.Success             | 接口调用成功 |      |
| General.Failure             | 接口调用失败 |      |
| General.InternalServerError | 服务器异常   |      |
| General.RpcServerError      | Rpc服务异常  |      |
| General.GiteaServerError    | Gitea服务异常|      |
| General.ParameterInvalid    | 参数校验失败 |      |


**响应业务码-General.Success**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.Success",
	"data": {},
	"msg": "接口调用成功"
}
```


**响应业务码-General.ParameterInvalid**:


**响应参数**:


| 参数名称 | 参数说明 | 类型   | 备注 |
| -------- | -------- | ------ | ---- |
| code     | 业务代码 | string |      |
| data     | 承载数据 | object |      |
| msg      | 返回消息 | string |      |


**响应示例**:


```javascript
{
	"code": "General.ParameterInvalid",
	"data": {},
	"msg": "参数校验失败"
}
```


## 更换手机


**接口地址**:`/api/user/editUserMobile`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**: 更换当前用户绑定的手机


#### 请求


**请求参数**:


| 参数名称 | 参数说明 | 必输项描述 | 数据类型 | 备注 |
| -------- | -------- |-------- | -------- | ------ |
|&emsp;&emsp;mobile|手机号||Y|string||
|&emsp;&emsp;oriMobile|原手机号||N|string||
|&emsp;&emsp;smsCode|验证码||Y|string||
|&emsp;&emsp;password|密码||Y|string||


**请求示例**:


```javascript
{
	"mobile": "1565XXXXXXX",
	"oriMobile": "1589XXXXXXX",
	"smsCode": "xjyq",
	"password": "*****"
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
|General.MobileHasBeenUsed|手机已被使用||
|Account.VerifyError|账户检验错误||


**响应业务码-General.Success**:


**响应参数**:


| 参数名称 | 参数说明 | 类型 | 备注 |
| -------- | -------- | ----- |----- |
|code|业务代码|string||
|data|承载数据|object||
|msg|返回消息|string||


**响应示例**:
```javascript
{
	"code": "General.Success",
	"data": {},
	"msg": "接口调用成功"
}
```


**响应业务码-General.ParameterInvalid**:


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
        "ruleViolated": {
            "mobile": [
                "notBlank"
            ]
        }
    },
    "msg": "request params[mobile] notBlank."
}
```


## 获取手机验证码


**接口地址**:`/api/user/generateSmsCode`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**:发送验证码到用户指定的手机


#### 请求


**请求参数**:


| 参数名称 | 参数说明 | 必输项描述 | 数据类型 | 备注 |
| -------- | -------- |-------- | -------- | ------ |
|&emsp;&emsp;internationalCode|国际电话区号|Y|string(16)||
|&emsp;&emsp;mobile|手机号|Y|string(16)||


**数据字典**:


| 参数名称 | 参数值 | 描述 | 默认值 | 分类代码 |
| -------- | -------- | -------- | -------- | -------- |
|&emsp;&emsp;internationalCode|86|中国||sys.internationalcode|


**请求示例**:


```javascript
{
	"internationalCode": "86",
	"mobile": "1565XXXXXXX"
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
|General.ParameterInvalid|参数校验失败||
|Account.OverGlobalSmsSendLimits|超过全局短信发送限制||


**响应业务码-General.Success**:


**响应参数**:


| 参数名称 | 参数说明 | 类型 | 备注 |
| -------- | -------- | ----- |----- |
|code|业务代码|string||
|data|承载数据|object||
|msg|返回消息|string||


**响应示例**:
```javascript
{
	"code": "General.Success",
	"data": {},
	"msg": "接口调用成功"
}
```


**响应业务码-General.ParameterInvalid**:


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
        "ruleViolated": {
            "internationalCode": [
                "notContainsDict"
            ]
        }
    },
    "msg": "[internationalcode] dict error."
}
```

# INFINITE平台 软件需求


**简介**:INFINITE平台 软件需求


**HOST**:localhost:8081


**联系人**:宋飞


**Version**:1.0.0


**接口路径**:/v2/api-docs?group=存储管理


[TOC]






# 存储管理

## 存储空间详情


**接口地址**:`/api/storage/storageInfo`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**:查询用户指定仓库下的存储空间信息


#### 请求


**请求参数**:


| 参数名称 | 参数说明 | 必输项描述 | 数据类型 | 备注 |
| -------- | -------- |-------- | -------- | ------ |
|&emsp;&emsp;repoId|仓库id|Y|long||

**请求示例**:


```javascript
{
	"repoId": "1"
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


**响应业务码-General.Success**:


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- |
|code|业务代码|string||
|data|承载数据|||
|&emsp;&emsp;fileCount|文件数量|integer(11)|
|&emsp;&emsp;maxResultSize|训练结果最大空间大小|integer(11)|单位mb|
|&emsp;&emsp;usedResultSize|训练结果已使用空间大小|integer(11)|单位mb|
|&emsp;&emsp;maxDataSize|训练数据最大空间大小|integer(11)|单位mb|
|&emsp;&emsp;usedDataSize|训练数据已使用空间大小|integer(11)|单位mb|
|msg|返回消息|string||


**响应示例**:
```javascript
{
	"code": "General.Success",
	"data": {
		"fileCount": 0,
		"maxResultSize": 10,
		"usedResultSize": 1,
		"maxDataSize": 10,
        "usedDataSize": 1
	},
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
            "repoId": [
                "notNull"
            ]
        }
    },
    "msg": "request params[repoId] notNull."
}
```

## 用户存储容量


**接口地址**:`/api/storage/getUserStorageSize`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**:查询用户指定仓库下存储空间的最大的存储容量和已使用的容量


#### 请求


**请求参数**:


| 参数名称 | 参数说明 | 必输项描述 | 数据类型 | 备注 |
| -------- | -------- |-------- | -------- | ------ |
|&emsp;&emsp;repoId|仓库id|Y|long||

**请求示例**:

```javascript
{
	"repoId": "1"
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


**响应业务码-General.Success**:


**响应参数**:

| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- |
|code|业务代码|string||
|data|承载数据|||
|&emsp;&emsp;maxCapacity|最大容量|long|单位mb|
|&emsp;&emsp;usedCapacity|使用容量|long|单位mb|
|msg|返回消息|string||


**响应示例**:
```javascript
{
	"code": "General.Success",
	"data": {
		"maxCapacity": 100,
		"usedCapacity": 90
	},
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
            "repoId": [
                "notNull"
            ]
        }
    },
    "msg": "request params[repoId] notNull."
}
```



## 文件查询列表


**接口地址**:`/api/storage/fileItemList`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**:查询用户指定仓库的训练数据 训练结果文件列表


#### 请求

| 参数名称   | 参数说明      | 必输项描述 | 数据类型       | 备注 |
| ---------- | ------------- | ---------- | -------------- | ---- |
| path|当前路径|N|string|默认根目录|
| repoId|仓库id|Y|long||
| storageType|存储类型|Y|string(255)||

**数据字典**:

| 参数名称 | 参数值 | 描述 | 默认值 | 分类代码 |
| -------- | -------- | -------- | -------- | -------- |
|&emsp;&emsp;storageType|storageType.storageData|训练数据||sys.db.userStorage|
|&emsp;&emsp;|storageType.storageResult|训练结果|||


```javascript
{
    "path": "/opt/data",
    "repoId": "1",
    "storageType": "storageType.storageData"
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
|Account.VerifyError|没有权限||


**响应业务码-General.Success**:


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- |
|code|业务代码|string||
|data|承载数据|||
|&emsp;&emsp;fileItemList|结果集|array|
|&emsp;&emsp;&emsp;&emsp;name|文件名|string||
|&emsp;&emsp;&emsp;&emsp;path|文件路径|string||
|&emsp;&emsp;&emsp;&emsp;fileStatus|动态信息:创建、更新|string|数据字典|
|&emsp;&emsp;&emsp;&emsp;type|文件类型<br>文件<br> 文件夹|string|数据字典|
|&emsp;&emsp;&emsp;&emsp;updateTime|更新时间|string(date-time)||
|msg|返回消息|string||


**数据字典**:

| 参数名称 | 参数值 | 描述 | 默认值 | 分类代码 |
| -------- | -------- | -------- | -------- | -------- |
|&emsp;&emsp;fileStatus|fileStatus.create|创建||sys.db.file|
|&emsp;&emsp;|fileStatus.update|更新|||
|&emsp;&emsp;fileType|fileType.file|文件||sys.db.file|
|&emsp;&emsp;|fileType.folder|文件夹|||


**响应示例**:
```javascript
{
	"code": "General.Success",
	"data": {
		"fileItemList": [
			{
				"name": "trainData.csv",
				"path": "/opt/data",
				"fileType": "fileType.file",
				"fileStatus":"fileStatus.create",
				"updateTime": "2020-4-30"
			}
		]
	},
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
            "path": [
                "notBlank"
            ]
        }
    },
    "msg": "request params[path] notBlank."
}
```



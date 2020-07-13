# INFINITE平台 软件需求


**简介**:INFINITE平台 软件需求


**HOST**:localhost:8081


**联系人**:张鹏


**Version**:1.0.0


**接口路径**:/v2/api-docs?group=资源管理


[TOC]






# 资源管理

# 资源管理


## 资源列表


**接口地址**:`/api/userPack/getUserPackList`

**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**: 获取用户资源列表数据信息,分页展示列表,接收资源状态和资源类型作筛选条件,当设置isFreeStatus为true时是可查询与用户可用资源列表


#### 请求


**请求参数**:

**数据字典**:


| 参数名称         | 参数值                                | 描述                        | 默认值 | 分类代码 |
| ---------------- | ------------------------------------- | --------------------------- | ------ | -------- |
| userPackStatus   | &emsp;&emsp;status.free       | 用户资源状态-空闲           |        |          |
| &emsp;&emsp;     | &emsp;&emsp;status.training   | 用户资源状态-运行中是才是从v 大瓦房店发的发的发大的东方东方东方的说法是的发送到大丰富单是大幅度发啥放豆腐沙发大的 |        |          |
| 大 |  | 东方 | | |
| &emsp;&emsp;     | &emsp;&emsp;status.outOfTime  | 用户资源状态-时间用尽       |        |          |
| packDurationType | &emsp;&emsp;type.timing   | 用户资源时长类型-时间计算   |        |          |
| &emsp;&emsp;     | &emsp;&emsp;type.activity | 用户资源时长类型-活动期无限 |        |          |





**请求示例**:


```javascript
{
	"order": [
		{
			"key": "packName",
			"sort": "asc"
		}
	],
	"isFreeStatus": false,
	"userPackStatus": "userPackStatus.free",
	"packDurationType": "packDurationType.timing",
	"pageNum": 1,
	"pageSize": 10
}
```


#### 响应


**响应状态**:


| 业务码                      | 说明            | 备注 |
| --------------------------- | --------------- | ---- |
| General.Success             | 接口调用成功    |      |
| General.Failure             | 接口调用失败    |      |
| General.InternalServerError | 服务器异常      |      |
| General.RpcServerError      | Rpc服务异常     |      |
| General.TokenExpired        | 账户Token已超时 |      |
| General.TokenInvalid        | 账户Token无效   |      |
| General.Unauthorized        | 请求未授权      |      |
| General.ParameterInvalid    | 参数校验失败    |      |


**响应业务码-General.Success**:

**响应参数**:


| 参数名称                                                     | 参数说明   | 类型              | 备注             |
| ------------------------------------------------------------ | ---------- | ----------------- | ---------------- |
| &emsp;&emsp;code                                             | 业务代码   | string            |                  |
| &emsp;&emsp;data                                             | 承载数据   | PackListResponse  | PackListResponse |
| &emsp;&emsp;&emsp;&emsp;userPackList                         | 资源包列表 | array             |                  |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;userPackId               | 用户资源id | long              |                  |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;packName                 | 资源包名   | string(255)       |                  |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;userPackStatus           | 资源状态   | string(255)       |                  |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;packDurationType         | 资源类型   | string(255)       |                  |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;duration                 | 剩余时长   | long              | 单位秒           |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;buyDatetime              | 购买时间   | string(date-time) |                  |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;nodeList                 | 节点列表   | array             |                  |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;cpuCount | cpu数量    | integer(11)       |                  |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;gpuCount | gpu数量    | integer(11)       |                  |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;memorySize | 内存大小   | long              |                  |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;nodeId | 节点id     | long              |                  |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;nodeName | 节点名称   | string(255)       |                  |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;nodeType | 节点类型   | string(20)        |                  |
| &emsp;&emsp;&emsp;&emsp;pageCurrent                          | 当前页     | integer(11)       |                  |
| &emsp;&emsp;&emsp;&emsp;pageSize                             | 每页的数量 | integer(11)       |                  |
| &emsp;&emsp;&emsp;&emsp;pageTotal                            | 总页数     | integer(11)       |                  |
| &emsp;&emsp;&emsp;&emsp;total                                | 总记录数   | long              |                  |
| &emsp;&emsp;msg                                              | 返回消息   | string            |                  |

**数据字典**:


| 参数名称     | 参数值                          | 描述                   | 默认值 | 分类代码 |
| ------------ | ------------------------------- | ---------------------- | ------ | -------- |
| packNodeType | &emsp;&emsp;nodeType.master | 资源节点类型master节点 |        |          |
| &emsp;&emsp; | &emsp;&emsp;nodeType.worker | 资源节点类型worker节点 |        |          |

**响应示例**:

```javascript
{ 
	"code": "General.Success",
	"data": {
        "total": "1",
        "pageCurrent": 1,
        "pageSize": 10,
        "pageTotal": 1,
        "userPackList": [
            {
                "packName": "1",
                "userPackId": "1",
                "duration": "0",
                "packDurationType": "type.activity",
                "userPackStatus": "status.free",
                "buyDatetime": "2020-05-08 14:15:38",
                "nodeList": [
                    {
                        "cpuCount": 1,
                        "gpuCount": 2,
                        "memorySize": 10,
                        "nodeId": 123,
                        "nodeName": "节点名称",
                        "nodeType": "packNodeType.master"
                    }
                ],
            }
        ]
	},
	"msg": "接口调用成功"
}
```




## 获取资源详情


**接口地址**:`/api/userPack/getUserPackDetail`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**:


#### 请求


**请求参数**:


| 参数名称               | 参数说明 | 必输项描述 | 数据类型 | 备注 |
| ---------------------- | -------- | ---------- | -------- | ---- |
| &emsp;&emsp;userPackId | 资源id   | Y          | long     |      |

**请求示例**:


```javascript
{
	"userPackId": 234
}
```


#### 响应


**响应状态**:


| 业务码                      | 说明            | 备注 |
| --------------------------- | --------------- | ---- |
| General.Success             | 接口调用成功    |      |
| General.Failure             | 接口调用失败    |      |
| General.InternalServerError | 服务器异常      |      |
| General.RpcServerError      | Rpc服务异常     |      |
| General.TokenExpired        | 账户Token已超时 |      |
| General.TokenInvalid        | 账户Token无效   |      |
| General.Unauthorized        | 请求未授权      |      |
| General.ParameterInvalid    | 参数校验失败    |      |
| General.NotFound            | NotFound        |      |

**响应业务码-General.Success**:


**响应参数**:


| 参数名称                                       | 参数说明 | 类型               | 备注               |
| ---------------------------------------------- | -------- | ------------------ | ------------------ |
| &emsp;&emsp;code                               | 业务代码 | string             |                    |
| &emsp;&emsp;data                               | 承载数据 | object             | PackDetailResponse |
| &emsp;&emsp;&emsp;&emsp;nodeList               | 节点列表 | array              | NodeDetailRequest  |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;cpuCount   | CPU数量  | integer(11)        |                    |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;gpuCount   | GPU数量  | integer(11)        |                    |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;memorySize | 内存大小 | long               |                    |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;nodeId     | 节点id   | long               |                    |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;nodeName   | 节点名称 | string(255)        |                    |
| &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;nodeType   | 节点类型 | string(20)         |                    |
| &emsp;&emsp;&emsp;&emsp;userPackId             | 资源id   | long               |                    |
| &emsp;&emsp;&emsp;&emsp;packName               | 资源包名 | string(255)        |                    |
| &emsp;&emsp;&emsp;&emsp;userPackStatus         | 资源状态 | string(255)        |                    |
| &emsp;&emsp;&emsp;&emsp;packDurationType       | 资源类型 | string(255)        |                    |
| &emsp;&emsp;&emsp;&emsp;purchasingTime         | 购买时间 | string(date-time)  |                    |
| &emsp;&emsp;&emsp;&emsp;duration               | 剩余时长 | long               |                    |
| &emsp;&emsp;msg                                | 返回消息 | &emsp;&emsp;string |                    |

**数据字典**:


| 参数名称     | 参数值                          | 描述                   | 默认值 | 分类代码 |
| ------------ | ------------------------------- | ---------------------- | ------ | -------- |
| packNodeType | &emsp;&emsp;nodeType.master | 资源节点类型master节点 |        |          |
| &emsp;&emsp; | &emsp;&emsp;nodeType.worker | 资源节点类型worker节点 |        |          |

**响应示例**:

```javascript
{
	"code": "General.Success",
	"data": {
		"nodeList": [
			{
				"cpuCount": 1,
				"gpuCount": 2,
				"memorySize": 10,
				"nodeId": 123,
				"nodeName": "节点名称",
				"nodeType": "packNodeType.master"
			}
		],
		"userPackStatus": "status.free",
        "packDurationType": "type.timing",
		"userPackId": 076,
		"packName": "测试资源",
		"buyDatetime": "2020-05-05 16:23:00",
		"duration": 180
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
    "data": {
        "ruleViolated": {
            "userPackId": [
                "notNull"
            ]
        }
    },
    "msg": "request params[userPackId] notNull."
}
```




## 资源使用记录列表


**接口地址**:`/api/pack/getTrainPackLogList`

**请求方式**:`POST`

**请求数据类型**:`application/json`

**响应数据类型**:`application/json`


**接口描述**: 获取用户资源使用记录


#### 请求

| 参数名称   | 参数说明      | 必输项描述 | 数据类型       | 备注 |
| ---------- | ------------- | ---------- | -------------- | ---- |
| order      | 排序集        | Y          | array          |      |
| &emsp;key  | 排序key       | Y          | string         |      |
| &emsp;sort | 排序,asc,desc | Y          | string         |      |
| pageNum    | 页码          | Y          | integer(int32) |      |
| pageSize   | 每页显示数量  | Y          | integer(int32) |      |


**请求示例**:


```javascript
{
	"order": [
		{
			"key": "",
			"sort": ""
		}
	],
	"pageNum": 1,
	"pageSize": 10
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


| 参数名称   | 参数说明      | 数据类型       | 备注 |
| ---------- | ------------- | -------------- | ---- |
|code|业务代码|String|
|data|承载数据|object |
|&emsp;&emsp;list|结果集|object|
|&emsp;&emsp;&emsp;&emsp;usageRecordId|使用记录id|string||
|&emsp;&emsp;&emsp;&emsp;packId|资源id|string||
|&emsp;&emsp;&emsp;&emsp;trainName|训练名称|string||
|&emsp;&emsp;&emsp;&emsp;trainId|训练id|string||
|&emsp;&emsp;&emsp;&emsp;userName|用户名称|string||
|&emsp;&emsp;&emsp;&emsp;duration|总训练时长|string||
|&emsp;&emsp;&emsp;&emsp;createTime|资源开始使用时间|string||
|&emsp;&emsp;&emsp;&emsp;endTime|资源结束使用时间|string||
|&emsp;&emsp;pageCurrent|当前页|int|
|&emsp;&emsp;pageSize|每页的数量||int|
|&emsp;&emsp;pageTotal|总页数||int|
|&emsp;&emsp;total|总记录数||long|
|msg|返回消息||string|


**响应示例**:
```javascript
{
	"code": "General.Success",
	"data": {
		"list": [
			{
			    "logId": "3113523513121653132",
			    "packId": "6841534864138",
				"trainId": "训练id",
				"trainName": "训练名称",
				"duration": "1天5时30分15秒",
				"userName": "张三",
				"createTime": "2020-04-28 12:12:12",
				"finishTime": "2020-04-28 12:12:36",
			}
		],
		"pageCurrent": 0,
		"pageSize": 0,
		"pageTotal": 0,
		"total": 0
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
    "code": "General.TokenInvalid",
    "data": {},
    "msg": "账户Token无效"
}
```





## 训练资源使用记录详情


**接口地址**:`/api/pack/getTrainPackLogDetail`


**请求方式**:`POST`


**请求数据类型**:`application/json`


**响应数据类型**:`application/json`


**接口描述**:


#### 请求


**请求参数**:


| 参数名称 | 参数说明 | 必输项描述 | 数据类型 | 备注 |
| -------- | -------- |-------- | -------- | ------ |
|&emsp;&emsp;logId|训练资源日志id|Y|long||


**请求示例**:


```javascript
{
	"logId": 135646135
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


| 参数名称 | 参数说明 | 类型 | 备注 |
| -------- | -------- | ----- |----- |
|code|业务代码| string||
|data|承载数据| object||
|&emsp;trainId|训练id|Long||
|&emsp;trainName|训练名字|string||
|&emsp;pack|资源包|object||
|&emsp;&emsp;packId|资源id|long||
|&emsp;&emsp;packName|资源名|string(255)||
|&emsp;&emsp;residueDuration|剩余时长|long||
|&emsp;&emsp;nodeList|节点列表|object||
|&emsp;&emsp;&emsp;nodeType|节点类型|string(20)||
|&emsp;&emsp;&emsp;nodeCount|节点数量|long||
|&emsp;&emsp;&emsp;cpuCount|cpu数量|long||
|&emsp;&emsp;&emsp;gpuCount|gpu数量|gpu||
|&emsp;&emsp;&emsp;memorySize|内存大小|long||
|&emsp;userId|使用人Id|Long||
|&emsp;userName|使用人名称|string(255)||
|&emsp;duration|时长|long||
|&emsp;startTime|开始时间|string（date-time）||
|&emsp;endTime|结束时间|string（end-time）||
|msg|返回消息|string||


**响应示例**:
```javascript
{
	"code": "General.Success",
	    "data": {
				"trainId": 5488464634,
				"trainName": "训练名称",
				"pack":{
				    "packId": 123,
				    "packName": "南栖",
				    "residueDuration": "1天5时20分55秒",
				    "nodeList": [
				            {
                				"nodeId": 674654354,
                				"nodeType": "master节点",
                			    "nodeCount":1,
                			    "cpuCount": 4,
                				"gpuCount": 1,
                				"memorySize": 8
                			}
                	]
				},
				"userId":6748564,
				"userName":"张三",
				"duration": 124124,
				"startTime": "2020-04-28 12:12:12",
				"endTime": "2020-04-28 12:12:36"
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
            "logId": [
                "notBlank"
            ]
        }
    },
    "msg": "request params[logId] notBlank."
}
```




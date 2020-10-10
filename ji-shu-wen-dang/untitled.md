---
description: 方舟5.0版本中新增API
---

# 数据接入管理



## 1. 获取用户属性方案列表

获取系统预置、用户自定义、代码埋点的用户属性列表，包含计划内和计划外，未回数和已回数的所有用户属性。

### 1.1 接口地址

> 【GET】 /uba/api/schema/userProperties

### 1.2 请求参数示例

```text
?plan=1&dataStatus=1
```

> **认证参数**：接口必传token和appKey两个参数，详情见 [项目接口认证]()。

#### **1.2.1 入参说明**

| 参数名称 | 类型 | 必填 | 说明 | 枚举 |
| :--- | :--- | :--- | :--- | :--- |
| plan | Integer | N | 计划状态：1为计划内 0为计划外 | 0/1 |
| datasStatus | Integer | N | 是否回数：1为已回数 0为未回数 | 0/1 |

### 1.3 返回结果示例

```java
[
    {
        //用户属性ID，唯一
        "id":"xwho",
        //用户属性名称，用于页面展示
        "name":"用户ID",
        //是否可用 1为启用 0为禁用 （通过方舟系统可以控制用户属性的可用性）
        "enable":1,
        //是否可见 1为可见 0为不可见（用于方舟系统，系统预置但不用于分析的属性在页面上被隐藏了）
        "visible":1,
        //是否预置属性 1为预置属性 0为自定义属性
        "preset": 1,
        //数据类型，有string、boolean、number、datetime、array<string>五种
        "dataType": "string",
        //计划状态：1为计划内 0为计划外
        "plan": 1,
        //是否回数：1为已回数 0为未回数
        "dataStatus": 1,
        //是否有字典 1为有字典 0为未上传字典
        "dict": 0
    }
]
```

### 1.4 接口调用示例

```text
curl -H "token:4113c9cad1c301113783f433e254888c" -H "appKey:31abd9593e9983ec" http://127.0.0.1:4005/ark/uba/api/schema/userProperties?plan=1&dataStatus=1
```

## 2. 获取事件方案列表

获取系统预置、用户自定义、代码埋点的事件列表，包含计划内和计划外，未回数和已回数的所有事件。

### 2.1 接口地址

> 【GET】 /uba/api/schema/event

### 2.2 请求参数示例‌

```text
?plan=1&dataStatus=1
```

> **认证参数**：接口必传token和appKey两个参数，详情见 [项目接口认证]()。

#### **2.2.1 入参说明**

| 参数名称 | 类型 | 必填 | 说明 | 枚举 |
| :--- | :--- | :--- | :--- | :--- |
| plan | Integer | N | 计划状态：1为计划内 0为计划外 | 0/1 |
| datasStatus | Integer | N | 是否回数：1为已回数 0为未回数 | 0/1 |

### 2.3 返回结果示例

```java
[
    {
        // 事件ID，唯一
        "id": "$startup",
        // 事件名称，用于页面展示
        "name": "启动",
        // 计划状态：1为计划内 0为计划外
        "plan": 1,
        // 是否回数：1为已回数 0为未回数
        "dataStatus": 1,
        // 是否预置事件 1为预置事件 0为自定义事件
        "preset": 1,
        // 是否可用 1为启用 0为禁用 （通过方舟系统可以控制事件的可用性）
        "enable": 1,
        // 备注
        "remark": "APP启动 / 打开网站"
    },
    {
        "id": "login",
        "name": "登录",
        "plan": 1,
        "dataStatus": 1,
        "preset": 0,
        "enable": 1,
        "remark": "用户登录"
    }
]
```

### 2.4 接口调用示例

```http
curl -H "token:4113c9cad1c301113783f433e254888c" -H "appKey:31abd9593e9983ec" http://127.0.0.1:4005/ark/uba/api/schema/event?plan=1&dataStatus=1
```

## 3. 获取事件属性

获取事件的属性列表，包含**事件自定义属性**和**通用属性**两种，自定义属性需要自己埋点上报，通用属性由方舟系统自动采集。

包含计划内和计划外，未回数和已回数的所有事件属性。

### 3.1 接口地址

> 【GET】 /uba/api/schema/eventProperties

### 3.2 请求参数示例

```text
//【必填】通过urlPath传参
eventId=?&plan=1&dataStatus=1
```

> **认证参数**：接口必传token和appKey两个参数，详情见 [项目接口认证]()。

#### **3.2.1 入参说明**

| 参数名称 | 类型 | 必填 | 说明 | 枚举 |
| :--- | :--- | :--- | :--- | :--- |
| eventId | String | Y | 事件ID |  |
| plan | Integer | N | 计划状态：1为计划内 0为计划外 | 0/1 |
| datasStatus | Integer | N | 是否回数：1为已回数 0为未回数 | 0/1 |

### 3.3 返回结果示例

```java
[
    {
        //事件属性ID
        "id":"$is_first_time",
        //事件属性名称，用于页面展示
        "name":null,
        //备注
        "remark":null,
        //是否可用 1为启用 0为禁用 （通过方舟系统可以控制事件属性的可用性）
        "enable":1,
        //是否通用属性，1为通用属性 0为事件定义属性
        "global":0,
        //是否事件预置属性 1为预置属性 0为自定义属性
        "preset": 1,
        //数据类型，有string、boolean、number、datetime、array<string>五种
        "dataType": "boolean",
        //计划状态：1为计划内 0为计划外
        "plan": 1,
        //是否回数：1为已回数 0为未回数
        "dataStatus": 1,
        //是否有字典 1为有字典 0为未上传字典
        "dict": 0
    }
]
```

> **global**： 0为事件自定义属性，1为通用属性，每个事件都默认有的属性称为通用属性。

### 3.4 接口调用示例

```text
curl -H "token:4113c9cad1c301113783f433e254888c" -H "appKey:31abd9593e9983ec" http://127.0.0.1:4005/uba/api/schema/eventProperties?eventId=%24startup&plan=1&dataStatus=1
```


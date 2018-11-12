
# AA公司BC平台接口文档 v3.2.0

## 1 规范说明

### 1.1 通信协议

HTTPS协议

### 1.2 请求方法
POST

### 1.3 URL地址

#### 1.6.1 参数说明
**RequestData（请求内容）：** 其明文为每次请求的具体参数，采用 JSON 格式，依次经过 DES 加密（以UTF-8编码、BASE64编码输出结果）和 URLEncode 后，作为 RequestData 的值。  

**SignData（签名内容）：** 请求参数（明文）的MD5加密字符串，用于校验RequestData是否合法。

#### 1.6.2 请求内容（RequestData）明文结构说明

采用JSON格式，其中包含Header（公有参数）、Body（私有参数）节点：

名称		|描述											|备注
:--		|:--											|:--
公共参数	|每个接口都包含的通用参数，以JSON格式存放在Header属性	|详见以下公共参数说明
私有参数	|每个接口特有的参数，以JSON格式存放在Body属性		|详见每个接口定义

**公共参数说明：**

公共参数（Header）是用于标识产品及接口鉴权的参数，每次请求均需要携带这些参数：

参数名称				|类型		|出现要求	|描述  
:----				|:---		|:------	|:---	
Token				|string		|R			|用户登录后token，没有登录则为空字符串
Version				|string		|R			|接口版本号
SystemId			|int		|R			|机构号，请求的系统Id
Timestamp			|long		|R			|当前UNIX时间戳

#### 1.6.5 请求报文示例
请求内容明文：

```
{
    "Header":{
        "Token":"2366CF921FAD44CCBB07FF9CD02FC90E",
        "Version":"3.2.0",
        "SystemId":100,
        "Timestamp":1502870664
    },
    "Body":{
        "Mobile":"18520322032",
        "Password":"acb000000"
    }
}

```

请求报文示例：

```
url?RequestData=UFAYIRF21XzGoaAaEU54qoDBYaFkT2KbRpWxKZuqqltApdIneF7AjlEArPLsg3%2Fo1Pu7FHFmsKZn%0A9KJb%2BGuwx0P%2F3jzv2TgwUpVtgwEdfd0vIRfqEF4jCouldaxxVBjbHvd%2F08pUoYJDNZJLvNrJ%2BsK4%0A79de92T0Cyu4hKNMUPtVI7Tp0IC%2BBw%3D%3D&SignData=0865c7d625f90d3bb5457f5d9ac3725d
```

### 1.7 响应报文结构
#### 1.7.1 结构说明
所有接口响应均采用JSON格式，如无特殊说明，每次请求的返回值中，都包含下列字段：

参数名称						|类型		|出现要求	|描述  
:----						|:---		|:------	|:---	
Code						|int		|R			|响应码，代码定义请见“附录A 响应吗说明”
Msg							|string		|R			|响应描述
Data						|object		|R			|每个接口特有的参数，详见每个接口定义


#### 1.7.2 响应报文示例

```
{
    "Code":200,
    "Msg":"调用成功",
    "Data":{
        "Channel":"A10086",
        "Type":7004
    }
}
```


## 2. 接口定义

### 2.1 密码登录
- **接口说明：** 密码登录
- **接口地址：** /account/signin

#### 2.1.1 请求参数
  
参数名称						|类型		|出现要求	|描述  
:----						|:---		|:------	|:---	
Header						|&nbsp;		|R			|请求报文头
&emsp;Token					|string		|R			|用户登录后token，没有登录则为空字符串
&emsp;Version				|string		|R			|接口版本号
&emsp;SystemId				|int		|R			|机构号，请求的系统Id
&emsp;Timestamp				|long		|R			|当前UNIX时间戳
Body						|&nbsp;		|R			|&nbsp;
&emsp;Mobile				|string		|R			|手机号
&emsp;Password				|string		|R			|密码


请求示例：

```
{
    "Header":{
        "Token":"",
        "Version":"3.2.0",
        "SystemId":100,
        "Timestamp":1502870664
    },
    "Body":{
        "Mobile":"18520322032",
        "Password":"acb000000"
    }
}

```


#### 2.1.2 返回结果

参数名称						|类型		|出现要求	|描述  
:----						|:---		|:------	|:---	
Code						|int		|R			|响应码，代码定义请见“附录A 响应吗说明”
Msg							|string		|R			|&nbsp;
Data						|object		|R			|&nbsp;
&emsp;UserId				|string		|R			|用户Id

示例：

```
{
    "Code":200,
    "Msg":"登录成功",
    "Data":{
        "UserId":"7D916C7283434955A235C17DD9B71C64"
    }
}
```



### 2.2 获取登录用户信息
- **接口说明：** 获取登录用户信息
- **接口地址：** /account/profile

#### 2.2.1 请求参数
  
参数名称						|类型		|出现要求	|描述  
:----						|:---		|:------	|:---	
Header						|&nbsp;		|R			|请求报文头
&emsp;Token					|string		|R			|用户登录后token，没有登录则为空字符串
&emsp;Version				|string		|R			|接口版本号
&emsp;SystemId				|int		|R			|机构号，请求的系统Id
&emsp;Timestamp				|long		|R			|当前UNIX时间戳
Body						|&nbsp;		|R			|&nbsp;



请求示例：

```

{
    "Header":{
        "Token":"CA64A439E7C344B0BA7F5C825E17C7AB",
        "Version":"3.2.0",
        "SystemId":100,
        "Timestamp":1502870664
    },
    "Body":null
}

```


#### 2.2.2 返回结果

参数名称						|类型		|出现要求	|描述  
:----						|:---		|:------	|:---	
Code						|int		|R			|响应码，代码定义请见“附录A 响应吗说明”
Msg							|string		|R			|&nbsp;
Data						|object		|R			|&nbsp;
&emsp;UserId				|string		|R			|用户Id
&emsp;RealName				|string		|R			|姓名
&emsp;ImageUrl				|string		|R			|头像
&emsp;Score					|int		|R			|积分
&emsp;Nickname				|string		|R			|昵称
&emsp;Sex					|int		|R			|性别：0-未知、1-男、2-女
&emsp;Title					|string		|R			|头衔


示例：

```
{
    "Code":200,
    "Msg":"处理成功",
    "Data":{
        "UserId":"7D916C7283434955A235C17DD9B71C64",
        "RealName":"张三",
        "ImageUrl":"https://img.xx.net/afdicew8751.png",
        "Score":4732,
        "Nickname":"张冠李戴",
        "Sex":1,
        "Title":"侠客Lv4"
    }
}
```


## 3 附录A 响应码说明

响应码	|说明  
:----	|:---
200		|处理成功
301		|解析报文错误
302		|无效调用凭证
303		|参数不正确
500		|系统内部错误
999		|处理失败

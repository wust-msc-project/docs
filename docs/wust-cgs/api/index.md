# 开发接口文档

**mention: 所有请求请使用 POST 方法， GET 方法服务器不会响应。请求体和响应体均为 json ，其他格式服务器不会通过。**

**除了注册和登录，其他时间的 HTTP Head 里在 Authentication 字段里发送 Token 到服务器中**

**每个接口，都要做一下鉴权！**

## 基础接口

### 发送手机验证码

`wust.tech/api/phone-code`

请求体：

```json
{
    "phone":"13012341234",
}
```

响应体：

```json
{
    "code":0,
    "msg":"OK",
}
```

### 发送邮箱验证码

`wust.tech/api/email-code`

请求体：

```json
{
    "email":"abc@qq.com",
}
```

响应体：

```json
{
    "code":0,
    "msg":"ok",
}
```



## 用户账户系列

### 创建新用户 ✓

`wust.tech/api/create-user`

请求体：

```json
{
	"nickname":"Kininaru", // unique
	"password":"ILoveXieboQian",//长度6-16之间的字符串，只能包含数字，大小写字母，且必须包含这三种的两种
	"phone":"13012341233",//unique
	"phoneCode":"123123",//手机验证码
}
```

响应体：

```json
{
    "code":0,
    "msg":"OK",
    "data":"This is the token to me",//send a token to client.I suggest the token exp time is 1d.
}
```

出错时，`msg` 和 `data` 均为空，可能出现的 `code` 如下：

```
400: Invalid request body
421: User Already Exists
422: Phone number too long
423: Invalid password
```

### 登录

`wust.tech/api/login`

请求体：

```json
{
    "phone":"13012341234",
    "password":"ILoveXieBoQian",
}
```

响应体：

```json
{
    "code":0,
    "msg":"ok",
    "token":"this is a token",
    "isBanned":0,
}
```

如果被封禁，`isBanned=1`；未实名认证，`isBanned=2`；账户正常，`isBanned=0`

### 实名认证

`wust.tech/api/real-name-auth`

请求体：

```json
{
    "username":"张三",
    "phone":"13012341234",
    "phoneCode":"123123",
    "company":"WUST 计卓20"
}
```

响应体：

```json
{
    "code":0,
    "msg":"ok",
    "isBanned":0,
}
```

### 验证邮箱

`wust.tech/api/email`

```json
{
    "email":"abc@qq.com",
    "emailCode":"123123",
}
```

```json
{
    "code":0,
    "msg":"ok",
}
```

### 修改密码

`wust.tech/api/change-password`

```json
{
    "oldPwd":"xxx",
    "newPwd":"xxx",
    "newPwdRepeat":"xxx",
}
```

```json
{
    "code":0,
    "msg":"ok",
}
```

### 找回密码（手机）

`wust.tech/api/find-account-by-phone`

```json
{
    "phone":"13012341234",
    "phoneCode":"123123",
    "newPwd":"xxx",
    "newPwdRepeat":"xxx",
}
```

```json
{
    "code":0,
    "msg":"ok",
}
```

### 找回密码（邮箱）

`wust.tech/api/find-account-by-email`

```json
{
    "email":"abc@qq.com",
    "emailCode":"123123",
    "newPwd":"xxx",
    "newPwdRepeat":"xxx",
}
```

```json
{
    "code":0,
    "msg":"ok",
}
```

### 查看个人资料

`wust.tech/api/get-user-info`

```json
{
}
```

```json
{
    "code":0,
    "msg":"ok",
    "details":{
        "username":"张三",
        "nickname":"qwq",
        "phone":"13012341234",
        "email":"abc@qq.com",
        "company":"WUST 计卓20",
    }
}
```

### 修改个人资料

`wust.tech/api/edit-user-info`

```json
{
    "details":{
        "username":"张三",
        "nickname":"qwq",
        "phone":"13012341234",
        "email":"abc@qq.com",
        "company":"WUST 计卓20",
    }
}
```

```json
{
    "code":0,
    "msg":"ok",
}
```

### 编辑用户权限（管理员）

`wust.tech/api/edit-user-permissions`

```json
{
    "phone":"13012341234",
    "permissions":["users.ban",]
}
```

这里的权限，需要我们设计一下都有什么。目前我的设计方案是：用户系统的权限为`users.permissions`.解释一下：`users`代表用户系统，`permissions`代表具体权限。比如`users.ban`代表可以封禁别人，`users.unban`代表可以解封别人。**我们把管理员所有的权限，解构成具体的一个一个小权限，到时候比较好做。**权限表我们另附一套。

```json
{
    "code":0
}
```

### 封禁用户（管理员）

`wust.tech/api/ban-user`

```json
{
    "phone":"13012341234"
}
```

```json
{
    "code":0,
    "msg":"ok"
}
```

### 查询某人是否被封禁（管理员）

`wust.tech/api/user-is-banned`

```json
{
    "phone":"13012341234"
}
```

```json
{
    "code":0,
    "msg":"ok",
    "isBanned":0
}
```

### 解封账户（管理员）

`wust.tech/api/unban-user`

```json
{
    "phone":"13012341234"
}
```

```json
{
    "code":0,
    "msg":"ok"
}
```

### 通过手机号查询账户（管理员）

`wust.tech/api/get-user-by-phone`

```json
{
    "phone":"13012341234"
}
```

```json
{
    "code":0,
    "msg":"ok",
    "details":{
        "username":"张三",
        "nickname":"qwq",
        "phone":"13012341234",
        "email":"abc@qq.com",
        "company":"WUST 计卓20",
    }
}
```

### 通过姓名查找账户（管理员）

`wust.tech/api/get-user-by-name`

```json
{
    "username":"张三"
}
```

```json
{
    "code":0,
    "msg":"ok",
    "details":{
        "username":"张三",
        "nickname":"qwq",
        "phone":"13012341234",
        "email":"abc@qq.com",
        "company":"WUST 计卓20",
    }
}
```

### 查询某个人参加过的活动（管理员）

`wust.tech/api/get-

### 添加权限组（管理员）



### 删除权限组（管理员）



### 对某个权限组添加某个权限（管理员）



### 对某个权限组删除某个权限（管理员）



### 把某个用户移动到某个权限组中（管理员）



## 活动系列

### 查询个人参加过的活动



### 报名活动



### 拉取活动列表



### 查询活动的部分信息



### 查询活动信息（管理员）



### 添加活动（管理员）



### 编辑活动（管理员）



## 证书系列

### 新建证书&初始化（管理员）

`wust.tech/api/create-certification`

```json
{
    "certName":"XBQ",
    "picture":"我没想好这个上传什么，xbq你处理下",
    "details":{
        "name":{
            "xPer":50%,
            "yPer":50%,
            "fontSize":13,
            "fontType":"Consolas"
        },
        "QRCode":{
            "xPer":50%,
            "yPer"
        }
    }
}
```

```json
{
    "code":0,
    "msg":"ok",
    "certId":1
}
```

### 编辑证书（管理员）

`wust.tech/api/edit-certification`

```json
{
    "certId":1,
    
}
```



### 下载证书（这个过程应该有鉴权和生成两步！）

`wust.tech/api/download-certification`

```json
{
    "phone":12312311231,
    "certId":1
}
```

```json
{
    "code":0,
    "msg":"ok",
    "link":"https://the.path.of.the.certification"
}
```










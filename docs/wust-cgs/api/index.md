# 开发接口文档

**mention: 所有请求请使用 POST 方法， GET 方法服务器不会响应。请求体和响应体均为 json ，其他格式服务器不会通过。**

**除了注册和登录，其他时间的 HTTP Head 里在 Authentication 字段里发送 Token 到服务器中**

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

### 创建新用户

`wust.tech/api/create-user`

请求体：

```json
{
	"nickname":"Kininaru",
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
    "token":"This is the token to me",//send a token to client.I suggest the token exp time is 1d.
}
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
    "isBanned":"0",
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



### 修改个人资料



### 编辑用户权限（管理员）



### 封禁用户（管理员）



### 通过手机号查询账户（管理员）



### 通过姓名查找账户（管理员）



### 查询某个人参加过的活动（管理员）



## 活动系列

### 查询个人参加过的活动



### 报名活动



### 拉取活动列表



### 查询活动的部分信息



### 查询活动信息（管理员）



### 添加活动（管理员）



### 编辑活动（管理员）



## 证书系列

### 新建证书模板（管理员）



### 上传已有的证书模板（管理员）



### 编辑证书（管理员）






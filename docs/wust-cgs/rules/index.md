# 状态码约定

**注意：基于 HTTP Code 约定，客户端统一用 POST 请求，服务端在网络正常的时候统一发送 HTTP 200，在封装好的 json 中写我们下面约定的状态码**

前面为 code ， 后边为说明。

**强制要求 HTTPS 传输。**

## 非失败状态码

### 成功

0  OK

### 信息性状态码

100 Continue

### 重定向状态码

**直接发送 HTTP Code ，而不是封装在 json 里**

301 Moved Permanently（301重定向）

302 Found（302重定向）

307 Temporary Redirect（307重定向）

## 失败状态码

### 客户端错误

400 Invalid Request Body

401 Unauthorized（不要用**403 Forbidden 状态码**返回未鉴权！）

403 Forbidden（拒绝了就是拒绝了，但是我们要细分一下）

404 Not Found

418 I'm a teapot

421 User Already Exists

422 Phone number too long

423 Invalid password

### 服务端错误

500 Internal Server Error

501 Not Implemented（如果不是 POST 请求，服务器会发501响应）

503 Service Unavailable


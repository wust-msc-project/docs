# 权限表

使用方法：在后端**硬编码**权限，然后在用户的 DBA 中存一下每个人的权限。同时，新建一个权限组的表，这个表里应当有权限组 id ，权限组名称，权限组内所包含的权限，权限组是哪个权限组的**父级**。权限组 ID 应当暴露给前端。同时，权限组的名字和中文名（ name Nickname ）不应该重复。

某个人的权限应当为：**这个人所在的权限组的权限+这个人单独有的权限**，重复了就筛掉，只保留一个。

默认权限组：

 `default` 学生权限组：`user.register` , `users.login` , `users.realNameAuth` , `users.email` , `users.phone` , `users.getInfo` , `users.editInfo` ,

`admin` 管理权限组： `default.permissions` , `users.getUsersInfo` , `users.editUsersInfo` , `users.ban` , `users.unban` , `users.inBanned` , `users.getAccount` , `users.getActivities` , 

`root` 超级管理权限组：`admin.permissions` , `users.editPermissions` , `users.addPermissionGroup` , `users.delPermissionGroup` , `users.editPermissionGroup` , `users.moveUserIntoGroup` , 

## 用户系统

`users.register` 注册

`users.login` 登录

`users.realNameAuth` 实名认证

`users.email` 用邮箱找回密码

`users.phone` 用手机找回密码

`users.changePwd` 修改密码

`users.getInfo` 获取自己的个人信息

`users.getUsersInfo` 获取某个人的用户信息

`users.editInfo` 编辑自己的个人信息

`users.editUsersInfo` 编辑某个人的用户信息

`users.editPermissions` 编辑某个人的权限

`users.ban` 封禁某个人

`users.isBanned` 查询某个人是否被封禁

`users.unban` 取消封禁某个人

`users.getAccount` 查找某个人账户

`users.getActivities` 查询某个人的活动

`users.addPermissionGroup` 添加一个权限组

`users.delPermissionGroup` 删除一个权限组

`users.editPermissionGroup` 修改权限组的内容和权限

`users.moveUserIntoGroup` 把某个人移动到某个权限组中


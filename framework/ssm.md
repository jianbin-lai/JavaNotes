##### 跨域

   浏览器从一个域名的网页去请求另一个域名的资源时，域名、端口、协议任一不同，都是跨域。在前后端分离的模式下，前后端的域名是不一致的，此时就会发生跨域访问问题。在请求的过程中我们要想回去数据一般都是post/get请求，所以..跨域问题出现。

##### 使用redis好处

​     redis服务器独立jvm，jvm崩了还是能顺利读取数据

RBAC权限系统（Role-Based Access Control：基于角色的访问控制）

一个系统，除了登陆也就是认证之外，还应该有一个重要的功能，就是鉴权。

1. 认证-规定了谁能够登陆
2. 鉴权-规定了谁能访问那些接口，浏览那些页面，使用哪些功能

在RBAC模型里面，有3个基础组成部分，分别是：**用户、角色和权限。**

- User（用户）：每个用户都有唯一的UID识别，并被授予不同的角色
- **Role（角色）**：不同角色具有不同的权限，比如：人事、会计等
- **Permission（权限**）：访问权限
- 用户-角色映射：用户和角色之间的映射关系
- 角色-权限映射：角色和权限之间的映射

##### 依赖冲突

- 项目同一依赖应用，存在多版本，每个版本同一个类，可能存在差异
- 项目不同依赖应用，存在包名，类名完全一样的类。

依赖机制：直接依赖和间接依赖








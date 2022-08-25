# login接口说明

## is_logged_in

### 接口地址

127.0.0.1:5000/login/is_logged_in/

### Method

`GET`  

### 接口说明

`is_logged_in`用于判断当前登录状态，通过`session`中是否含有`'username'`项进行判断，若是则返回对应的`username`及代码`200`，若否返回错误代码`401`。

## login

### 接口地址

127.0.0.1:5000/login/

### Method

`POST`

### 接口说明

`login`用于登录。  

&ensp;&ensp;&ensp;&ensp;请求体中的数据需以`json`格式进行传输，若用户名密码验证成功，则返回`'success'`及代码`200`；若验证失败，则返回`'failed'`及代码`401`。

## logout

### 接口地址

127.0.0.1:5000/login/logout/

### Method

`GET`

### 接口说明

访问该接口将登出当前用户。返回`'success'`及代码`200`。

## register

### 接口地址

127.0.0.1:5000/login/register/

### Method

`POST`，`DELETE`

### 接口说明

该接口用于注册/注销。 请求体中的数据需以`json`的格式传输。

&ensp;&ensp;&ensp;&ensp;当使用`POST`方法访问该端口时，该端口的作用是注册新用户。若用户名已被注册，则返回`'duplicate username'`及代码`400`；若因其他服务器内部原因注册失败，则返回`'failed to register'`及代码`500`；若注册成功，则返回`'success'`及代码`201`。

&ensp;&ensp;&ensp;&ensp;当使用`DELETE`方法访问该端口时，该端口的作用是注销用户。若用户名密码验证失败，则返回`'password wrong'`及代码`401`；若因其他服务器内部原因注销失败，则返回`'failed to deregister'`及代码`500`；若注销成功，则返回`'success'`及代码`200`。

### 1.设计规格

#### 1.1. API网关使用HTTPS协议

* 总是使用TLS（就是https）来访问API  
* 对所有非TLS的请求返回403 Forbidden  


#### 1.2. API Key的发放

* 使用 JSON Web Tokens
* [Go的JWT实现](https://github.com/dgrijalva/jwt-go)
* [JWT-Go的使用指南](http://blog.brainattica.com/restful-json-api-jwt-go/)

#### 1.3. 

* 用户登出删除Token
* Token到期的自动刷新

#### 参考. 网关设计案例

[Netflix Hystrix](https://github.com/Netflix/Hystrix)
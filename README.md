## CSL中超官方移动互联网产品系统设计书

### -------- 请仔细阅读如下文档! ----------

### 1. 通用规则 

#### 1.1. API网关请求地址：

* 正式服务: http://api-csl.9h-sports.com/v1/
* 测试服务: http://123.59.84.71/v1/

#### 1.2. API请求的默认参数:  

* page-num(默认值1，可重载)
* page-row(默认值20，可重载) 

注: [子服务系统]使用Header扩展来使用分页信息，客户端依然使用page-num,page-row。

请求：Header扩展
* X-Page-Num   页数
* X-Page-Row   每页行数 

返回: Header扩展
* X-Total-Page    总共页数
* X-Total-Row     总共记录数
* X-Page-Row      每页记录数
* X-Page-Num      当前页数
* X-Page-Hasnext  是否有下一页

#### 1.3. API网关返回结果的JSON约定包含:

```
{
	oper_code: "0/1",  0:非正常流程，客户端需要做异常处理,1:正常流程。
	message  : "..." 用于非正常流程下，服务器端的提示信息。
	err_code : "01030561" 用于对旧的oper_code表达力不足的扩展，err_code将会有一套完整的系统编码，覆盖所有非正常流程。
}

```

注: [子服务系统]使用Header扩展来使用err_code,API网关负责转换该信息至body体
* X-Err-Code  具体的错误信息码

#### 1.3.1. err_code完整编码表


#### 1.4. 子服务返回结果的约定如下 [ 该约定是提供给API网关消费]:

>RESTful HTTP服务端程序必须根据HTTP规范返回状态码。状态码的第一个数字标识返回类型，1xx表示临时响应，2xx表示成功响应 ，3xx代表转发，4xx表示客户端错误，5xx代表服务端错误。

正确码的使用：
* 200: 当GET请求成功完成，DELETE或者PATCH请求同步完成。
* 201: 创建数据成功，同步方式成功完成POST请求。
* 202: POST，DELETE或者PATCH请求提交成功，稍后将异步的进行处理。
* 204: 无内容，资源有空表示。
* 206: GET请求成功完成，但只返回了部分数据。(目前可不实现该约定)。
* 301: Moved Permanently，资源的URI已被更新(转移)
* 303: See Other,其他（如，负载均衡）
* 304：Not Modified, 资源未更改（缓存）

错误码的使用：
* 400：Bad Request: 请求格式错误，请求参数有误，不被支持。
* 401: Unauthorized: 请求失败，因为用户没有进行认证。
* 403: Forbidden: 请求失败，因为用户被认定没有访问特定资源的权限。
* 404: Not Found: 未找到该资源地址，服务器不能接受该url的请求。
* 422: Unprocessable Entity: 你的请求服务器可以理解，但是其中包含了不合法的参数。
* 429: Too Many Requests: 请求频率超配，稍后再试。
* 500: Internal Server Error: 服务器出错了，检查网站的状态，或者报告问题
* 503: Service Unavailable: 服务端当前无法处理请求

> GET 操作符的状态码定义及使用场景

1.典型用法
* 获取表示
* 变更时获取表示（缓存）

2.典型状态码
* 200（OK） - 表示已在响应中发出
* 204（无内容） - 资源有空表示
* 301（Moved Permanently） - 资源的URI已被更新
* 303（See Other） - 其他（如，负载均衡）
* 304（not modified）- 资源未更改（缓存）
* 400（bad request）- 指代坏请求（如，参数错误）
* 404（not found）- 资源不存在
* 406（not acceptable）- 服务端不支持所需表示
* 500（internal server error）- 通用错误响应
* 503（Service Unavailable）- 服务端当前无法处理请求

安全？是 幂等？是

> POST

1.典型用法
* 使用服务端管理的（自动产生）的实例号创建资源
* 创建子资源
* 部分更新资源
* 如果没有被修改，则不过更新资源（乐观锁）

2.典型状态码
* 200（OK）- 如果现有资源已被更改
* 201（created）- 如果新资源被创建
* 202（accepted）- 已接受处理请求但尚未完成（异步处理）
* 301（Moved Permanently）- 资源的URI被更新
* 303（See Other）- 其他（如，负载均衡）
* 400（bad request）- 指代坏请求
* 404 （not found）- 资源不存在
* 406 （not acceptable）- 服务端不支持所需表示
* 409 （conflict）- 通用冲突
* 412 （Precondition Failed）- 前置条件失败（如执行条件更新时的冲突）
* 415 （unsupported media type）- 接受到的表示不受支持
* 500 （internal server error）- 通用错误响应
* 503 （Service Unavailable）- 服务当前无法处理请求

> PUT 操作符的状态码定义及使用场景

1.典型用法
* 用客户端管理的实例号创建一个资源
* 通过替换的方式更新资源
* 如果未被修改，则更新资源（乐观锁）

2.典型状态码
* 200 （OK）- 如果已存在资源被更改
* 201 （created）- 如果新资源被创建
* 301 （Moved Permanently）- 资源的URI已更改
* 303 （See Other）- 其他（如，负载均衡）
* 400 （bad request）- 指代坏请求
* 404 （not found）- 资源不存在
* 406 （not acceptable）- 服务端不支持所需表示/p>
* 409 （conflict）- 通用冲突
* 412 （Precondition Failed）- 前置条件失败（如执行条件更新时的冲突）
* 415 （unsupported media type）- 接受到的表示不受支持
* 500 （internal server error）- 通用错误响应
* 503 （Service Unavailable）- 服务当前无法处理请求

安全？否 幂等？是

> DELETE 操作符的状态码定义及使用场景

1.典型用法
* 删除资源

2.典型状态码
* 200 （OK）- 资源已被删除
* 301 （Moved Permanently）- 资源的URI已更改
* 303 （See Other）- 其他，如负载均衡
* 400 （bad request）- 指代坏请求t
* 404 （not found）- 资源不存在
* 409 （conflict）- 通用冲突
* 500 （internal server error）- 通用错误响应
* 503 （Service Unavailable）- 服务端当前无法处理请求

安全？否 幂等？是

#### 1.4. 数据库表默认字段:

	created_at: 新数据创建时间
	updated_at: 数据最后一次修改时间
	is_deleted: 数据是否被软删除(1:被删，不可用, 0:可用，默认0)




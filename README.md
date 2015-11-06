## CSL中超官方移动互联网产品系统设计书


### 1. 产品概况


### 2. 系统设计要求


### 3. 系统设计概述

### 4. 通用规则 

```
1. 默认URL头部 http://api-csl.9h-sports.com/v1/
2. API请求的默认参数:  
	page-num(默认值1),page-size(默认值20) 
3. API返回结果的约定包含:
	oper_code: 0  非正常流程，客户端需要做异常处理。
	oper_code: 1  正常流程，结果为期待结果。
4. 数据库表默认字段:
	created_at: 新数据创建时间
	updated_at: 数据最后一次修改时间
```

### 5. 附录

#### Gitbook相关教程

* http://www.colobu.com/2014/10/09/gitbook-quickstart/  
* http://help.gitbook.com/format/markdown.html  

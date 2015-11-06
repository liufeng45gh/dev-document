
### 3.2.2. 新闻系统服务接口

#### 2.1. 获取新闻资源列表

|接口地址| http://news.service.9h.com/resources|
| -- | : ---|
| 请求方式 | GET |
| 请求参数 | pageNo,pageSize 可选|

#### 2.2. 删除一条新闻资源

|接口地址|http://news.service.9h.com/resources/{resource_id}|
| -- |: -- |
| 请求方式 | DELETE |
| 请求参数 | resource_id  : 新闻资源id, 必填 |

#### 2.3 新增一条新闻资源

|接口地址| http://news.service.9h.com/resources/{resource_id}|
| -- | : -- |
| 请求方式 | POST |
| 请求参数 |  resource_id  : 新闻资源id, 必填 |

#### 2.4. 修改一条新闻资源

|接口地址|http://news.service.9h.com/resources/{resource_id}|
| -- | : -- |
| 请求方式 | PUT |
| 请求参数 |  resource_id  : 新闻资源id, 必填 |

#### 2.5. 获取一条新闻资源

|接口地址|http://news.service.9h.com/resources/{resource_id}|
| -- | : -- |
| 请求方式 | GET |
| 请求参数 |  resource_id  : 新闻资源id, 必填 |

#### 2.6. 获取当前的所有频道的新闻[已上线内容，支持下拉刷新和历史加载]

| 接口地址 | http://news.service.9h.com/publish-news/onlined|
| -- | : -- |
| 请求方式 | GET |
| 请求参数 | section_type : 频道类型, 必填<br /> timestamp : 时间戳(下拉刷新和历史加载必填)<br /> method_type : 操作类型(init,refresh,history) 必填<br /> pageSize : 每页行数 , 可选|

> 可选参数
* section_type (频道类型)
* timestamp (时间戳)
* pageNo (页码)
* pageSize (每页行数)

注: 该接口将会提供给API网关调用

#### 2.7. 发布一条新闻

POST http://news.service.9h.com/publish-news

#### 2.8. 修改一条新闻

PUT  http://news.service.9h.com/publish-news/{news_id}

#### 2.9. 删除一条新闻

DELETE http://news.service.9h.com/publish-news/{news_id}

#### 2.10. 获取一条新闻

GET http://news.service.9h.com/publish-news/{news_id}

####  2.11. 获取某个俱乐部相关的新闻

| 接口地址 | http://new.service.9h.com/publish-news/club/{club_id}|
| -- | : -- |
| 请求方式 | GET |
| 请求参数 |club_id : 俱乐部, 必填|

 #### 2.12. 获取某条新闻的阅读数

|接口地址|http://new.service.9h.com/publish-news/{news_id}/read-count|
| -- | : -- |
|请求方式| GET|
|请求参数| news_id : 新闻id, 必填|

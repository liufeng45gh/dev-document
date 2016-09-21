
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
--------------------------------------------

#### 2.12. 获取某条新闻的评论列表

| 接口地址 | http://new.service.9h.com/publish-news/{newsId}/comments|
| -- | : -- |
| 请求方式 | GET |
| 请求参数 |isHot: 是否为热门评论(true或false), 选填<br />refresh: 是否为刷新(true或false)，选填<br />history: 是否为加载历史(true或false)<br />timestamp: 用于刷新和加载，不传入或传入值为null则表示初次加载<br /> commentId: 当从通知中进入评论列表是必填|
|heards|X-Page-Row，userId|

返回JSON
```
[
    {
        "refUserId":"",			-->引用用户ID
        "refIsDeleted":,		-->引用评论是否被删除
        "newsCommentId":"",     -->该评论ID
        "refCommentId":"",		-->引用评论ID
        "newsId":"", 			-->被评论新闻ID
        "userId":"",			-->该评论用户ID
        "avatar":"",			-->该评论用户头像
        "nickName":"",			-->该评论用户昵称			
        "praiseCount":"",		-->该评论点赞数
        "isPraise":,			-->是否被赞
        "refNickName":"",		-->引用用户昵称
        "refAvatar":"",			-->引用用户头像
        "refContent":"",		-->引用评论内容
        "createdAtShow":"",		-->该评论创建时间
        "timestamp":"",
        "content":""			-->该评论内容
    },
    {...},
    {...},
    {...},
    {...}
]
```
> 例：
* 热门评论 ：http://123.59.84.71/v1/news/publish-news/161/comments?isHot=true
* 全部评论 ：http://123.59.84.71/v1/news/publish-news/161/comments
* 加载更多 ：http://123.59.84.71/v1/news/publish-news/161/comments?history=true&timestamp=1474346566924
* 下拉刷新 ：http://123.59.84.71/v1/news/publish-news/161/comments?refresh=true&timestamp=1474346566924

#### 2.13. 评论某条新闻
| 接口地址 | http://new.service.9h.com/publish-news/{newsId}/comment|
| -- | : -- |
| 请求方式 | POST |

请求体
```
{
	"userId":"",
	"commentId":"",
	"content":"",
	"refUserId":"",		-->引用用户ID
	"refCommentId":"",	-->引用评论ID
}
```

#### 2.14. 赞某条新闻的某条评论
| 接口地址 | http://new.service.9h.com/publish-news/{newsId}/comments/{commentId}/praise|
| -- | : -- |
| 请求方式 | POST |

请求体
```
{
	"commentId":"",		-->被赞评论ID
	"userId":""			-->点赞用户ID
}
```
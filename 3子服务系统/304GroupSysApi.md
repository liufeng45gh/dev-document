
## 3.5.2. 数据服务接口

正式地址:   
Swagger:  
测试地址: http://123.59.84.71:8082/group/v1/  
Swagger: http://123.59.84.71:8082/group/swagger/index.html  

### 3.5.3.1. 圈子的所有服务接口清单

 方法 | 接口 | 用途 | 返回 | 是否走网关 
 :-- | :--  | :-- | :-- | :--
 GET | /sections | 获取所有的圈子版块 | [] |
     | /sections?onlined=true | 获取所有的已上线圈子版块 | [] | 是
 POST| /sections | 新增一个圈子 | {} |
 PUT | /sections/{section_id} | 修改一个圈子资料(含下线)  | {} |
 DELETE| /sections/{section_id} | 删除一个圈子| |
 GET | /sections/{section_id} | 获取某个圈子的详细资料 | section | 是
     |  |  |  |  
 GET | /sections/{section_id}/topics | 获取某个圈子的所有帖子信息(分页) | topics |
 GET | /sections/{section_id}/topics?isTop=true | 获取某个圈子的置顶帖信息 | topics | 是
 GET | /sections/{section_id}/topics?method=init | 第一次获取某个圈子的最新帖子，默认20条| topics|是
 GET | /sections/{section_id}/topics?method=refresh&timestamp={timestamp}(分页)|下拉刷新获取新帖 | topics |是
 GET | /sections/{section_id}/topics?method=history&timestamp={timestamp}(分页)|上拉加载获取旧帖 | topics |是 
 POST| /sections/{section_id}/topics | 某个圈子内发表新帖 | topic | 是
     |  |  |  |
 GET | /topics/{topic_id} | 获取某个帖子的详情 | topic |是
 PUT | /topics/{topic_id} | 修改某个帖子 | topic | 是
 DELETE|/topics/{topic_id}| 删除某个帖子 |  | 是
 GET | /topics/{topic_id}/praisies?user_id={user_id}|检查某人是否已赞某个主贴| {} | 是
 POST| /topics/{topic_id}/praisies| 赞某个帖子 |  | 是 
 DELETE|/topics/{topic_id}/praisies/{praise_id}| 取消赞某个帖子 |  | 是 
 POST|  /topics/{topic_id}/shares| 分享某个帖子 |  | 是
 POST| /topics/{topic_id}/reports | 对某个帖子进行举报| report |是
 GET | /topics/{topic_id}/replys| 获取某个帖子的回帖(分页)| replys |是    
 POST| /topics/{topic_id}/replys | 对某个帖子进行回帖| reply |是
 PUT | /topics/{topic_id}/replys/{reply_id}| 修改某个帖子| reply |是
 DELETE| /topics/{topic_id}/replys/{reply_id}| 删除某个回帖 |  | 是
  | | | | 
 GET | /topics/{topic_}/replys/{reply_id}/comments|获取某个回帖的评论(分页，默认10)| [] |是
 GET | /topics/{topic_}/replys/{reply_id}/comments?getAll=true|获取某个回帖的所有评论| [] |是
 POST| /topics/{topic_}/replys/{reply_id}/comments|对某个回帖进行评论| {} |是
  | | | | 
 GET | /topics-praisies | 获取所有获赞记录 | |
 GET | /topics-shares   | 获取所有分享记录 | |
 GET | /topics-reports  | 获取所有举报记录 | |
 GET | /replys-reports  | 获取所有回帖的举报记录| |
  | | | |
 GET | /sections/{section_id}/admins | 查询某个论坛的坛主 | [] | 
 POST| /
 
### 3.5.3.2. 各接口的样例数据及字段解释

#### 获得圈子所有的版块信息

GET http://group.service.9h.com/v1/sections

返回格式:

```
HTTP Stauts Code: 200

BODY:
[
    {
        "sectionId": "1", ->版块id
        "title": "中超联赛", -> 版块名称
        "logo": "", -> 版块的缩略图,为俱乐部队徽
        "clubId": "", -> 关联俱乐部id，中超联赛的版块不关联clubId
        "bgImage": "", ->背景图片
        "isHidden":"", ->是否显示
        "topics": 3456, -> 发帖数
        "bgImage": "", ->背景图
        "timestamp": "",->时间戳
    },
    {},
    {}
]

```

#### 获得某个圈子的版块信息

GET http://group.service.9h.com/v1/sections/{section_id}

@param sectionId @PathVariable("section_id") 板块id

返回格式:

```
{

                "sectionId": "1", ->版块id
                "title": "中超联赛", -> 版块名称
                "logo": "", -> 版块的缩略图,为俱乐部队徽
                "clubId": "", -> 关联俱乐部id，中超联赛的版块不关联clubId
                "bgImage": "", ->背景图片
                "isHidden":"", ->是否显示
                "topics": 3456, -> 发帖数
                "bgImage": "", ->背景图

}
```

#### 获得某个版块的置顶贴信息

GET http://group.service.9h.com/v1/sections/{section_id}/topcis?isTop=true

#### 获得某个版块的所有主贴列表(非置顶，含精华，含附件，获赞数，回帖数)

GET http://group.service.9h.com/v1/sections/{section_id}/topcis

@param sectionId @PathVariable("section_id") 板块id

@param method @RequestParam(value = "method",required=false,defaultValue="init") 操作方法

@param timestamp @RequestParam(value = "timestamp",required=false) Long timestamp 时间戳

@param isTop @RequestParam(value = "isTop",required=false,defaultValue="false") 是否置顶贴

@param page @RequestParam(value = "page-num",required=false,defaultValue="1") 第几页

@param count @RequestParam(value = "page-size",required=false,defaultValue="20")  每页条数


返回JSON


```
{
    "oper_code": "1",
    "data": {
                hasNext: true,
                dataList: [
                                {
                                    "topicId": "1", ->帖子id
                                    "sectionId": "->版块id
                                    "authorId": "", ->作者id
                                    "title": "", -> 帖子标题
                                    "content": "", -> 帖子内容
                                    "isBest": "", -> 精华贴
                                    "isTop": "", ->置顶贴
                                    "replys":"", ->回复条数
                                    "praisies": 3456, -> 赞
                                    "isDeleted": "", ->是否删除
                                    "timestamp": "",->时间戳
                                },
                                {},
                                {}
                            ]
            }

    
}
```

####创建主贴

POST http://group.service.9h.com/v1/sections/{section_id}/topics

@param sectionId  @PathVariable("section_id") 板块id

@param topic {authorId:1,title:"xxxxxxx",content:"xxxxxxxxxxx"}

返回json:

```
{
    "oper_code": "1",
    "data": {
                "sectionId": "1", ->版块id
                "title": "中超联赛", -> 版块名称
                "logo": "", -> 版块的缩略图,为俱乐部队徽
                "clubId": "", -> 关联俱乐部id，中超联赛的版块不关联clubId
                "bgImage": "", ->背景图片
                "isHidden":"", ->是否显示
                "topics": 3456, -> 发帖数
                "bgImage": "", ->背景图
            }
}
```



#### 获得某个主帖的回帖列表

GET http://group.service.9h.com/v1/topics/{topic_id}/replys

@param topicId @PathVariable("topic_id") 主贴id

@param method  @RequestParam(value = "method",required=false,defaultValue="init") 操作

@param timestamp @RequestParam(value = "timestamp",required=false) 时间戳

@param page @RequestParam(value = "page-num",required=false,defaultValue="1")  第几页

@param count @RequestParam(value = "page-size",required=false,defaultValue="20") 每页条数

返回json:

```
{
    "oper_code": "1",
    "data": {
                hasNext: true,
                dataList： [
                                {
                                    "replyId": "1", ->回复id
                                    "topicId": "1", ->帖子id
                                    "authorId": "", ->回复人id
                                    "content": "", -> 内容
                                    "userAtTag": "", -> @的用户 
                                    "comments": "", ->评论数
                                    "isDeleted": "", ->是否删除
                                    "timestamp": "",->时间戳
                                },
                                {},
                                {}
                            ]
            }

    
}
```


#### 跟帖某个主贴

POST http://group.service.9h.com/v1/topics/{topic_id}/replys

@param topicId  @PathVariable("topic_id") 主贴id

@param reply  {authorId:"xxxx",content:"xxxxxx",userAtTag:"xxxxxx"}

返回json:

```
{
    "oper_code": "1",
    "data": {                               
                "replyId": "1", ->回复id
                "topicId": "1", ->帖子id
                "authorId": "", ->回复人id
                "content": "", -> 内容
                "userAtTag": "", -> @的用户 
                "comments": "", ->评论数
                "isDeleted": "", ->是否删除
                "timestamp": "",->时间戳                                                            
            }    
}
```


#### 获得某个帖子的某个回帖的所有评论

GET http://group.service.9h.com/v1/topics/{topic_id}/replys/{reply_id}/comments

@param replyId @PathVariable("reply_id")  回复id

@param method  @RequestParam(value = "method",required=false,defaultValue="init") 操作

@param timestamp @RequestParam(value = "timestamp",required=false) 时间戳

@param page  @RequestParam(value = "page-num", required=false,defaultValue="1")  第几页

@param count @RequestParam(value = "page-size",required=false,defaultValue="20") 每页条数

返回json:

```
{
    "oper_code": "1",
    "data": {
                hasNext: true,
                dataList：[
                                {
                                    "commentId": "1", ->评论id
                                    "replyId": "1", ->回复id
                                    "content": "", -> 内容
                                    "userAtTag": "", -> @的用户 
                                    "authorId": "", ->评论人id
                                    "isDeleted": "", ->是否删除
                                    "timestamp": "",->时间戳
                                },
                                {},
                                {}
                            ]
            }

    
}
```

#### 评论某个回帖

POST http://group.service.9h.com/v1/topics/{topic_id}/replys/{reply_id}/comments

@param replyId @PathVariable("reply_id") 回帖id

@param comment {authorId:"xxxxx",comment:"xxxxxxx",userAtTag:"xxxxx"}

@param topicId @PathVariable("topic_id") 主帖id

返回json:


```
{
    "oper_code": "1",
    "data": 
            {
                "commentId": "1", ->评论id
                "replyId": "1", ->回复id
                "content": "", -> 内容
                "userAtTag": "", -> @的用户 
                "authorId": "", ->评论人id
                "isDeleted": "", ->是否删除
                "timestamp": "",->时间戳
            }

    
}
```


#### 赞主贴

POST http://group.service.9h.com/v1/topics/{topic_id}/praisies

@param topicId  @PathVariable(value = "topic_id") 主贴id

@param praise  {authorId:"xxxxx"}

返回json: 

```
{
    "oper_code": "1",
    "data": null  
}
```

#### 取消赞主贴

DELETE http://group.service.9h.com/v1/topics/{topic_id}/praises

@param topicId  @PathVariable(value = "topic_id") 主贴id

@param praise  {authorId:"xxxxx"}

返回json: 

```
{
    "oper_code": "1",
    "data": null  
}
```



#### 赞跟贴

POST http://group.service.9h.com/v1/topics/{topic_id}/replys/{reply_id}/praisies

@param replyId  @PathVariable(value = "reply_id") 跟帖id

@param praise  {authorId:"xxxxx"}

返回json: 

```
{
    "oper_code": "1",
    "data": null  
}
```

#### 取消赞跟贴

DELETE http://group.service.9h.com/v1/topics/{topic_id}/replys/{reply_id}/praisies

@param replyId  @PathVariable(value = "reply_id") 跟帖id

@param praise  {authorId:"xxxxx"}

返回json: 

```
{
    "oper_code": "1",
    "data": null  
}
```

#### 分享主贴

POST http://group.service.9h.com/v1/topics/{topic_id}/shares

#### 举报主贴

POST http://group.service.9h.com/v1/topics/{topic_id}/reports

@param topicId @PathVariable("topic_id") 主贴id

@param report {reportUserId:"xxxxxx",reason:"xxxxxx"}

返回json: 

```
{
    "oper_code": "1",
    "data": null  
}
```

#### 举报跟帖

POST http://group.service.9h.com/v1/topics/{topic_id}/replys/{reply_id}/reports

@param replyId @PathVariable("reply_id") 跟帖id

@param report  report {reportUserId:"xxxxxx",reason:"xxxxxx"}

返回json: 

```
{
    "oper_code": "1",
    "data": null  
}
```

---

### 3.5.3. 实现方案

* 考虑用 Redis 做存储



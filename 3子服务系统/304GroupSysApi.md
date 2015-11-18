
## 3.5.2. 数据服务接口

#### 获得圈子所有的版块信息

GET http://group.service.9h.com/v1/sections

返回格式:

```
{
    "oper_code": "1",
    "data": [
            {
                "sectionId": "1", ->版块id
                "title": "中超联赛", -> 版块名称
                "logo": "", -> 版块的缩略图,为俱乐部队徽
                "clubId": "", -> 关联俱乐部id，中超联赛的版块不关联clubId
                "bgImage": "", ->背景图片
                "isHidden":"", ->是否显示
                "topics": 3456, -> 发帖数
                "bgImage": "", ->背景图
            },
            {},
            {}
        ]
}
```

#### 获得某个圈子的版块信息

GET http://group.service.9h.com/v1/sections/{section_id}

@param sectionId @PathVariable("section_id") 板块id

返回格式:

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

#### 获得某个版块的置顶贴信息

GET http://group.service.9h.com/v1/sections/{section_id}/topcis?isTop=true

#### 获得某个版块的所有主贴列表(非置顶，含精华，含附件，获赞数，回帖数)

GET http://group.service.9h.com/sections/{section_id}/topcis

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
    "data": [
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
            },
            {},
            {}
        ]
}
```

#### 获得某个主帖的回帖列表

GET http://group.service.9h.com/topics/{topic_id}/replys

@param topicId @PathVariable("topic_id") 主贴id

@param method  @RequestParam(value = "method",required=false,defaultValue="init") 操作

@param timestamp @RequestParam(value = "timestamp",required=false) 时间戳

@param page @RequestParam(value = "page-num",required=false,defaultValue="1")  第几页

@param count @RequestParam(value = "page-size",required=false,defaultValue="20") 每页条数

返回json:

```
{
    "oper_code": "1",
    "data": [
            {
            	"replyId": "1", ->回复id
                "topicId": "1", ->帖子id
                "authorId": "", ->回复人id
                "content": "", -> 内容
                "userAtTag": "", -> @的用户 
                "comments": "", ->评论数
                "isDeleted": "", ->是否删除
            },
            {},
            {}
        ]
}
```

#### 跟帖某个主贴

POST http://group.service.9h.com/topics/{topic_id}/replys

#### 获得某个帖子的某个回帖的所有评论

GET http://group.service.9h.com/topics/{topic_id}/replys/{reply_id}/comments

@param replyId @PathVariable("reply_id")  回复id

@param method  @RequestParam(value = "method",required=false,defaultValue="init") 操作

@param timestamp @RequestParam(value = "timestamp",required=false) 时间戳

@param page  @RequestParam(value = "page-num", required=false,defaultValue="1")  第几页

@param count @RequestParam(value = "page-size",required=false,defaultValue="20") 每页条数

返回json:

```
{
    "oper_code": "1",
    "data": [
            {
            	"commentId": "1", ->评论id
                "replyId": "1", ->回复id
                "content": "", -> 内容
                "userAtTag": "", -> @的用户 
                "authorId": "", ->评论人id
                "isDeleted": "", ->是否删除
            },
            {},
            {}
        ]
}
```

#### 评论某个回帖

POST http://group.service.9h.com/topics/{topic_id}/replys/{reply_id}/comments

#### 赞主贴

POST http://group.service.9h.com/topics/{topic_id}/praisies

#### 取消赞主贴

DELETE http://group.service.9h.com/topics/{topic_id}/praises/{praise_id}

#### 分享主贴

POST http://group.service.9h.com/topics/{topic_id}/shares

#### 举报主贴

POST http://group.service.9h.com/topics/{topic_id}/reports

#### 举报跟帖

POST http://group.service.9h.com/topics/{topic_id}/replys/{reply_id}/reports


---

### 3.5.3. 实现方案

* 考虑用 Redis 做存储



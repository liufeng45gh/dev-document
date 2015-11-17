
## 3.5.2. 数据服务接口

#### 获得圈子所有的版块信息

GET http://group.service.9h.com/v1/sections

#### 获得某个圈子的版块信息

GET http://group.service.9h.com/v1/sections/{section_id}

@param sectionId @PathVariable("section_id") 板块id

#### 获得某个版块的置顶贴信息

GET http://group.service.9h.com/v1/sections/{section_id}/topcis?isTop=true

#### 获得某个版块的所有主贴列表(非置顶，含精华，含附件，获赞数，回帖数)

GET http://group.service.9h.com/sections/{section_id}/topcis

@param sectionId @PathVariable("section_id") 板块id

@param isTop @RequestParam(value = "isTop",required=false,defaultValue="false") 是否置顶贴

@param page @RequestParam(value = "page-num",required=false,defaultValue="1") 第几页

@param count @RequestParam(value = "page-size",required=false,defaultValue="20")  每页条数

#### 获得某个主帖的回帖列表

GET http://group.service.9h.com/topics/{topic_id}/replys

@param topicId @PathVariable("topic_id") 主贴id

@param page @RequestParam(value = "page-num",required=false,defaultValue="1")  第几页

@param count @RequestParam(value = "page-size",required=false,defaultValue="20") 每页条数

#### 跟帖某个主贴

POST http://group.service.9h.com/topics/{topic_id}/replys

#### 获得某个帖子的某个回帖的所有评论

GET http://group.service.9h.com/topics/{topic_id}/replys/{reply_id}/comments

@param replyId @PathVariable("reply_id")  回复id

@param page  @RequestParam(value = "page-num", required=false,defaultValue="1")  第几页

@param count @RequestParam(value = "page-size",required=false,defaultValue="20") 每页条数

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



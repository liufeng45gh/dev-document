## 3.11.2. 随手拍服务接口

正式地址:   
Swagger:  
测试地址: 
Swagger: http://123.59.84.71:8091/photo/swagger/index.html   


### 3.11.2.1. 随手拍的所有服务接口清单

 方法 | 接口 | 用途 | 返回 | 是否走网关 
 :-- | :--  | :-- | :-- | :--
 GET | /tabs | 获取所有的随手拍菜单 | [] |
     |  |  |  |  
 GET | /subjects?tab_id={}&is_new={}&display={}&method={}&timestamp={} | 条件查询主题(分页) | subjects |
 GET | /subjects?tab_id={}&is_new=1&display=1 | 获取某个菜单的最新主题信息 | subjects | 是
 GET | /subjects?tab_id={}?method=init | 第一次获取某个菜单的最新主题信息，默认20条| subjects|是
 GET | /subjects?tab_id={}?method=refresh&timestamp={timestamp}(分页)|下拉刷新获取新主题 | subjects |是
 GET | /subjects?tab_id={}?method==history&timestamp={timestamp}(分页)|上拉加载获取旧主题 | subjects |是 
 POST| /subjects | 发表新主题 | {} | 是
 PUT| /subjects/{id} | 修改主题 | {} | 是
 DELETE| /subjects/{id} | 删除主题 | {} | 是
     |  |  |  |
 GET | /photo-group/list?subject_id={}&author_id={}&method={}&timestamp={} | 条件查询图片组 | [] |是
 POST | /photo-group | 新建图片组 | {} | 是
 PUT | /photo-group/{id} | 修改图片组 | {} | 是
 DELETE|/photo-group/{id}| 删除图片组 |  | 是
     |  |  |  |
 GET | /photos/{photo_id}/praises?user_id={user_id}|检查某人是否已赞图片组| {} | 是
 GET | /photos/{photo_id}/praises-v2?user_id={user_id}|检查某人是否已赞图片组| {} | 是
 POST| /photos/{photo_id}/praises| 赞图片 |  | 是 
 DELETE|/photos/{photo_id}/praises/{id}| 取消赞图片组 |  | 是 
 POST|  /photos/{photo_id}/shares| 分享某个图片组 |  | 是
  	 | | | | 
 GET | /photos/{photo_id}/comments|获取某个图片的评论(分页，默认10)| [] |是
 GET | /photos/{photo_id}/comments?getAll=true|获取某个图片的所有评论| [] |是
 POST| /photos/{photo_id}/comments|对某个图片进行评论| {} |是
  	 | | | | 
 GET | /photos-praisies | 获取所有获赞记录 | |
 GET | /photos-shares   | 获取所有分享记录 | |
 GET | /photos-reports  | 获取所有举报记录 | |
	 | | | |

 
### 3.5.3.2. 各接口的样例数据及字段解释

#### 获得圈子所有的版块信息

GET http://123.59.84.71:8091/photo/v1/tabs

返回格式:

```
HTTP Stauts Code: 200

BODY:
[
  {
    "id": 1, ->菜单id
    "name": "随手拍", ->菜单显示名称
    "index": 1  ->索引 顺序
  },
  .....
]

```

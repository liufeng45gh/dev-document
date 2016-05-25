## 3.11.2. 随手拍服务接口

正式地址:   
Swagger:  
测试地址: 
Swagger: http://123.59.84.71:8091/photo/swagger/index.html   


### 3.11.2.1. 随手拍的所有服务接口清单

 方法 | 接口 | 用途 | 返回 | 是否走网关 
 :-- | :--  | :-- | :-- | :--
 GET | {tabName}/subjects | 条件查询主题(分页) | subjects |
 POST| {tabName}/subjects | 发表新主题 | {} | 是
 PUT| /subjects/{id} | 修改主题 | {} | 是
 DELETE| /subjects/{id} | 删除主题 | {} | 是
     |  |  |  |
 GET | /subjects/{subject_id}/photo-groups | 条件查询图片组 | [] |是
 POST | /subjects/{subject_id}/photo-groups | 新建图片组 | {} | 是
 PUT | /photo-group/{id} | 修改图片组 | {} | 是
 DELETE|/photo-group/{id}| 删除图片组 |  | 是
     |  |  |  |
 GET | /photo-groups/{photo-group_id}/praises?user_id={user_id}|检查某人是否已赞图片组| {} | 是
 GET | /photo-groups/{photo-group_id}/praises/praises-v2?user_id={user_id}|检查某人是否已赞图片组| {} | 是
 POST| /photo-groups/{photo-group_id}/praises| 赞图片 |  | 是 
 

 
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

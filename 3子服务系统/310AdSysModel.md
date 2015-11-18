### 3.3.1. 数据模型

#### 3.3.1.1. 广告资源管理

```SQL
Table:    ad_resource

id
ad_type       广告类型(1:image 2:video 3:text )
snapshot      资源的截图(视频类用)
title         标题
local_url     资源的本地路径
cloud_url     资源的云平台路径
content       文字内容(text类型使用)
content _url  文字内容来源地址
memo          备注(1,2,3通用)
created_at    资源创建时间
updated_at    资源修改时间
```

#### 3.3.1.2. 广告发布管理

```SQL
Table:    ad_publish

id
ad_id           广告资源ID  PK -> ad_resources.id
status          状态1:上线 2:下线
setion_type     栏目类型 101:csl-赛事新闻 102:csl-官方公告 103:csl-精彩视频 104:csl-专家评球 ..
publish_type    使用类型 1: csl-首页轮播 2:csl-新闻广告 3: csl-首页跑马灯
action_enabled  是否可以有后续交互(比如点击) 1:可以0:不可以，默认0
action_data     点击该广告资源的后续交互数据(JSON格式串)
onlined_at      上线时间
offlined_at     下线时间
for_app         管理发布的App类型(101:中超App 201:国安App)  《- 待商议
display_order   权重排序,数字越大,权重越高，默认皆为1
created_at      广告发布管理创建时间
updated_at      广告发布管理更新时间
```
注: 权重排序为第一优先排序，上线时间倒序为第二优先排序，以后皆类同

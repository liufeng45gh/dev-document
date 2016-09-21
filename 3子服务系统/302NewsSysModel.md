
### 3.2.1. 数据模型

#### 3.2.1.1. 资讯资源管理

```SQL
Table news_resource

id             唯一ID
news_type      新闻资源类型(1：图文混排；2：视频类；3：纯文本)
title          标题
outline        内容概要
original_from  新闻来源
thumb_url      缩略图URL(列表显示用)
content        正文内容
content_url    正文链接
created_at     创建时间
updated_at     修改时间
```

#### 3.2.1.2. 资讯发布管理

```SQL
Table news_publish

id
news_id        对应新闻ID, FK -> news_resource.id
status         状态1:上线 2:下线
section_type   栏目类型 101:csl-赛事新闻 102:csl-官方公告 103:csl-精彩视频 104:csl-专家评球 ...
onlined_at     上线时间
offlined_at    下线时间
display_order  权重排序,数字越大,权重越高，默认皆为1
read_count     阅读数
for_app        管理发布的App类型(101:中超App 201:国安App)  《- 待商议
ann_type       官方公告类使用(1:官方公告,2:处罚决定,3:通知)默认为1
is_top         新闻是否置顶(1: 置顶，0 : 未置顶; 默认为 : 0 )
relative_tag   相关跳转标签(俱乐部,球员,比赛,联赛...)
created_at     创建时间
updated_at     更新时间
```

注: 
> 关联标签设计格式 A方案 JSON格式
```JavaScript
[
	{
		"tagType":  "Club",
		"tagValue": "ClubID",
		"tagName":  "国安俱乐部"
	},
	{
		"tagType":  "Player",
		"tagValue": "PlayerID",
		"tagName":  "徐云龙"
	},
	{
		"tagType":  "League",
		"tagValue": "leaugeId",
		"tagName":  "中超联赛"
	}
]
```

#### 3.2.1.3 资讯评论
```SQL
Table news_comment		

id 						唯一主键
news_publish_id 		新闻Id（关联news_publish表 ID）
user_id 				用户ID
content					评论内容
praise_count			点赞数
ref_user_id				被回复用户ID
ref_comment_id			被回复评论ID
timestamp				保存点赞时间（bigint）
created_at
updated_at								
is_deleted				是否删除（用于软删除）
delete_reason			删除原因
```

#### 3.2.1.4  用户与评论的点赞关系
```SQL
Table news_comment_praise

id 						唯一主键
comment_id 				新闻评论ID（关联news_comment表 ID）
user_id 				用户ID
timestamp				保存点赞时间（bigint）
created_at
updated_at
is_deleted				是否删除（用于软删除）
```


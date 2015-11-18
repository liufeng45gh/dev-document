
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




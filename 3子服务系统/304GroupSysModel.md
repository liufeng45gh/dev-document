### 3.5.1 数据模型
```dsds

#### 圈子的版块基础信息表

```SQL
Table forum_section

id
title      版块的标题
logo       主题的logo
topics     发帖总数
club_id    关联的俱乐部ID
bg_image   版块的背景图
is_hidden  是否需要隐藏(这里做软删除，1:隐藏,0:显示，默认皆为0)
```
注: 中超联赛的球队每年有变化，这样降级的球队版块将会隐藏。

#### 圈子的主帖信息

```SQL
Table forum_topic

id
section_id  对应的版块ID FK->forum_section.id
author_id   对应的发帖人 FK->user.id
title       主贴标题
content     主贴内容
is_best     是否精华帖
is_top      是否置顶贴
posted_at   发表时间
updated_at  修改时间
replys      获得的回帖数
praisies    获得的赞数
is_deleted  是否被删除(这里做软删除，1:被删,0:存在，默认皆为0)
```

#### 圈子的主贴对应的附件图片信息

```SQL
Table forum_topic_file

id
topic_id   所属帖子的id
author_id  发帖人的id
type       附件类型(image[图片],video[视频],vocie[语音],)
title      附件标题
file_url   附件的路径(url)
thumb_url  附件的缩略图路径
upload_at  附件上传的时间
is_deleted 是否被删除(这里做软删除，1:被删,0:存在，默认皆为0)
```
#### 圈子的帖子对应的跟帖信息

```SQL
Table forum_topic_reply

id
topic_id   所属帖子的id
author_id  跟帖人的id
content    跟贴内容
posted_at  发表时间
updated_at 修改时间
user_at_tag 评论中@的用户 (user_id:user_name 以,做分隔符的字符串)
comments   获得的评论回复数
is_deleted 是否被删除(这里做软删除，1:被删,0:存在，默认皆为0)
```


#### 圈子的帖子对应的跟帖的附件图片信息

```SQL
Table forum_reply_file

id
topic_id   所属主帖的id
reply_id   所属跟帖的id
author_id  回复人的id
type       附件类型(image[图片],video[视频],vocie[语音],)
title      附件标题
file_url   附件的路径(url)
thumb_url  附件的缩略图路径
upload_at  附件上传的时间
is_deleted 是否被删除(这里做软删除，1:被删,0:存在，默认皆为0)
```
### 圈子的主贴对应的跟帖的评论信息

```SQL
Table forum_reply_comment

id
topic_id    评论对应的主贴id
reply_id    评论对应的跟帖id
author_id   评论人id
comment     评论文字信息(表情+文字+@信息)
comment_at  评论时间
user_at_tag 评论中@的用户 (user_id:user_name 以,做分隔符的字符串)
is_deleted  是否被删除(这里做软删除，1:被删,0:存在，默认皆为0)
```

### 圈子的主帖的被赞记录

```SQL
Table forum_topic_praise

id
topic_id   对应的帖子ID FK-> forum_topic.id
priser_id  对应点赞人   FK-> user.id
prise_at   点赞时间(用于点赞排序)
```

### 圈子的主帖的分享记录

```SQL
Table forum_topic_share

id
topic_id   被分享的主帖ID
share_user 分享人 FK->user.id
share_on   分享的渠道(1:weibo 2:qq 3:weixin 4:)
share_at   分享时间
```

### 圈子的主贴的举报记录

```SQL
Table forum_topic_report

id
topic_id    被举报的主帖id FK-> forum_topic.id
report_user 举报人  FK->user.id
reason      举报理由
report_at   举报时间(用于对举报帖子做规则限制)
```
注1: 每个账号每小时对相同帖子只可以举报1次，超出举报限制则会弹出提示信息。
注2: 每个账号对不同帖子举报时间1分钟内限制1贴。

#### 圈子的跟贴的举报记录

```SQL
Table forum_reply_report

id
reply_id    被举报的跟帖id
report_user 举报人  FK->user.id
reason      举报理由
report_at   举报时间(用于对举报帖子做规则限制)
```


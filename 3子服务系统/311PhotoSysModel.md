
### 数据模型

### 菜单 ###


```SQL
Table:    tab

id                     主键
name                   名字
index                  索引 顺序

```

### 主题 ###


```SQL
Table:    subject
id                  主键
tab_id               菜单id
title               标题
photo_count          照片数量
player_count         参与者数量
display             是否显示
is_deleted           是否删除
created_at           创建时间
updated_at           修改时间
end_at               结束时间
start_at             开始时间
is_new               是否最新
bphct               基础图片数量
bplct               基础参与者数量
```

### 图片组 ###

```SQL
Table:    photo_group
id                  主键
subject_id           主题id
thumbs              缩略图集合 用逗号分隔,目前没有使用 是冗余
urls                图片url 集合 用逗号分隔
description         描述
praise_count         赞数
created_at           创建时间
update_at            修改时间
author_id            作者id
is_deleted           是否删除
```

### 赞 ###

```SQL
Table:    praise

id                  主键
photo_id             图片组Id
user_id              用户Id
created_at           创建时间
updated_at           修改时间
is_deleted           是否删除
```





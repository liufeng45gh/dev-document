### 3.1.1. 数据模型

#### 3.1.1.1. 用户注册信息

```SQL
Table user

id        自增长(长整,以下所有id字段皆为该规则)
uuid      uuid生成规则(App侧调用)
cloud_id  云平台绑定ID(LeanCloud),允许为空
weixin_id 微信绑定ID,允许为空
weibo_id  微博绑定ID,允许为空
qq_id     QQ绑定ID,允许为空
account   账号(系统自动生成规则QQ+?  WX+?  WB+? Phone+?) 极客学院的案例:weibo_1xvrf8hs
phone     绑定手机,允许为空
mail      绑定邮箱,允许为空
password  密码,(加密后的密码,非明文),允许为空
salt      加密盐,6位随机数字字母组合,允许为空
app_tag   在不同的App上的激活标签
```
注: 除开password,salt,以上字段在有值的情况下皆为唯一值

#### 3.1.1.2. 用户详细资料

```SQL
Table user_info

id
user_id   用户唯一ID, FK-> users.id
nick_name 昵称
avatar    头像图片路径
true_name 真实姓名
sex       性别 1:男 2:女 3:保密
province  所在省份
city      所在城市
card_id   身份证号码
birth     出生年月日
level     用户等级
points    用户积分

```

#### 3.1.1.3. 用户关注俱乐部

```SQL
Table user_follow_club

id 
user_id   用户id  FK-> user.id
club_id   俱乐部id FK-> data_club.id
```

#### 3.1.1.4. 用户关注比赛

```SQL
Table user_follow_match

id
user_id   用户id FK-> user.id
match_id  比赛id FK-> data_league_match.id
```

#### 3.1.1.5. 用户关注其他用户的列表

```SQL
Table user_follow_user

id
user_id        用户id FK-> user.id
follow_user_id 该用户关注的对象id FK-> user.id
```

#### 3.1.1.6. 用户被其他用户关注的列表(与3.1.1.5组成双向关系)

```SQL
Table user_followed_by_user

id
user_id             用户id FK-> user.id
followed_by_user_id 该用户的关注人id FK-> user.id
is_blocked          该用户是否屏蔽关注人(1:屏蔽 0:不屏蔽 默认皆为0)
```
#### 3.1.1.7. 用户的签到信息

```SQL
Table user_checkin_log

id
user_id      用户ID
checked_at   签到时间
```

#### 3.1.1.8. 用户等级与积分的对照

```SQL
Table user_level_point

id
title         称号
level         等级
icon_url      等级图标(图片)
points_higher 积分上限
points_Lower  积分下限
```

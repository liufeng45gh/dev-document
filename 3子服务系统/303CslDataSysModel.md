### 3.4.1. 数据模型

#### 3.4.1.1. 球员资料

```SQL
Table data_player

id
name                 中文姓名
english_name         英文姓名
country              国籍
native_place         籍贯
birth                出生年月日
created_at           创建时间
updated_at           修改时间
```

#### 3.4.1.2. 俱乐部资料

```SQL
Table data_club

id
logo           俱乐部logo
bg_image       背景图
name           中文名称,常用,比如:广州恒大
full_name      中文全称,备用,比如:广州恒大淘宝足球俱乐部
en_name        英文名称
en_full_name   英文全称
history_name   俱乐部历史名称，json字符串保存:{"2015":"广州恒大淘宝"}
history_logo   俱乐部历年所用的logo，json字符串保存:{"2015":"https:9hgame.com"}
intro_url      俱乐部介绍资料(一个网页URL)
founded_at     俱乐部创立时间
created_at     创建时间
updated_at     修改时间
```

#### 3.4.1.3. 教练资料

```SQL
Table data_coach

id
name           中文姓名
english_name   英文姓名
country        国籍
birth          出生年月日
created_at     创建时间
updated_at     修改时间
```

#### 3.4.1.4. 球员与俱乐部关联关系

```SQL
Table data_player_re_club

id
player_id           球员ID FK->data_player.id
club_id             俱乐部ID FK->data_club.id
player_number       球衣号码
player_number_icon  球衣号码图片URL
position            队内位置，文字描述(门将/后卫/中场/前锋)
position_number     位置权重，排序用,数字大在前面 1:门将 2:后卫 3:中场 4:前锋;默认为0  
avatar              球员头像URL
weight              球员体重(如: 65 kg)
height              球员身高(如: 185 cm)
onfield             球员在本赛季代表俱乐部的出场次数
onfield_last        球员在本赛季代表俱乐部的出场时间
goals               本赛季的进球数
serial_number       参赛编号
year                效力年份(用于跟踪球员的转会历史)
league_type         1:踢正赛(比如中超)，2:踢正赛,非正赛(比如中超预备队) 3:踢非正赛
created_at          创建时间
updated_at          修改时间
```
#### 3.4.1.5. 教练与俱乐部关联关系

```SQL
Table data_coach_re_club

id
coach_id         教练ID FK -> data_coach.id
club_id          俱乐部ID FK-> data_club.id
year             效力年份
avatar           教练头像URL
created_at       创建时间
updated_at       修改时间
```

#### 3.4.1.6. 联赛资料

```SQL
Table data_league

id
name         联赛中文简称(中超，亚冠，预备队...),常用,比如:中超联赛
full_name    联赛的全文名称,作为某些情况下的备份,比如:中国足球超级联赛
en_name      英文简称,常用,比如:CSL
en_full_name 英文全称,备份,比如:Chinese Super League
type         联赛类型 1:联赛(积分制) 2:杯赛(淘汰制)
region       举办地区 (中国,亚洲...)
region_type  联赛范围 1:国家级,2:洲级,3:世界级
start_at     开始举办年份
created_at   创建时间
updated_at   修改时间
```
#### 3.4.1.7. 联赛与俱乐部关联关系

```SQL
Table data_league_re_club

id
club_id         俱乐部ID   FK-> data_club.id
league_id       联赛ID     FK-> data_league.id
year            联赛年份 (支持不带-的当年和带-的跨年两种格式 注:这里考虑到url的/冲突,避免用/做分隔符)
display_order   权重排序,数字越大,权重越高，默认皆为1
created_at      创建时间
updated_at      修改时间

注: 这就意味着每个新赛季都需要重新录入俱乐部和该联赛的参与关系
```

#### 3.4.1.8. 联/杯赛赛程

```SQL
Table data_league_match

id
kick_at         比赛时间(年月日时分)
home_score      主队比分(未开赛则为0)
guest_score     客队比分(未开赛则为0)
home_club_id    主队ID   FK -> data_club.id
guest_club_id    客队ID   FK -> data_club.id
round            比赛轮次 (用于记录联赛的情况)
knockout         比赛分组(用于记录杯赛的情况,分 pre[预选],a-z[小组],1/16,...1/8,1/4,semi-final[半决赛],final[决赛])
weekday          比赛星期(一~日)
stadium          比赛球馆
league_id        所属联赛  FK-> data_league.id
audiences        观众人数(用于计算上座率)
match_status     是否已经结束(1:结束,2:未结束,3:正在进行中,默认皆为 2)
video_url        精彩视频转播URL
broadcast        比赛转播(以Json 格式保存如：[{"castName":"乐视","castUrl":"http://leshi.com"},{"castName":"腾讯","castUrl":"http://v.qq.com/"}])
year             联赛年份 (支持不带-的当年和带-的跨年两种格式 注:这里考虑到url的/冲突,避免用/做分隔符)
created_at       创建时间
updated_at       修改时间
```

#### 3.4.1.9. 联赛转播计划

```SQL
Table data_league_match_broadcast

id
match_id      该转播计划关联的比赛ID FK-> data_league_match.id
cast_name     转播方
cast_url      转播链接
display_order 排序权重，默认为1，高的在前
created_at    创建时间
updated_at    修改时间
```
#### 3.4.1.10. 联赛积分榜

```SQL
Table data_league_rank_club

id
league_id  联赛ID
club_id    俱乐部ID
round      场次
wins       胜场
ties       平场
loses      负场
goals      进球
goals_a    失球
goals_d    净胜球
points     积分
year       联赛年份 (支持不带-的当年和带-的跨年两种格式 注:这里考虑到url的/冲突,避免用/做分隔符)
created_at 创建时间
updated_at 修改时间
```

####3.4.1.11.联赛主场积分榜

```SQL
Table data_league_rank_club_home
id
league_id  联赛ID
club_id    俱乐部ID
round      场次
wins       胜场
ties       平场
loses      负场
goals      进球
goals_a    失球
goals_d    净胜球
points     主场积分
year       联赛年份 (支持不带-的当年和带-的跨年两种格式 注:这里考虑到url的/冲突,避免用/做分隔符)
created_at 创建时间
updated_at 修改时间
```

####3.4.1.12.联赛客场积分榜

```SQL
Table data_league_rank_club_guest
id
league_id  联赛ID
club_id    俱乐部ID
round      场次
wins       胜场
ties       平场
loses      负场
goals      进球
goals_a    失球
goals_d    净胜球
points     客场积分
year       联赛年份 (支持不带-的当年和带-的跨年两种格式 注:这里考虑到url的/冲突,避免用/做分隔符)
created_at 创建时间
updated_at 修改时间
```

#### 3.4.1.13. 联赛射手榜

```SQL
Table data_league_rank_goal

id
league_id  联赛ID
player_id  球员ID
club_id    所属俱乐部ID
goals      进球数
year       联赛年份 (支持不带-的当年和带-的跨年两种格式 注:这里考虑到url的/冲突,避免用/做分隔符)
created_at 创建时间
updated_at 修改时间
```

#### 3.4.1.14. 联赛助攻榜

```SQL
Table data_league_rank_assistant

id
league_id         联赛ID
player_id         球员ID
club_id           所属俱乐部ID
assistants        助攻数
home_assistants   主场助攻数
guest_assistants  客场助攻数
year              联赛年份 (支持不带-的当年和带-的跨年两种格式 注:这里考虑到url的/冲突,避免用/做分隔符)
created_at        创建时间
updated_at        修改时间
```
#### 3.4.1.15. 联赛红黄牌榜

```SQL
Table data_league_rank_card

id
league_id      联赛ID
club_id        俱乐部ID
red_cards      红牌数
yellow_cards   黄牌数
double_y_cards 双黄牌数
year           联赛年份 (支持不带-的当年和带-的跨年两种格式 注:这里考虑到url的/冲突,避免用/做分隔符)
created_at     创建时间
updated_at     修改时间
```

#### 3.4.1.16. 联赛公平竞赛榜

```SQL
Table data_league_rank_peace

id
league_id     联赛ID
club_id       俱乐部ID
points        积分
yellow_cards  黄牌数
red_cards     红牌数
dock_of_cards 红黄牌扣分
dock_of_fouls 纪律处罚扣分
dock_of_sum   扣分合计
year          联赛年份 (支持不带-的当年和带-的跨年两种格式 注:这里考虑到url的/冲突,避免用/做分隔符)
created_at    创建时间
updated_at    修改时间
```
#### 3.4.1.17. 联赛裁判

```SQL
Table data_judge

id
name          裁判姓名
name_initials 姓名首字母缩写(用于可能需要的姓名自然排序)
nationality   国籍
region        地区(直辖市/省级的粒度)
birth         生日(用于自动计算年龄)    
level         级别(1:国家级 2:国际级)
created_at    创建时间
updated_at    修改时间
```
#### 3.4.1.18. 历史数据-中超历年积分

注:详见 3.4.1.9.联赛积分榜

#### 3.4.1.19. 历史数据-中超历年射手

注:详见 联赛射手榜

#### 3.4.1.20. 历史数据-中超历年助攻

注:详见 联赛助攻榜

#### 3.4.1.21. 历史数据-中超历年红黄牌

注:详见 联赛红黄牌榜

#### 3.4.1.22. 历史数据-中超升降级信息

```SQL
Table data_league_updown

id
league_id   联赛ID
club_id     俱乐部ID
updown_type 升降级类型(1:升级 2:降级)
year        联赛年份 (支持不带-的当年和带-的跨年两种格式 注:这里考虑到url的/冲突,避免用/做分隔符)
created_at  创建时间
updated_at  修改时间
```

#### 3.4.1.23. 历史数据-中超历年最佳

```SQL
Table data_league_outstanding

id
league_id           联赛id
league_name         联赛名称
player_id           最佳球员  FK -> data_league_player.id
player_name         球员姓名
player_re_club_name 球员所属俱乐部名称
player_re_club_logo 球员所属俱乐部logo
player_number       球员号码
judge_id            最佳裁判  FK -> data_league_judge.id 
judge_name          裁判姓名
judge_region        裁判地区(直辖市/省级的粒度)
judge_birth         裁判出生年月
fish_id             最佳新人  FK -> data_league_player.id
fish_name           新人姓名
fish_re_club_name   新人所属俱乐部名称
fish_re_club_logo   新人所属俱乐部logo
fish_number         新人球员号码
coach_id            最佳教练 (FK -> data_league_coach.id)
coach_name          教练姓名
coach_re_club_name  教练所属俱乐部名称
coach_re_club_logo  教练所属俱乐部logo
lineUp              最佳阵容(一张阵容图的URL)
year    联赛年份 (支持不带-的当年和带-的跨年两种格式 注:这里考虑到url的/冲突,避免用/做分隔符)
created_at          创建时间
updated_at          修改时间
```

#### 3.4.1.24. 历史数据-中超上座率

注:详见 联赛的比赛记录信息，根据观众人数排序生成

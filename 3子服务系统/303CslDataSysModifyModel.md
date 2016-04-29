 数据合并修改详情
---
## 1. 修改表
####  1.1 data_club（俱乐部） 表：
| 初始 | 修改后| 释义|
| --  | -- |--|
|id|id|唯一主键|
|logo||俱乐部logo|
|bg_image|bg_image|俱乐部背景图|
|bg_player_image|bg_player_image|俱乐部下球员背景图|
|name|name|俱乐部名称(冗余字段，标识作用)|
|full_name||俱乐部中文全名|
|en_name||俱乐部英文名|
|en_full_name||俱乐部英文全名|
|history_name||俱乐部历史名称|
|history_logo||俱乐部历史logo|
|intro_url|intro_url|俱乐部简介(中超使用)|
|founded_at|founded_at|俱乐部创建时间|
|created_at|created_at||
|updated_at|updated_at||
### 1.2 data_league_re_club（俱乐部联赛关系）表：
| 初始 | 修改后| 释义|
| --  | -- |--|
|id|id|唯一主键|
|club_id|club_id|俱乐部ID|
|league_id|league_id|联赛ID|
||league_name|联赛名称（冗余）|
|year|year||
||honors|荣誉（球队名次）|
|display_order|display_order|球队排序|
|created_at|created_at||
|updated_at|updated_at||
### 1.3 data_coach（教练）表：
| 初始 | 修改后| 释义|
|--|--|--|
|id|id|唯一主键|
|name|name|名字|
|english_name|english_name|英文名|
|country|country|国籍|
||native_place|籍贯（出生地）|
|birth|birth|生日|
|avatar||头像|
|created_at|||
|updated_at|||
### 1.4 data_coach_re_club（教练与俱乐部关联关系）表：
| 初始 | 修改后| 释义|
|--|--|--|
|id|id|唯一主键|
|coach_id|coach_id|教练ID|
|club_id|club_id|俱乐部ID|
||type|教练类型（参考coachtype表）|
||type_name|教练类型名称(冗余)|
||club_history_id|球队历史ID|
|avatar|avatar|头像|
||cir_avatar|半身像圆角图|
||info_avatar|带文字描述的头像|
||full_avatar|全身像|
|is_last_served|||
|served_at||效力时间|
|year|||
||end_year|结束年|
|created_at|created_at||
|updated_at|updated_at||
### 1.5 data_judge（联赛裁判）表：
| 初始 | 修改后| 释义|
|--|--|--|
|id|id|唯一主键|
|name|name|裁判姓名|
|name_initials|name_initials|姓名首字母缩写(用于可能需要的姓名自然排序)|
|nationality|nationality|国籍|
||native_place|籍贯（出生地）|
|region|region|地区(直辖市/省级的粒度)(暂时不删除，但是建议用行政区划)|
||region_code|行政区划6位编码(备用）|
|birth|birth|生日(用于自动计算年龄)|
|level|level|级别(1:国家级 2:国际级)|
|created_at|created_at||
|updated_at|updated_at||

### 1.6 data_league（联赛类型）表：
| 初始 | 修改后| 释义|
|--|--|--|
|data_league|league_type|表名|
|id|id|唯一主键|
|name|name|联赛中文简称(中超，亚冠，预备队...),常用,比如:中超联赛|
|full_name|full_name|联赛的全文名称,作为某些情况下的备份,比如:中国足球超级联赛|
|en_name|en_name|英文简称,常用,比如:CSL|
|en_full_name|en_full_name|英文全称,备份,比如:Chinese Super League|
|type|type|联赛类型 1:联赛(积分制) 2:杯赛(淘汰制)|
|region|region|举办地区 (中国,亚洲...)|
|region_type|region_type|联赛范围 1:国家级,2:洲级,3:世界级|
|start_at|start_at|开始举办年份|
|created_at|created_at||
|updated_at|updated_at||

### 1.7 data_player（球员）表：
| 初始 | 修改后| 释义|
|--|--|--|
|id|id|唯一主键|
|name|name|中文姓名|
|english_name|english_name|中文姓名|
|country|country|国籍|
|native_place|native_place|籍贯|
|birth|birth|出生年月|
|position||队内位置，文字描述(门将/后卫/中场/前锋)|
|position_number||位置权重，排序用,数字大在前面 1:门将 2:后卫 3:中场 4:前锋;默认为0|
|player_number||球衣号码|
|player_number_icon||球衣号码图片URL|
|avatar||球员头像URL|
|stature||球员身高|
|weight||球员体重|
|serial_number||球员参赛编号|
|created_at|created_at||
|updated_at|updated_at||

### 1.8 data_player_re_club（球员历史）表：
| 初始 | 修改后| 释义|
|--|--|--|
|id|id|唯一主键|
|player_id|player_id|球员ID FK->data_player.id|
|club_id|club_id|俱乐部ID FK->data_club.id|
||club_history_id|俱乐部历史ID(新增)|
|served_at||效力时间(用于跟踪球员的转会历史)|
|year|year|开始年份(改为了int)|
||end_year|结束年份(新增)|
|is_last_served|is_last_served|是否是最后效力的俱乐部(用于查询俱乐部当前所有球员的列表 ,"0"表示否,"1"表示是)|
|league_type|league_type|1:踢正赛(比如中超)，2:踢正赛,非正赛(比如中超预备队) 3:踢非正赛|
|player_number|player_number|球衣号码|
|player_number_icon|player_number_icon|球衣号码图片URL|
|position|position|队内位置，文字描述(门将/后卫/中场/前锋)|
|position_number|position_number|位置权重，排序用,数字大在前面 1:门将 2:后卫 3 中场  4:前锋;默认为0|
|avatar|avatar| 球员头像URL(半身像方框)|
||cir_avatar|半身像圆角图|
||full_avatar|全身像|
||info_avatar|带文字描述的头像|
|weight|weight|球员体重(如: 65 kg)|
|height|height|球员身高(如: 185 cm)|
|onfield|onfield|球员在本赛季代表俱乐部的出场次数|
|onfield_last|onfield_last|球员在本赛季代表俱乐部的出场时间|
|goals|goals|本赛季的进球数(默认为0)|
||shoot_times|射门次数|
||assist_times|助攻次数|
||yellow_times|黄牌次数|
||red_times|红牌次数|
|serial_number|serial_number||
|updated_at|updated_at||
|created_at|created_at||

### 1.9 data_league_match（赛程）表：
| 初始 | 修改后| 释义|
|--|--|--|
|id|id|唯一主键|
|kick_at|kick_at|比赛时间(年月日时分)|
|home_score|home_score|主队比分(未开赛则为0)|
|guest_score|guest_score|客队比分(未开赛则为0)|
|home_club_id|home_club_id|主队ID   FK -> data_club.id|
||home_club_history_id|主队历史ID|
|guest_club_id|guest_club_id|客队ID   FK -> data_club.id|
||guest_club_history_id|客队历史ID|
|round|round|比赛轮次 (用于记录联赛的情况)|
|knockout|knockout|比赛分组(用于记录杯赛的情况,分 pre[预选],a-z[小组]|
|weekday|weekday|比赛星期(一~日)|
|stadium|stadium|比赛球馆|
|league_id|league_id|所属联赛  FK-> data_league.id|
||league_sub_id|联赛子类型|
|audiences|audiences|观众人数(用于计算上座率)|
|relative_tag|relative_tag|(是否需要)相关关联标签(如转播计划,精彩视频等),参见新闻的关联标签设计|
|video_url|video_url|精彩视频转播URL|
|year|year|联赛年份|
|match_status|match_status|比赛是否结束 1:表示结束，2：表示进行中，3：表示未开始，4:比赛延期 默认皆为 3|
|broadcast||比赛转播(以Json 格式保存如：[{"castName":"乐视","castUrl":"http://leshi.com"},{"castName":"腾讯","castUrl":"http://v.qq.com/"}])|
|created_at|created_at||
|updated_at|updated_at||

### 1.10 data_league_match_broadcast（联赛转播计划）表：
| 初始 | 修改后| 释义|
|--|--|--|
|id|id|唯一主键|
|match_id|match_id|该转播计划关联的比赛ID FK-> data_league_match.id|
|cast_name|cast_name|转播方|
|cast_url|cast_url|转播链接|
||cast_logo|视频标识|
||play_times|播放次数|
|display_order|display_order|排序权重，默认为1，高的在前|
|created_at|created_at||
|updated_at|updated_at||

### 1.11 data_league_outstanding（历史数据-中超历年最佳）表：无修改

### 1.12 data_league_rank_assistant（联赛助攻榜）表：
| 初始 | 修改后| 释义|
|--|--|--|
|id|id|唯一主键|
|league_id|league_id|联赛ID|
|player_id|player_id|球员ID|
|club_id|club_id|所属俱乐部ID|
||club_history_id|俱乐部历史ID|
|assistants|assistants|助攻数|
|home_assistants|home_assistants|主场助攻数|
|guest_assistants|guest_assistants|客场助攻数|
||pre_ranking|上轮排名|
|ranking|ranking|排名|
|year|year|联赛年份|
||end_year|结束年|
|created_at|created_at||
|updated_at|updated_at||

### 1.13 data_league_rank_card（联赛红黄牌榜）表：
| 初始 | 修改后| 释义|
|--|--|--|
|id|id|唯一主键|
|league_id|league_id|联赛ID|
|club_id|club_id|俱乐部ID|
||club_history_id|俱乐部历史ID|
|red_cards|red_cards|红牌数|
|yellow_cards|yellow_cards|黄牌数|
|double_y_cards|double_y_cards|双黄牌数|
|ranking|ranking|名次，默认为0|
|year|year|开始年份|
||end_year|结束年份|
|created_at|created_at||
|updated_at|updated_at||

### 1.14 data_league_rank_club（联赛积分榜）表：
| 初始 | 修改后| 释义|
|--|--|--|
|id|id|唯一主键|
|league_id|league_id|联赛ID|
||league_sub_id|联赛子ID|
||grouping|分组（小组赛）|
|club_id|club_id|俱乐部ID|
||club_history_id|俱乐部历史ID|
|round|round|场次|
|wins|wins|胜场|
|ties|ties|平场|
|loses|loses|负场|
|goals|goals|进球|
|goals_a|goals_a|失球|
|goals_d|goals_d|净胜球|
|points|points|积分|
|year|year|联赛年份 |
||end_year|联赛结束年份|
||pre_ranking|上一轮排名|
|ranking|ranking|当前排名|
|display_order|display_order|用于积分榜的手动排序，数值越大越靠前。默认为1|
|ranking_status|ranking_status|排名状态|
|created_at|created_at||
|updated_at|updated_at||

### 1.15 data_league_rank_club_guest（联赛客场积分榜）表：
与联赛积分榜变化一样
### 1.16 data_league_rank_club_home（联赛主场积分榜）表：
与联赛积分榜变化一样

### 1.17 data_league_rank_goal（联赛射手榜）表：
| 初始 | 修改后| 释义|
|--|--|--|
|id|id|唯一主键|
|league_id|league_id|联赛ID|
|club_id|club_id|所属俱乐部ID|
|player_id|player_id|球员ID|
|goals|goals|进球数|
||pre_ranking|上一轮排名|
|ranking|ranking|当前排名|
|year|year|联赛年份|
||end_year|联赛结束年份|
|created_at|created_at||
|updated_at|updated_at||
### 1.18 data_league_rank_peace（公平竞赛榜）表：无修改
### 1.19 data_league_updown（联赛升降级）表：无修改
### 1.20 data_match_event（比赛事件）表：
| 初始 | 修改后| 释义|
|--|--|--|
|id|id|唯一主键|
|match_id|match_id|赛事ID|
|club_id|club_id|球队ID FK -> data_club.id|
|event_type|event_type|事件类型|
|event_data|event_data|赛事事件文本|
|club_type|club_type|产生此事件的球队(1:主场球队,2:客场球队)|
|event_point|event_point|事件发生时间点|
|event_at|event_at|事件发生时间|
||player_id|球员ID|
||player_secondary_id|次要球员ID|
||player_name|球员名称|
||player_secondary_name|次要球员名称|
|created_at|created_at||
|updated_at|updated_at||

### 1.21 data_match_id_mapped（比赛Id  与 amisco 数据中的比赛id 对应表）：无修改
### 1.22 data_match_line（比赛阵容）表：
| 初始 | 修改后| 释义|
|--|--|--|
|id|id|唯一主键|
|match_id|match_id|赛事ID   FK -> data_match.id|
|home_club_id|home_club_id|主队ID   FK -> data_club.id|
|guest_club_id|guest_club_id|客队ID   FK -> data_club.id|
|line_url|line_url|比赛球队阵容图URL|
||home_line_url|主队阵容图(半场)URL|
||guest_line_url|客队阵容图(半场)URL|
|home_line|home_line|主队阵型|
|guest_line|guest_line| 客队阵型|
|created_at|created_at||
|updated_at|updated_at||
|year|year|约束作用(冗余)|

### 1.23  data_match_player（比赛球员）表：取消avatar字段
### 1.24 data_match_stat（比赛统计）表：无修改
### 1.25 data_player_id_mapped（比赛球员Id  与 amisco 数据中的比赛球员id 对应表）：无修改

* * *
## 2. 新增表
### 2.1 club_history（俱乐部历史） 表：
```SQL
    id	             bigint(45) PK   唯一主键
    club_id	        bigint(20)      俱乐部ID   FK-> data_club.id
    year	           varchar(45)     联赛年份 
    logo	           varchar(255)    图片
    name	           varchar(45)     队名    
    en_name	        varchar(45)     英文名
    full_name	      varchar(45)     中文全名
    en_full_name	   varchar(100)    英文全名
    created_at	     datetime        创建时间
    updated_at	     datetime        最后修改时间
    court	          varchar(45)     主场场地
    color	          varchar(45)     俱乐部主体颜色
```
### 2.2 club_type（球队主客关系）表：
```SQL
    id          int(11) AI PK       逻辑主键
    name        varchar(32)         名称
```
### 2.3 coach_history（教练履历）表：
```SQL
    id              bigint(20) PK   履历主键
    year            int(11)         联赛开始年份
    end_year        int(11)         结束年份
    coach_id        bigint(20)      教练主键
    coach_name      varchar(255)    
    league_name     varchar(255)    联赛名称
    club_name       varchar(255)    俱乐部名称
    honors          varchar(255)    荣誉
    create_at       datetime
    update_at       datetime
```
### 2.4 coach_type（教练类型）表：
```SQL
    id      int(11) AI PK   逻辑主键
    name    varchar(32)     
```
### 2.5 data_judge_re_match（裁判与比赛的关联关系）表：
```SQL
    id              bigint(20) AI PK    唯一主键
    judge_id        bigint(20)          裁判ID
    match_id        bigint(20)          比赛ID
    judge_type_id   int(11)             裁判类型
    avatar          varchar(255)        裁判头像URL(方框半身像)
    cir_avatar      varchar(255)        半身像圆角图
    info_avatar     varchar(255)        带文字描述的头像
    full_avatar     varchar(255)        全身像
    created_at      datetime    
    updated_at      datetime
```
### 2.6 judge_type（裁判类型）表：
```SQL
    id      int(11) PK      唯一主键
    name    varchar(32)     裁判类型名称
```
### 2.7 rounds（轮次）表：
```SQL
    Id              int(11) AI PK   唯一主键
    RoundsId        int(11)         轮次号
    Name            varchar(32)     轮次名称
    LeagueTypeId    int(11)         联赛子类型
```
### 2.8 state_type（赛事状态）表：
```SQL
    id      int(11) AI PK       唯一主键
    name    varchar(32)         名称
```
### 2.9 event_type（事件类型）表：
```SQL
    id      int(11) AI PK       唯一主键
    name    varchar(32)         赛事事件名称
    icon    varchar(255)        图标
```
### 2.10 player_line_type（球员阵容类型）表：
```SQL
    id      int(11) PK      唯一主键
    name    varchar(32)     名称
```
### 2.11 updown_type（球队升降级）表：
```SQL
    id      int(11) PK      唯一主键
    name    varchar(32)     名称
```
### 2.12 match_video（赛事视频）表
```SQL
    id              bigint(20) PK   唯一主键
    club_id         bigint(20)      俱乐部ID
    match_id        bigint(20)      比赛ID
    logo            varchar(255)    视频主图
    title           varchar(255)    视频标题
    url             varchar(255)    视频链接
    public_time     datetime        发布时间
    play_times      int(10) UN      播放次数
    create_at       datetime        
    update_at       datetime
```
### 2.13 player_position_type（球员阵容类型）表：
```SQL
    id      int(11) AI PK       唯一主键
    name    varchar(32)         名称
```
### 2.14 match_position
```SQL
    name            varchar(32) PK      位置名称
    x               int(11)             x坐标
    y               int(11)             y坐标
    club_type_id    int(11)             主客关系ID
```

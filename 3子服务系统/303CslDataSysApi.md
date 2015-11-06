### 通用规则
* 分页参数：pageNo，pageSize
    * pageNo：对查询数据的页数请求，可选，默认为1
    * pageSize：对每页数据的行数请求，可选，默认为20
* 接口返回数据中的分页信息：totalItemNumber,totalPageNumber,hasNext,hasPrev,prev,pageNo,pageSize
    *  totalItemNumber：查询出来的总数
    *  totalPageNumber：根据数据页数计算出来的页数
    *  hasNext：是否有下一页
    *  hasPrev：是否有上一页
    *  prev：上一页页码
    *  pageNo：当前页码
    *  pageSize：每页请求数量
*  请求参数（以下参数接口中若有出现必填）
    *  player_id：测试值为9~261
    *  club_id：测试值为2~21
    *  judge_id：测试值为1~2
    *  coach_id：测试值为1~14
    *  league_id：测试值为：1
    *  round：测试值：1~2
    *  year：测试值：2015
注： 请求参数 league_id  可用 league_name 代替,league_name 的值为 :  csl(中超联赛), cl(中甲联赛), csl-p(中超预备队联赛), acl(亚冠联赛) 

### 3.4.2. 数据服务接口

#### 3.4.2.1  获取某位球员的详细资料

| 接口地址 |http://data.service.9h.com/players/{player_id}  |
| --  | :-- |
| 请求方式 | GET,PUT,DELETE |
|请求参数|player_id：球员的id,必填|

####  3.4.2.2  修改某位球员的详细资料

|接口地址| http://data.service.9h.com/players |
| --  | :-- |
|请求方式| POST : 保存一位球员 |
|请求方式| GET : 获取所有的球员|
|请求参数| filters (如:pageNo,pageSize),value(如:1,25) 可选|
|请求方式| DELETE : 删除多个球员|
|请求参数| ids(如:4,5,6,7)  必填|

#### 3.4.2.3  获取某个俱乐部的详细资料

| 接口地址 |http://data.service.9h.com/clubs/{club_id}  |
| --  | :-- |
| 请求方式 | GET、PUT、DELETE |
|请求参数|club_id：俱乐部的id，必填|

####  3.4.2.4  修改某个俱乐部的详细资料

| 接口地址 | http://data.service.9h.com/clubs |
| --  | :-- |
| 请求方式 | POST :保存一个俱乐部|
| 请求方式 | GET :获取所有俱乐部|
| 请求参数 | pageNo ,pageSize 可选|
| 请求方式 | DELETE : 删除多个俱乐部|
| 请求参数 | ids(如:ids=1,2,3) 必填|

#### 3.4.2.5  根据一组clubId获取多个俱乐部详细资料

|接口地址| http://data.service.9h.com/follow-clubs  |
| --  | :-- |
|请求方式 |GET : 获取多个俱乐部详情|
|请求参数 | ids(如:ids=12,13,14)  必填|
注:此接口用于用户关注俱乐部使用

####  3.4.2.6 获取某个俱乐部下属(现役)所有球员的资料

| 接口地址 |http://data.service.9h.com/clubs/{clubId}/players |
| --  | :-- |
| 请求方式 | GET : 获取球员<br />POST : 给某俱乐部添加球员|
| 请求参数|club_id：俱乐部的id,必填<br >served=true : 获取某个俱乐部下现役的所有球员<br/>served=false：获取某个俱乐部下服役过的球员(不包括在役球员)<br/>served : 不填写将返回所有的球员|

#### 3.5.2.7  修改某个俱乐部与球员的关联关系

|接口地址|http://data.service.9h.com/clubs/{clubId}/players/{playerReClubId}|
| --  | :-- |
|请求方式|PUT:更新球员与俱乐部的关联关系<br />DELETE : 删除球员与俱乐部的关联关系|
|请求参数|playerReClubId 必填|

####  3.5.2.8  获取某位教练的详细资料

| 接口地址 |http://data.service.9h.com//coachs/{coach_id} |
| --  | :-- |
| 请求方式 | GET、PUT、DELETE |
|请求参数|coach_id：教练的id，必填|

####  3.5.2.9  将一位教练的详细信息保存到数据库

|接口地址|http://data.service.9h.com/coachs |
| --  | :-- |
|请求方式 |POST : 保存一位教练|
|请求方式 |GET : 获取所有的教练|
|请求参数 |pageNo,pageSize 可选|
|请求方式 |DELETE : 删除多位教练|
|请求参数 |ids : 必填(如 : ids=12,3,2)|

####  3.5.2.10  获取某位裁判的详细资料

| 接口地址 |http://data.service.9h.com/judges/{judge_id} |
| --  | :-- |
| 请求方式 | GET、PUT、DELETE |
|请求参数|judge_id：裁判的id，必填|

#### 3.5.2.11   将一位裁判的详细信息保存到数据库

| 接口地址 |http://data.service.9h.com/judges |
| --  | :-- |
| 请求方式 |POST : 保存一位裁判|
| 请求方式 |GET :  获取所有的裁判|
| 请求参数 |pageNo，pageSize 可选|
| 请求方式 |DELETE : 删除多位裁判|
| 请求参数 |ids : 必填(如 : ids= 12,1,2)|

####   3.5.2.12  获取某个联赛/杯赛的基本信息

| 接口地址 |http://data.service.9h.com/leagues/{league_id} |
| --  | :-- |
| 请求方式 | GET、PUT、DELETE |
|请求参数|league_id：联赛的id，必填|

#### 3.5.2.13   将一个联赛/杯赛的基本信息保存到数据库

| 接口地址 |http://data.service.9h.com/leagues|
| --  | :-- |
| 请求方式 |POST : 保存一个联赛  |
| 请求方式 |GET : 获取所有联赛|
| 请求参数 |pageNo,pageSize  选填|
| 请求方式 | DELETE : 删除多个联赛|
| 请求参数 | ids(如 : ids=14,12,13) 必填|

####   3.5.2.14  获取某个联赛/杯赛在某年的所有参赛球队

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/clubs |
| --  | :-- |
| 请求方式 | GET, POST  |
|请求参数|league_id：联赛的id，必填<br >year：联赛年份，必填|

####  3.5.2.15  修改俱乐部与联赛之间的关系

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/clubs/{leaugeReClubId} |
| --  | :-- |
|请求方式 | GET, POST  |
|请求参数|league_id：联赛的id, 必填<br >year：联赛年份, 必填<br >leaugeReClubId : 联赛与俱乐部的关联Id,  必填 |

####   3.5.2.16   获取某个联赛/杯赛在某年的所有比赛情况

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/matchs|
| --  | :-- |
| 请求方式 | GET |
|请求参数|league_id：联赛的id，必填<br >year：联赛年份，必填|

####   3.5.2.17 获取全部比赛

|接口地址|http://data.service.9h.com/matchs|
| -- | : -- |
|请求方式| GET|
|请求参数|year: 联赛年份,可选<br >leagueId: 联赛Id,可选<br >round:比赛轮次，可选<br >matchStatus : 比赛状态(1:已结束,2:正在进行中,3:未开始),可选<br >pageNo,pageSize 可选|


####  3.5.2.18  给数据库中保存一场比赛信息

|接口地址|http://data.service.9h.com/leagues/matchs|
| -- | : -- |
|请求方式| POST|

####  3.5.2.19 修改数据库中一场比赛信息

|接口地址|http://data.service.9h.com/leagues/matchs/{leagueMatchId}|
| -- | : -- |
|请求方式| PUT, DELETE|
|请求参数|leagueMatchId 必填|

####  3.5.2.20  获取某个联赛/杯赛在某年在某轮的所有比赛情况

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/matchs/{round} |
| --  | :-- |
| 请求方式 | GET |
|请求参数|league_id：联赛的id，必填<br >year：联赛年份，必填<br >round：比赛轮次，必填|

####   3.5.2.21   获取某场比赛的情况

| 接口地址 |http://data.service.9h.com/matchs/{match_id}|
| --  | :-- |
| 请求方式 | GET |
|请求参数|match_id：比赛的id，必填|


####   3.5.2.22   获取某个联赛/杯赛在某年的所有比赛的转播计划

| 接口地址 | http://data.service.9h.com/leagues/{league_id}/{year}/matchs/broadcasts|
| --  | :-- |
| 请求方式 | GET |
|请求参数|league_id：联赛的id，必填<br >year：联赛年份，必填|


####  3.5.2.23   获取某个联赛/杯赛在某年在某轮的所有比赛的转播计划

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/matchs/{round}/broadcasts |
| --  | :-- |
| 请求方式 | GET |
|请求参数|league_id : 联赛的id,必填<br >year : 联赛年份,必填<br >round : 比赛轮次,必填|

####  3.5.2.24   获取某个联赛/杯赛在某年在某轮的所有比赛上座率情况

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/matchs/{round} |
| --  | :-- |
| 请求方式 | GET |
|请求参数|league_id：联赛的id，必填<br >year：联赛年份，必填<br >round：比赛轮次，必填<br >query : 上座率参数, 必须为 : query=seat-rat|

####  3.5.2.2   某个联赛在某年的球队积分榜

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/rank-club|
| --  | :-- |
| 请求方式 | GET |
|请求参数|league_id：联赛的id，必填<br >year：联赛年份，必填|

####  3.5.2.20   某个联赛在某年的射手榜

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/rank-goal |
| --  | :-- |
| 请求方式 | GET |
| 请求方式 | POST : 给射手榜添加一条信息 |
| 请求方式 | DELETE : 删除某个射手榜|
| 请求参数 |league_id：联赛的id，必填<br >year：联赛年份，必填|

#### 3.5.2.21  修改某个联赛在某年的某个射手榜

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/rank-goal/{LeagueRankGoalId}|
| --  | :-- |
| 请求参数 | LeagueRankGoalId : 射手榜 id , 必填<br >league_id：联赛的id，必填<br >year：联赛年份，必填|
| 请求方式 |GET : 获取某个射手榜上的一条信息<br >DELETE : 删除某个射手榜上的一条信息 <br >PUT : 新射手榜上的一条信息|

####  3.5.2.22   某个联赛在某年的助攻榜

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/rank-assistant|
| --  | :-- |
|请求方式 | GET , POST|
|请求参数 |league_id：联赛的id，必填|
|请求参数 |year：联赛年份，必填|
|请求方式 |DELETE : 删除某个联赛在某年的一组助攻榜信息|
|请求参数 | ids 必填(ids=1,2,3)|

####  3.5.2.23   修改某个联赛在某年的助攻榜信息

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/rank-assistant/{AssistantId}|
| --  | :-- |
| 请求方式 | GET , DELTE , PUT|
| 请求参数 |league_id：联赛的id，必填<br >year：联赛年份，必填|

####   3.5.2.24   某个联赛在某年的红黄牌榜

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/rank-card|
| --  | :-- |
| 请求方式 | GET , POST|
| 请求参数 |league_id：联赛的id，必填|
| 请求参数 |year：联赛年份，必填|
| 请求方式 |DELETE : 删除一组某个联赛在某年的红黄牌信息|
| 请求参数 |ids  必填, (ids=12,14,25)|

####   3.5.2.25   修改某个联赛在某年的红黄牌榜

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/rank-card/{rankCardId}|
| --  | :-- |
| 请求方式 | GET , POST|
| 请求参数 |league_id：联赛的id，必填<br >year：联赛年份，必填<br >rankCardId : 红黄牌榜信息id|

####  3.5.2.26  某个联赛在某年的公平竞赛榜

| 接口地址 | http://data.service.9h.com/leagues/{league_id}/{year}/rank-peace|
| --  | :-- |
| 请求方式 | GET ,POST|
| 请求参数 |league_id：联赛的id，必填<br >year：联赛年份，必填|

####  3.5.2.27  某个联赛在某年的公平竞赛榜

| 接口地址 | http://data.service.9h.com/leagues/{league_id}/{year}/rank-peace|
| --  | :-- |
| 请求方式 | GET ,POST, DELETE|
| 请求参数 |league_id：联赛的id，必填<br >year：联赛年份，必填<br >ids  必填, (ids=12,14,25)|

####  3.5.2.27  修改某个联赛在某年的公平竞赛榜

| 接口地址 | http://data.service.9h.com/leagues/{league_id}/{year}/rank-peace/{rankPeaceId}|
| --  | :-- |
| 请求方式 | GET ,PUT|
| 请求参数 |league_id：联赛的id，必填<br >year：联赛年份，必填<br >rankPeaceId : 公平竞赛榜id, 必填|

####   3.5.2.28  某个联赛在某年的升降级情况

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/updown|
| --  | :-- |
| 请求方式 | GET ,POST|
| 请求参数 |league_id：联赛的id，必填<br >year：联赛年份，必填|

####   3.5.2.29  修改某个联赛在某年的升降级情况

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/updown/{leagueUpdownId}|
| --  | :-- |
| 请求方式 | GET ,PUT|
| 请求参数 |league_id：联赛的id，必填<br >year：联赛年份，必填<br >leagueUpdownId : 必填|

####  3.5.2.30   某个联赛在某年的最佳评选

| 接口地址 |http://data.service.9h.com/leagues/{league_id}/{year}/outstanding|
| --  | :-- |
| 请求方式 | GET ,POST|
| 请求参数 |league_id：联赛的id，必填<br >year：联赛年份，必填|







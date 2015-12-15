### 后台管理系统


#### 1.获取置顶新闻
|接口地址|http://news.service.9h.com/v1/news/publish-news/top-news  |
|--| :--|
|请求方式| GET|

#### 2.将新闻置顶或取消置顶
|接口地址|http://news.service.9h.com/v1/news/publish-news/top-news/{news_publish_id}  |
|--| :--|
|请求方式| PUT|
|请求参数|news_publish_id：新闻Id，必填|
|请求体|如 : {"isTop":"1"}<br /> isTop：新闻是否置顶，1: 置顶，0: 未置顶;可选, 默认为: 0 |

#### 3.获取所有球员的基础资料
|接口地址|http://data.service.9h.com/v1/data/players|
|--| :--|
|请求方式| GET|
|请求参数|filters：参数名称集合(如：pageNo,pageSize,name,birth,country,nativePlace)<br />value：参数值集合(如:1,25,卡卡,1982-4-22,巴西,巴西利亚) |

#### 4.获取所有的俱乐部
| 接口地址 |http://data.service.9h.com/clubs  |
| --  | :-- |
| 请求方式 | GET|
|请求参数|pageNo,pageSize;可选<br />name : 俱乐部名称;可选<br /> enName : 俱乐部英文名;可选|

#### 5.获取所有教练的基础资料
|接口地址|http://data.service.9h.com/v1/data/coaches|
|--| :--|
|请求方式| GET|
|请求参数|filters：参数名称集合(如：pageNo,pageSize,name,birth,country,englishName)<br />value：参数值集合(如:1,25,贾秀全,1963-03-23,中国,Jia Xiuquan) |

#### 6.获取所有裁判
|接口地址|http://data.service.9h.com/v1/data/judges|
|--| :--|
|请求方式| GET|
|请求参数|filters：参数名称集合(如：pageNo,pageSize,name,birth,nationality,region,level)<br />value：参数值集合(如:1,25,王津,1970-03-01,中国,天津,国家级) |

#### 7.获取某个俱乐部某年的所有球员
|接口地址|http://data.service.9h.com/v1/data/clubs/{clubId}/{year}/players|
|--| :--|
|请求方式| GET|
|请求参数|filters：参数名称集合(如：pageNo,pageSize,name,birth,country,nativePlace,position,playerNumber,leagueType)<br />value：参数值集合(如:1,25,赵石,1993-03-16,中国,北京,门将,1,1) |

#### 8.某个联赛在某年的助攻榜
|接口地址|http://data.service.9h.com/v1/data/leagues/{leagueId}/{year}/rank-assistant|
|--| :--|
|请求方式| GET|
|请求参数|filters：参数名称集合(如：pageNo,pageSize,name,clubId,assistants)<br />value：参数值集合(如:1,25,高拉特,3,10) |

#### 9.某个联赛在某年的射手榜
|接口地址|http://data.service.9h.com/v1/data/leagues/{league_id}/{year}/rank-goal |
|--| :--|
|请求方式| GET|
|请求参数|filters：参数名称集合(如：pageNo,pageSize,playerName,clubId,goals)<br />value：参数值集合(如:1,25,阿洛伊西奥,4,22) |

#### 10.获取所有比赛
|接口地址|http://data.service.9h.com/v1/data/leagues/matches |
|--| :--|
|请求方式| GET|
|请求参数|filters：参数名称集合(如：pageNo,pageSize,leagueId,round,year,matchStatus,homeClubId,guestClubId,startAt,endAt,stadium)<br />value：参数值集合(如:1,25,1,2,2016,3,10,8,2016-10-14,2016-10-15,经开) |

#### 11.获取所有新闻
|接口地址|http://news.service.9h.com/v1/news/publish-news |
|--| :--|
|请求方式| GET|
|请求参数|filters：参数名称集合(如：pageNo,pageSize,onlined,startAt,endAt,title,origin,clubName)<br/>value：参数值集合(如:1,25,false,2015-10-22,2015-11-09,测,浪,海中) |

#### 12.获取所有广告
|接口地址|http://news.service.9h.com/v1/news/publish-ads |
|--| :--|
|请求方式| GET|
|请求参数|filters：参数名称集合(如：pageNo,pageSize,onlined,startAt,endAt,title,label,sectionType)<br/>value：参数值集合(如:1,25,true,2015-10-30,2015-12-15,备队,广告,101) |

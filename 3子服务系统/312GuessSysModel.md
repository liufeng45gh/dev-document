### 竞猜类型 ###
<A NAME="GuessType">GuessType</A>

ID|名称
-|-
1	|赛事趣味竞猜

### 竞猜题目类型 ###
<A NAME="TitleType">TitleType</A>

ID|名称
-|-
1	|赛事竞猜
2	|趣味竞猜

### 投注状态 ###
<A NAME="BetStatus">BetStatus</A>

ID|名称
-|-
1	|已投注(未开奖)
2	|已中奖
3	|未中奖

### 竞猜状态 ###
<A NAME="GuessStatus">GuessStatus</A>

ID|名称
-|-
1	|新建
2	|已发布
3	|已开始
4	|已截止
5	|已开奖
6	|已取消

### 竞猜 ###
<A NAME="Guess">Guess</A>

名称|类型|描述
-|-|-
id                  |Integer   |竞猜ID
sn					|String    |竞猜编号
title               |String    |竞猜标题
round               |Integer   |轮次
year                |Integer   |年份
guessType           |Integer   |竞猜类型ID
guessStatus         |Integer   |竞猜状态ID
startTime           |Date      |启动时间
endTime             |Date      |截止时间
publishTime         |Date      |预计开奖时间
limitTime           |Date      |领奖超时时间
jackpot             |Integer   |奖池总金额(单位分)
injection           |Integer   |注资金额
orderCount          |Integer   |投注单数
buyCount            |Integer   |购买商品数量
description         |String    |描述
operator            |String    |操作员
titles				|Title[]   |竞猜题目
cancelReason        |String    |取消竞猜原因

### 竞猜题目 ###
<A NAME="Title">Title</A>

名称|类型|描述
-|-|-
id                  |Integer   |题目ID
index               |Integer   |序列号
content             |String    |题目内容
guessId             |Integer   |竞猜ID
answerValue         |Integer   |答案值(0表示无论如何都算答对，其他选项从1开始)
answerText			|String	   |答案文本
items				|Item[]	   |题目选项
leagueTime          |Date      |比赛时间
homeTeamName        |String    |主队名称
guestTeamName       |String    |客队名称
homeTeamScore       |Integer   |主队分数
guestTeamScore      |Integer   |客队分数
homeTeamLogo        |String    |主队图标
guestTeamLogo       |String    |客队图标
result				|Integer   |胜负关系(-1主负0主平1主胜)
type				|Integer   |1 赛事竞猜 2 趣味竞猜

### 竞猜题目选项 ###
<A NAME="Item">Item</A>

名称|类型|描述
-|-|-
id                  |Integer   |选项ID
guessId             |Integer   |竞猜ID
titleId             |Integer   |题目ID
itemText            |String    |选项文本
itemValue           |Integer   |选项值（0为全都答对预留，所以选项值从1开始）

### 投注状态 ###
<A NAME="BetStatus">BetStatus</A>

ID|名称
-|-
1|	已投注
2|	已中奖
3|	未中奖

### 答案 ###
<A NAME="Answer">Answer</A>

名称|类型|描述
-|-|-
guessOrderNumber    |String    |竞猜单号(JC+13位毫秒+3位顺序号)
userId              |String    |用户ID
guessId             |Integer   |竞猜ID
titleId             |Integer   |题目ID
answerValue         |Integer   |回答值
answerText          |String    |回答文本
equirementId        |Long      |虚拟道具ID
chanceType          |Integer   |机会牌类型
freezonReason       |String    |冻结原因
freezonStatus       |Integer   |冻结状态（0：未冻结1：已冻结）
betStatus           |Integer   |投注状态
phoneNumber			|String		|投注通知手机号
userNickName		|String		|用户昵称

### 用户 ###
<A NAME="User">User</A>

名称|类型|描述
-|-|-
id                  |Long      |用户ID
uuid                |String    |uuid
account             |String    |账户名
phone               |String    |电话号码
nickName            |String    |昵称
avatar              |String    |头像
trueName            |String    |真实姓名
sex                 |String    |性别
city                |String    |城市
province            |String    |省份
birth               |Date      |生日
nhId                |String    |NHID
## 求球v1.0系统设计说明书

##### v1.0.0 2015-10-21, Ora

### 默认全局配置

```
1. 默认URL头部 http://api-qq.9h-sports.com/v1/
2. API请求的默认参数:  
	page-num(默认值1),page-size(默认值20) 
3. API返回结果的约定包含:
	oper_code: 0  非正常流程，客户端需要做异常处理。
	oper_code: 1  正常流程，结果为期待结果。
4. 删除资源的操作:
	非真实删除，统一给资源加上一个不可用状态的字段[指 useable=false]。
5. 数据库表默认字段:
	created_at: 新数据创建时间
	updated_at: 数据最后一次修改时间
	deleted_at: 软删除时间
	useable   : 数据是否可用 true[被视为可用],false[被视为软删除],默认为true
```
### 1.球场资源

#### 数据模型 

```
Table qq_field

id         自增长(长整,以下所有id字段皆为该规则)
name       球场名称
location   球场位置的文字描述
geo		   球场的地理位置
side_type  半场人数 5:5人制 7:7人制 9, 11 
light_type 灯光类型
grass_type 草地类型
field_type 球场类型
parking_type 停车场类型
room_type  更衣室类型
star       球场评分
price      球场价格，按小时计
contact_line 联系电话
```


#### 资源接口

```
GET    /fields    获取所有球场的列表
POST   /fields 	   增加一块场地


GET    /fields/{field_id}    获取某个球场的详细信息
PUT    /fields/{field_id}    修改一块场地
DELETE /fields/{field_id} 	  删除一块场地(将场地置为不可用)

```
#### 球场关联资源表

##### 球场介绍的图片 

1. 数据模型

```
Table qq_field_file

id 
field_id  球场id   -> qq_field.id
file_type 球场的附属资料，如文档，图片等 (1:image 2:video 3:text 4:doc)
thumb_url 附属资料的缩略图地址
file_url  附属资料的在线地址
```
2. 资源接口

```
GET  /fields/{field_id}/files 获取某个球场的所有附属资料信息，比如球场的介绍图片
POST /fields/{field_id}/files

GET    /fields/{field_id}/files/{file_id} 获取某块场地的某一个附件信息
PUT    /fields/{field_id}/files/{file_id} 修改某块场地的某一个附件信息
DELETE /fields/{field_id}/files/{file_id} 删除某块场地的某个附件信息
```

#### 球场评价记录表 

1.数据模型

```
Table qq_field_comment

id
field_id   球场id    -> qq_field.id
starer_id  评价人  -> qq_user.id
star       评分(1-5)
content    评价内容
comment_at 评价时间 
```
2. 资源接口

```
GET     /fields/{field_id}/comments  获取某个球场的所有评价
POST    /fields/{field_id}/comments  增加一个球场评价

GET     /fields/{field_id}/comments/{comment_id}
PUT     /fields/{field_id}/comments/{comment_id}
DELELTE /fields/{field_id}/comments/{comment_id}
```
#### 球场可用时间段表

1. 数据模型

```
Table qq_field_period

id
field_id   球场id
start_at   起始时间  格式:yyyy-MM-dd hh:mm:ss
end_at     结束时间
range      时段间隔 (/小时)
is_booked  被订走 [1:被订走 0:可用 默认为0, 这里跟useable分开，虽然可以等同]
```
2. 资源接口


#### 球队信息表

1. 数据模型

```
Table qq_team

id
name    球队名称
avatar  队徽图标
city    活动城市
region  活动区域
creator 创建人  -> qq_user.id
```

2. 数据接口

```
GET    /teams  获得所有球队
GET    /teams?user_id={user_id}  获得某个用户创建的球队
```
#### 用户信息表

```
Table qq_user

id        自增长
uuid      uuid生成规则(App侧调用)
account   用户账号,平台生成
phone     用户手机
password  密码,(加密后的密码,非明文),6-16位字母数字组合
salt      加密盐,6位随机数字字母组合
nick_name 用户昵称
avatar    用户头像图片路径
```

#### 用户收藏场地表

1. 数据模型

```
Table qq_user_favor_field

id
user_id   用户id -> qq_user.id
field_id  球场id -> qq_field.id

```
2. 资源接口

```
GET    /users/{user_id}/favor-fields  某个用户的场地收藏列表 
POST   /users/{user_id}/favor-fields  用户收藏某个场地

DELETE /user/{user_id}/favor-fields/{field_id} 用户取消收藏场地
```


#### 用户评价场地

1.数据模型
参见 qq_field_comment 相关接口

2. 资源接口

```
GET   /users/{user_id}/field-comments   某个用户的所有球场评论 注：不实现该接口，调用	qq_field_comment相关
GET   /users/{user_id}/fields/{field_id}/
```

#### 用户反馈表

1. 数据模型

```
Table qq_user_feedback

id
user_id 用户id
feed    反馈内容
```
2. 资源接口

```
GET  /feedbacks   获取所有用户反馈
POST /feedbacks   用户发表一个反馈

DELETE /feedbacks/{feedback_id}  删除一条用户反馈
```
#### 用户信息推送

1.数据模型

```
Table qq_user_message

id
user_id 
title       通知标题
content     通知正文
post_at     通知发布时间
is_read     是否阅读[1:已阅读, 0:未阅读, 默认0]
action_data 该消息的交互协议 
```

#### 球场订单表 - 订场类型

注：这里把订单做成主订单和子订单；对战相当于2个子订单，当2个子订单都付款时，主订单才会生效

1. 数据模型

```
Table qq_order_main   主订单

id
total_price      订单总价
status           订单状态 1:未付款 2:部分付款 3:全部付款 4:未付款过期失效 5:客户申请退款 6:拒绝退款 7:可退款,正在处理 8:已完成退款 
invalid_at       订单失效时间->status:4
valid_at         订单生效时间->status:3
created_at       订单产生时间->status:1

Table qq_order_son  子订单

id
booker_id        订场人  -> qq_user.id
field_id         球场id  -> qq_field.id
field_period_id  时间段  -> qq_field_period.id
price          价格   [/元]
pay_at         付款时间
pay_by         付款方式  [1:支付宝支付 2:微信支付 ]
team_id        球队id    -> qq_team.id
battle_word    对战宣言
status         订单状态  [同上，没有2状态]
```

2. 资源接口


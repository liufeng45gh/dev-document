### 3.1.2. 用户系统服务接口

#### 3.1.2.0. 用户手机下发验证码

POST https://api-csl.9h-sports.com/v1/user/phone-sms

上送: BODY: { "phone" : "135xxxxxx"}

返回: {oper_code:1}

注: 该接口会继续调用第三方系统[短信平台]进行短信下发
	该接口每个手机号24小时内限制发送5次,同一个ip24小时内限制20次(同一个公司出去的一般都是同一个ip)
	(此接口做压测要谨慎,最好跟易美那边先沟通，或者不适合做压测)


#### 3.1.2.1. 比较验证码

POST https://api-csl.9h-sports.com/v1/user/phone-checks

上送: BODY: { "telephone" : "135xxxxxx","code":"1234"}

返回: {oper_code:1}}

注: 该接口会比较用户提交的验证码和发给用户的是否一致

#### 3.1.2.2. 用户手机+验证码注册新用户

POST https://api-csl.9h-sports.com/v1/user/registers

上送: BODY: {phone:"18610814074",code:"xxxxxx",password:"xxxxxxx",rePassword:"xxxxxx"}

返回: {oper_code:1,data:"token-Characters"}

注: 该接口会需要传入 手机号,验证码,密码，重复密码


#### 3.1.2.3. 重置密码

POST https://api-csl.9h-sports.com/v1/user/reset-pass

上送: BODY: {phone:"18610814074",code:"xxxxxx",password:"xxxxxxx",rePassword:"xxxxxx"}

返回: {oper_code:1}

注: 该接口会需要传入 手机号,验证码,密码，重复密码

#### 3.1.2.4. 绑定手机

POST https://api-csl.9h-sports.com/v1/user/bind-phone/{user_id}

上送: BODY: {phone:"18610814074",code:"xxxxxx",password:"xxxxxxx",rePassword:"xxxxxx"}

返回: {oper_code:1}

注: 该接口会需要传入 手机号,验证码,密码，重复密码

#### 3.1.2.4. 从新绑定手机

POST https://api-csl.9h-sports.com/v1/user/re-bind-phone/{user_id}

上送: BODY: {phone:"18610814074",code:"xxxxxx",password:"xxxxxxx"}

返回: {oper_code:1}

注: 该接口会需要传入 手机号,验证码,密码 还需要token


#### 3.1.2.5. 比较密码

POST https://api-csl.9h-sports.com/v1/user/check-password

上送: BODY: {userId:"xxxx",password:"xxxxxxx"}

返回: {oper_code:1}

注: 该接口需要token

#### 3.1.2.5. 检查手机是否已经注册

GET https://api-csl.9h-sports.com/v1/user/is-phone-exist/{phone}

返回: {oper_code:1}


#### 3.1.2.6. 登录

POST https://api-csl.9h-sports.com/v1/user/logins

上送 :BODY : 账号登陆 {phone:"18610814074",password:"xxxxxxx"}, 微博登陆{weiboId:"xxxxxxx",accessToken:"xxxxxxxxxx"},微信登陆{weixinId:"xxxxxxx",accessToken:"xxxxxxxxxx"}

返回 : {oper_code:1,message:"xxxxx"}



#### 3.1.2.7. 用户登出系统

DELETE https://api-csl.9h-sports.com/v1/user/logins/{user_id}

#### 3.1.2.8. 删除某个注册的用户 (目前还未使用)

DELETE https://api-csl.9h-sports.com/v1/user/registers/{user_id}




#### 3.1.2.9. 上传设备 device_token

POST https://api-csl.9h-sports.com/v1/user/upload-device

request: {deviceToken:"xxxxxxxxxxxx",userId:"xxx",osType:"android",osVersion:"version"}

response:{oper_code:1}


注: 以上全部接口都是对user对象进行操作，以下是对user_info对象进行操作
-----------

#### 获取某个用户详细资料

GET  https://api-csl.9h-sports.com/v1/user/users/{user_id}

#### 更新某个用户详细资料

POST  https://api-csl.9h-sports.com/v1/user/users/{user_id}

request : {userId:1,nickName:"xxx",avatar:"http://xxx.png"} cookie: token

response : {oper_code:1}

#### 查询用户等级信息

POST https://api-csl.9h-sports.com/v1/user/user-level/{user_id}

#### 用户关注俱乐部

POST https://api-csl.9h-sports.com/v1/user/user-club-stars/{user_id}

request: {clubId:'xxxx'}

response: {oper_code:1,data: clubObject}

#### 用户取消关注俱乐部

DELETE https://api-csl.9h-sports.com/v1/user/user-club-stars/{user_id}/{club_id}

#### 获取用户关注的所有俱乐部

GET https://api-csl.9h-sports.com/v1/user/user-club-stars/{user_id}

response: {clubs: clubObjects}


---------------

#### 用户关注比赛

POST https://api-csl.9h-sports.com/v1/user/user-match-stars/{user_id}

request: {matchId:xxxx}

#### 用户取消关注比赛

DELETE https://api-csl.9h-sports.com/v1/user/user-match-stars/{user_id}/{match_id}

#### 用获取用户关注的所有比赛

GET https://api-csl.9h-sports.com/v1/user/user-match-stars/{user_id}


--------------------------------------------


#### 用户获取自己的关注他人列表(2.0未实现)

GET http://user.service.9h.com/user-follows/{user_id}

#### 用户关注其他用户(2.0未实现)

POST http://user.service.9h.com/user-follows/{user_id}

#### 用户取消关注其他用户(2.0未实现)

DELETE http://user.service.9h.com/user-follows/{user_id}/{user_id}

#### 用户获取自己的被关注列表(2.0未实现)

GET http://user.service.9h.com/user-follow-bys/{user_id}

#### 用户获得一次被关注(2.0未实现)

POST http://user.service.9h.com/user-follow-bys/{user_id}

#### 用户从被关注列表中屏蔽关注自己的用户(2.0未实现)

DELETE http://user.service.9h.com/user-follow-bys/{user_id}/{user_id}

----------------------------------------

#### 用户获取自己的每日签到记录

GET https://api-csl.9h-sports.com/v1/user/user-check-ins/{user_id}

#### 用户签到

POST https://api-csl.9h-sports.com/v1/user/user-check-ins/{user_id}

#### 获取用户今天的签到状态

GET https://api-csl.9h-sports.com/v1/user/get-user-check-ins/{user_id}

#### 获取用户签到排行

GET https://api-csl.9h-sports.com/v1/user/user-checkin-rank/{user_id}


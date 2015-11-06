### App管理服务接口

#### 1.获取快捷导航设置列表(未实现)

GET  http://setting.service.9h.com/app-navibars

#### 2.[Android]根据qudao号获取最新版本信息

POST  https://api-csl.9h-sports.com/v1/user/app-lastest-version/{qudao}

request: {osType:"android",versionId:"1.0.2"}

response: {data:{osType:"android",qudao:"91",versionId:"1.0.2"},open_code:1}

#### 3.添加一个新App版本(未实现)

POST http://setting.service.9h.com/app-versions

#### 4.删除一个App版本(未实现)

DELETE http://setting.service.9h.com/app-versions/{id}

#### 5.修改一个App版本(未实现)

PUT http://setting.service.9h.com/app-versions/{id}

#### 6.用户提交一个反馈

POST http://setting.service.9h.com/app-feedbacks

#### 7.获取所有用户反馈

GET http://setting.service.9h.com/app-feedbacks

#### 8.删除一个用户反馈

DELETE http://setting.service.9h.com/app-feedbacks/{feedback_id}


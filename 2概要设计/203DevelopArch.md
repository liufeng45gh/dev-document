### 2.3.1. 整体架构





### 2.3.2. 子系统间调用关系

#### 2.3.2.1. 通过Restful风格的HTTP协议[同步调用]

1. 详见 3子服务系统 的服务接口

#### 2.3.2.1. 通过Pub/Sub解耦的消息机制[异步调用]

1. 短信发送  

	* user:valicode  -> 短信校验       	
	* user:register  -> 注册成功

	* 将手机号放入redis队列 -> CODE_SENDING_PHONE_LIST
	* 设置手机号与验证码的关系  msgcode:{telephone} -> {code}

	* 监控进程监听队列  CODE_SENDING_PHONE_LIST ->取出并调用webservice发送

2. 消息推送  

	* feed:match     -> 比赛有新动态 (从关注俱乐部的列表中取用户列表推送)
	* feed:topic     -> 圈子有新主贴 
	* feed:reply     -> 主贴有新回帖
	* feed:comment   -> 回帖有新评论
	* feed:reply:at  -> 回帖含@其他用户
	* feed:comment:at-> 评论含@其他用户
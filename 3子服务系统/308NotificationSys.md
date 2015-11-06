### 3.9. 推送系统

### 推送系统需要侦听来自其他子系统的事件



### 推送系统内部需要侦听的事件

* send:message
* send:sms
* send:mail

#### 1. App消息推送 [+LeanCloud实现]


#### 2. 短信推送 [+LeanCloud实现]
	* 将手机号放入redis队列 -> CODE_SENDING_PHONE_LIST
	* 设置手机号与验证码的关系  msgcode:{telephone} -> {code}

	* 后台监控进程监听队列  CODE_SENDING_PHONE_LIST ->取出并调用webservice发送

#### 3. Mail推送
### 3.9. 推送系统

### 推送系统需要侦听来自其他子系统的事件



### 推送系统内部需要侦听的事件

* send:message
* send:sms
* send:mail

#### 3.9.1. App消息推送 [+友盟实现]

##### 3.9.1.1 中超老版本赛事消息推送规则(2016.8.1以前)

* 老版本赛事推送需求：跳转到比赛详情页 (自动推送只涉及赛事)
* 具体实现：友盟推送参数的 "custom" 参数中(iOS平台为"go\_custom"的自定义参数)，传入跳转协议字符串，协议规则： csl://match/live/{match\_id} ,具体格式分 Android和iOS平台不同

* 客户端通过解析协议字符串 csl://match/live/{match\_id}，得到比赛ID，跳转到比赛详情页
* 示例：
 <pre><code>
 Android:
	 {
	    "appkey":"5604ed9ee0f55a3f600040bc",
	    "production_mode":"true",
	    "description":"test",
	    "type":"unicast",
	    "payload":{
	        "display_type":"notification",
	        "body":{
	            "title":"test",
	            "ticker":"test",
	            "text":"test",
	            "custom":"csl://match/live/1",
	            "after_open":"go\_custom",
	            "play_vibrate":"true",
	            "play_sound":"true",
	            "play_lights":"true"
	        }
	    },
	    "policy":{
	        "expire\_time":"2016-08-07 15:09:53"
	    },
	    "device_tokens":"Ak1FNlgp\_lp3YI3FyO9CiQKZftL4UG\_faATQnVdHUKaf"
	}
</code></pre>

	<pre><code>
	 iOS:
	 {
	    "appkey":"55d681b567e58e3881000623",
	    "production_mode":"true",
	    "description":"test",
	    "type":"unicast",
	    "payload":{
	        "aps":{
	            "sound":"default",
	            "badge":1,
	            "alert":"test"
	        },
	        "go_custom":"csl://match/live/1"
	    },
	    "policy":{
	        "expire_time":"2016-08-07 15:24:22"
	    },
	    "device_tokens":"Ak1FNlgp_lp3YI3FyO9CiQKZftL4UG_faATQnVdHUKaf"
	}	
	</code></pre>

##### 3.9.1.2 中超新版本消息推送规则

* 新版本推送需求：细分赛事详情页跳转逻辑，并增加其他活动推送
* 版本兼容：为了兼容老版本赛事消息推送与跳转逻辑，新版本跳转使用新增推送参数，在"extra"内自定义key-value,老版本 custom 参数保留
* 自定义参数键为 ： "jump\_to", 值为协议字符串
* 协议字符串以 http:\\\ 开头，则为H5页面地址，需打开此页面地址
* 协议字符串以 csl:\\\ 开头，则为跳转到应用内页面
* csl:\\\ 跳转规则详情：

| 推送形式 | 推送触发 | 点击打开 | 协议示例 |
|:----:|:----:|:----:|:----:|
| 自动推送赛前 | 订阅比赛开始前5分钟 | 打开此比赛详情的阵容Tab | csl://match/live/{news_id}/before|
| 自动推送赛中 | 订阅比赛比分更改 | 打开此比赛详情的事件Tab | csl://match/live/{news_id}/underway|
| 自动推送赛后 | 订阅比赛结束后 | 打开此比赛详情的统计Tab | csl://match/live/{news_id}/after|
| 新闻/公告/视频/专家评球内容推送| 友盟后台发送 | 打开新闻html页面 | http://static.news.20160801.html|
| 活动新闻页推送| 友盟后台发送 | 打开活动新闻 | csl://news/{news_id} |
| 运营推送今日赛事 | 友盟后台发送 | 打开赛程列表页面 | csl://match/list |
| 运营推送积分榜 | 友盟后台发送 | 打开积分榜页面 | csl://match/leaguetable |
| 【活动】趣味竞猜 | 友盟后台发送 | 打开趣味竞猜首页 | csl://fun/guess |
| 【活动】幸运转盘 | 友盟后台发送 | 打开幸运转盘首页 | csl://fun/roulette |
| 【活动】摄影专区 | 友盟后台发送 | 打开摄影专区首页 | csl://fun/easyphoto |
| 【活动】全民票选 | 友盟后台发送 | 打开全民票选首页 | csl://fun/bestplay |
	

* 示例：
<pre><code>
 Android:
	 {
	    "appkey":"5604ed9ee0f55a3f600040bc",
	    "production_mode":"true",
	    "description":"test",
	    "type":"unicast",
	    "payload":{
	        "extra":{
	            "jump\_to":"csl://match/live/1/before"
	        },
	        "display_type":"notification",
	        "body":{
	            "title":"test",
	            "ticker":"test",
	            "text":"test",
	            "custom":"csl://match/live/1",
	            "after\_open":"go\_custom",
	            "play\_vibrate":"true",
	            "play\_sound":"true",
	            "play\_lights":"true"
	        }
	    },
	    "policy":{
	        "expire_time":"2016-08-07 16:52:27"
	    },
	    "device_tokens":"Ak1FNlgp\_lp3YI3FyO9CiQKZftL4UG\_faATQnVdHUKaf"
	}
</code></pre>

	<pre><code>
	 iOS:
	 {
	    "appkey":"55d681b567e58e3881000623",
	    "production_mode":"true",
	    "description":"test",
	    "type":"unicast",
	    "payload":{
	        "aps":{
	            "sound":"default",
	            "badge":1,
	            "alert":"test"
	        },
	        "go_custom":"csl://match/live/1",
	        "jump_to":"csl://match/live/1/before"
	    },
	    "policy":{
	        "expire_time":"2016-08-07 15:24:22"
	    },
	    "device_tokens":"Ak1FNlgp_lp3YI3FyO9CiQKZftL4UG_faATQnVdHUKaf"
	}	
	</code></pre>


#### 3.9.2. 短信推送 [+LeanCloud实现]
	* 将手机号放入redis队列 -> CODE_SENDING_PHONE_LIST
	* 设置手机号与验证码的关系  msgcode:{telephone} -> {code}

	* 后台监控进程监听队列  CODE_SENDING_PHONE_LIST ->取出并调用webservice发送

#### 3.9.3. Mail推送
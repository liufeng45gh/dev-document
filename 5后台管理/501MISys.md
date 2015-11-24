### 后台管理系统

#### 1.获取置顶新闻 

#### 1.获取置顶新闻 
|接口地址|http://news.service.9h.com/v1/news/publish-news/top-news  |
|--| :--|
|请求方式| GET|

#### 2.将新闻置顶或取消置顶
|接口地址|http://news.service.9h.com/v1/news/publish-news/top-news/{news_publish_id}  |
|--| :--|
|请求方式| PUT|
|请求参数|news_publish_id：新闻Id，必填;<br /> is_top：新闻是否置顶，1: 置顶，0: 未置顶;可选, 默认为: 0 |


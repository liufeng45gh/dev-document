
### 3.3.2. 广告管理服务接口

#### 3.3.2.1. 获取广告资源   

|接口地址 | http://ad.service.9h.com/resources |
| -- | : -- |
| 请求方式 | GET |
| 请求参数 |pageNo : 当前页码, 可选<br> pageSize : 每页行数, 可选 |

#### 2.2. 删除一条广告资源

| 接口地址 | http://ad.service.9h.com/resources/{resource_id} |
| -- | :-- |
| 请求方式 | DELETE |
| 请求参数 | resource_id : 广告资源id ,必填|

#### 2.3 新增一条广告资源

| 接口地址 |  http://ad.service.9h.com/resources|
| -- | : -- |
|请求方式 | POST |

#### 2.4. 修改一条广告资源

| 接口地址 | http://ad.service.9h.com/resources/{resource_id} |
| -- | :-- |
| 请求方式 | PUT |
| 请求参数 | resource_id : 广告资源id ,必填|

#### 2.5. 获取当前的所有频道的广告信息[已上线内容]


| 接口地址 | http://ad.service.9h.com/publish-ads/onlined|
| -- | : -- |
| 请求方式 | GET |
| 请求参数 |pageNo : 当前页码, 可选<br> pageSize : 每页行数, 可选 |

注: 该接口将会提供给API网关调用

#### 2.6. 发布一个广告信息

| 接口地址 | http://ad.service.9h.com/publish-ads|
| -- | : -- |
| 请求方式 | POST |

#### 2.7. 修改一个广告信息

| 接口地址 | http://ad.service.9h.com/publish-ads/{ad_id} |
| -- | :-- |
| 请求方式 | PUT |
| 请求参数 | ad_id : 广告id ,必填|

#### 2.8. 删除一个广告信息

| 接口地址 | http://ad.service.9h.com/publish-ads/{ad_id} |
| -- | :-- |
| 请求方式 | DELETE |
| 请求参数 | ad_id : 广告id ,必填|





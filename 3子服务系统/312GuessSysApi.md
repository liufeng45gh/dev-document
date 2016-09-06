## 3.11.2. 竞猜服务接口

正式地址:   
Swagger:  
测试地址: 
Swagger: http://123.59.61.245:8093/swagger/index.html   


### 3.11.2.1. 竞猜的所有服务接口清单

 方法 | 接口 | 用途 | 返回 | 是否走网关 
 :-- | :--  | :-- | :-- | :--
 GET| /guess/guess-info | 获取当期竞猜、题目及选项 | {} | 是
 GET| /guess/guess-infos/{user_id}| 按照中奖状态取得用户所参与的竞猜 | {} | 是
 GET| /guess/guess-infos-status| 按照竞猜状态取得竞猜列表 | {} | 是
 POST| /guess/bet| 投注竞猜 | {} | 是
 GET| /guess/guess-answer/{user_id}| 获取一个人的竞猜答案 | {} | 是
 GET| /guess/guess-answers/{user_id}| 获取一个人对于多场竞猜的竞猜答案（批量接口） | {} | 是
 GET| /guess/guess-answer-status/{user_id}| 按照状态获取一个人的竞猜答案 | {} | 是
 GET| /guess/jackpot-oper-record| 获取最新奖池更新记录 | {} | 是



 



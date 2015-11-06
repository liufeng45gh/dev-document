###  数据类型

#### 用户反馈

```SQL
Table app_user_feedback

id
user_id  反馈人id
title    反馈内容的标题
content  反馈内容正文
feed_at  反馈时间
```
#### App设备信息

```SQL
Table app_user_device

id
user_id    用户id
device_id  用户使用的设备id(用于进行信息推送)
actived_at 设备激活时间(用于排序获取用户最后一次登录激活的设备)
os_type    os类型(ios,wp,android)
os_version os版本
```

#### App版本管理 

```SQL
Table app_setting_version

id
os_type         终端系统(1:android 2:ios 3:winphone)
qudao           App投放的渠道号
version_id      版本id
version_name    版本号
version_info    版本描述
download_url    下载地址(网站自下载android/winphone使用)
appstore_url    应用介绍地址(第三方商店或者Appstore使用)
```

#### App渠道管理表（针对Android这样的在第三方平台上架的场景）

```SQL
Table app_setting_qudao

id       
code     渠道编码
name     渠道名称
```

#### App快捷导航设置

```SQL
Table app_setting_navbar

id
section_id    目录id    FK-> app_setting_section.id
order_num     快捷导航的排序(数字大在前)
```

#### App全局目录分类

```SQL
Table app_setting_section

id       
name      目录名称  (新闻/联赛/圈子/数据/我的/商城/娱乐 ...)
path      目录路径  (一级目录/二级目录/三级目录 ....)
for_app   对应的App (1:中超 2:国安)
```
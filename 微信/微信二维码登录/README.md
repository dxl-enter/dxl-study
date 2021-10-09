# 微信二维码登录

## 前端没有绑定域名的情况下
1. 获取二维码链接
https://open.weixin.qq.com/connect/qrconnect?appid=wxb829f3b08f186ae0&redirect_uri=http://ig2gnb.natappfree.cc/base&response_type=code&scope=snsapi_login&state=2021#wechat_redirect
2. 前端通过iframe加载到网页中
3. 二维码隔5分钟自动刷新一次
4. 通过前端轮询的办法调用后台接口获取的uniid
5. 用uniid和手机号密码进行绑定

## 前端绑定了域名的情况下
1. 先在index.html中引入js文件
2. 在需要的页面进行实例化（本项目是在登录页进行扫码）
3. 中间页中进行登录逻辑操作
4. 

参考文章 
1. https://www.jianshu.com/p/3733777a2020
2. https://blog.csdn.net/WYH1205/article/details/115489751

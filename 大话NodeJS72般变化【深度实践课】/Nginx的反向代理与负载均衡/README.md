### 部署nodejs上线步骤
1. 打开https://brew.sh/index_zh-cn.html
2. brew search nginx  brew install nginx
3. brew info nginx
4. nginx -v 查看nginx信息
5. 启动sudo brew services start nginx(默认端口8080)
  * 备注：如果你安装过jenkins的话这里会失败
  * sudo launchctl unload/Library/LaunchDaemons/org.jenkins-ci.plist
  * systemctl start jenkins
6. 关闭sudo brew services stop nginx/nginx
7. nginx -s reload 、nginx -s stop
8. 打开nginx具体安装目录 查看配置文件 /usr/local/etc/nginx/
9. 验证配置文件nginx -t -c 自己的配置文件地址
10. 拷贝配置文件至node项目目录 重新修改
11. 服务器端的nginx地址

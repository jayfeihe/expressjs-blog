Node.js+Express+mongodb3.x开发的博客初级版本,基于WebStorm IDEA开发
==============

##用expressjs开发的个人博客系统
###主要功能和特色
1. 文集功能，将文章整理成册
2. 功能齐全的富文本编辑器，写博客更随心
3. 响应式布局，手机上效果也很出色
4. 搜索引擎优化，自动提取文章大纲和关键词，填入description和keywords
5. 占内存少，方便托管于bae的128m最小web服务上
6. 漂亮的侧边栏，博主信息，标签，文集，文章大纲等
7. 文章大纲根据文章的标题自动提取
8. 自定义URL，博客链接可以体现主题

###待开发功能
1. 文章大纲自动添加锚点进行定位
2. 增加markdown的编辑器
3. 回复审核和删除功能的完善
4. seo优化目前只是雏形，继续深入开发。
5. 文章所在文集下的上一篇和下一篇文章

###项目启动流程：
1.安装并启动mongodb
   E:\mongodb\bin>mongod --dbpath=E:\mongodb\db
   
2.启动mongodb客户端
   E:\mongodb\bin>mongo

3.创建数据库和相关文件(创建mongodb的新用户并授权)
   show dbs
   use blog
     db.createUser(
           {
             user: "root",
             pwd: "1234",
             roles: [ "readWrite", "dbAdmin" ]
           }
        )
   db.auth("root","1234");

4.配置 common/config.js文件
      dbName 为 blog
      dbUser 为 root
      dbPass 为 1234
      dbAddress 为 mongodb所在机器IP
  注mongodb默认不能远程连接，如果需要远程连接，要更改mongo的配置。如果在本机连接，dbUser, dbPass不要填。

5.执行
      npm install
      node server.js

6.到 IP:3000/register 下注册
  注册成功之后注释掉useRoutes.js的63-66行。
  
7.到 IP:3000/admin 下管理博客


常见错误解析：
1.>{ [Error: Cannot find module '../build/Release/bson'] code: 'MODULE_NOT_FOUND' }

   js-bson: Failed to load c++ bson extension, using pure JS version

    原因：bson中的bson.js路径不对
    解决方案：
         Ctrl+Shift+F 全局查找 ../build/Release/bson,找到后
         修改 node_modules\mongoose\node_modules\mongodb\node_modules\bson\ext中的index.js
         将两处
           bson = require('../build/Release/bson');
         修改为
           bson = require('../browser_build/bson');


###本人技术博客：
[逍遥飞鹤的博客](http://blog.csdn.net/he90227)

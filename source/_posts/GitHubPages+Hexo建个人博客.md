---
title: 建立个人博客
date: 2018-10-16 22:28:59
tags: 工作
---
在朋友的帮助下建立了自己的个人博客，以后会慢慢更新，至此，人生的任务清单中，又少了一项
<!-- more -->
## 购买域名
1. godaddy购买[域名](https://sg.godaddy.com/zh)
2. 管理DNS  
GoDaddy>管理域名>管理DNS
删除所有类型为A的记录,添加两条记录:
   - 类型为”A (Host)” ，”主机” 为 @ ， “指向” = 192.30.252.153
   - 类型为”A (Host)” ，”主机” 为 @ ， “指向” = 192.30.252.154
   >github pages提供的域名，192.30.252.153和192.30.252.154

## 创建github pages
1. 创建repo
repo name：username.github.io
2. 绑定域名
cname文件中添加域名

## 安装hexo
1. 安装Node.js  
去[官网](https://nodejs.org)下载安装最新版本
   >node -v #查看node版本   
    npm -v #查看npm版本
2. 安装Git配置SSH
   - xcode自带Git
   - 配置SSH   
      - cd ~/.ssh #检查是否有ssh，No such file or directory 表示没有
      - ssh-keygen -t rsa -C "邮件地址@youremail.com" #生成SSH输入密码串
      - /Users/your_user_directory/.ssh/id_rsa.pub #打开ssh文件，复制key
      - Account Settings—>SSH Public keys —> add another public keys #粘贴key，添加设备title，addkey
      - ssh -T git@github.com#测试
      - YES
      - git config --global user.name "yourname" #用户名
      - git config --global user.email  "youremail@gmail.com" #填写自己的邮箱

    - 显示隐藏文件。切换快捷键：Command+Shift+.（点）

3. 安装hexo  
   - sudo npm install -g hexo-cli #安装hexo
   - hexo -v #查看版本，是否安装成功

4. 初始化hexo
   - mkdir blog #常见博客文件夹名称
   - cd blog #进入博客文件
   - hexo init #初始化
   - hexo server或者hexo s #启动hexo

5. 下载hexo主题
   - git clone https://github.com/iissnan/hexo-theme-next themes/next #在themes创建主题

6. 配置Hexo  
   - 打开根目录的_config.yml配置文件
   >title #网站名称  
    description #网站描述  
    author #作者  
    language:zh-CH #语言  
    theme: next #配置主题  
    type:git #配置部署信息  
    repository:https://github.com/ggkai/ggkai.github.io.git  
    branch:master

   - 配置主题风格
   >next下的主题配置文件_config.yml，并在其中搜索scheme属性，注释掉不使用的加#，使用的去掉#

## 写作
1. 创建博客
   - cd blog
   - hexo new "blogname" #在blog/source/_posts中就会看到一个blogname.md的文件
2. 编辑文章
   - title: postName #文章的名称，可以任意修改，不会出现在URL中
   - date: 2015-04-25 15:30:16 #文章的时间，一般不改，当然也可以任意修改
   - categories: #文章的分类目录，可以为空
   - tags: #文章的标签，多标签请用格式[tag1,tag2,tag3]，可以为空
   - description: #本页的描述，可以为空
   >需要注意的是，上面所有冒号:后面必须要有一个空格，不然会报错。
   - 网站首页摘要，点击Read More链接打开全文：
   >\---  
   摘要  
   \<!--more-->  
    正文
3. 发布
   - hexo clean #清除缓存
   - hexo generate #生成静态文件
   - hexo server #启动本地服务器，默认端口4000'ctrl + c'关闭
   - hexo deploy #部署到服务器
   - hexo deploy -g 生成并部署
4. git远程同步
   - git status #查看更改  
   - git add +A #添加更改  
   - git commit #提交到本地  
   - git push origin #同步到远程  

## 多设备同步
- 安装nodejs
- 安装git
- 安装hexo
   >sudo npm install -g hexo-cli
- clone 本仓库
   >git clone https://github.com/ggkai/blog-release.git
- npm install

## 建站问题
1. 报错  
npm install hexo-deployer-git --save #重新 deploy 即可
>Deployer not found:git  
2. 域名绑定  
/source目录中创建CNAME文件，记录 www.gogokai.com
3. 修改头像  
如果想修改头像可以直接在主题的_config.yml文件里面修改、友情链接
4. 缓存问题  
提交了更新但是没有文章内容，需要清理缓存
   >hexo clean#清除缓存，重新生成部署
5. 图床  
七牛图床，[教程](https://zhuanlan.zhihu.com/p/34747279)
6. 报错  
   >xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun

   >xcode-select --install
7. hexo server报错  
   错误：   
   >ERROR Local hexo not found in E:\blog，ERROR Try running: 'npm install hexo --save'

   解决方案：  
   >cd blog  
    npm install  
    hexo server  
   
   原因分析：
   >.gitignore文件里面忽略了node_modules文件夹，所以这个文件夹没有更新上去。所以用npm重新安装

## 参考
<https://hexo.io/zh-cn/docs/>
<https://www.jianshu.com/p/dfcae367aae6>

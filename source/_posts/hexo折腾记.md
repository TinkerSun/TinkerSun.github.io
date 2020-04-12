---
title: hexo折腾记
date: 2019-03-27 15:01:57
tags: [hexo]
categories:
---
### 1、安装git
下载地址：https://git-scm.com/downloads
```
$ git config --global user.name "xxx"
$ git config --global user.email xxx@yyy.com
$ ssh-keygen -t rsa
```
### 2、安装node.js
下载地址：https://nodejs.org/en/
可用下列命令查看安装的版本号
>node -v
>npm -v

### 3、安装并配置hexo
>npm install -g hexo-cli

<!--more-->
常用hexo命令
```
hexo init blog         # 初始化博客
hexo n HelloWorld      # 新建文章
hexo n page "pageName" # 新建页面
hexo g                 # 生成
hexo s                 # 启动服务预览 在本地预览效果，默认情况下，访问网址为： http://localhost:4000/
hexo d                 # 部署
hexo clean             # 清理缓存
```

hexo的help如下：
```
Usage: hexo <command>

Commands:
  clean     Remove generated files and cache.
  config    Get or set configurations.
  deploy    Deploy your website.
  generate  Generate static files.
  help      Get help on a command.
  init      Create a new Hexo folder.
  list      List the information of the site
  migrate   Migrate your site from other system to Hexo.
  new       Create a new post.
  publish   Moves a draft post from _drafts to _posts folder.
  render    Render files with renderer plugins.
  server    Start the server.
  version   Display version information.

Global Options:
  --config  Specify config file instead of using _config.yml
  --cwd     Specify the CWD
  --debug   Display all verbose messages in the terminal
  --draft   Display draft posts
  --safe    Disable all plugins and scripts
  --silent  Hide output on console

For more help, you can use 'hexo help [command]' for the detailed information
or you can check the docs: http://hexo.io/docs/
```

配置Deployment，在其文件夹中，找到_config.yml文件，修改repo值
```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: git@github.com:TinkerSun/TinkerSun.github.io.git
  branch: master
```

### 4、配置next主题
>git clone https://github.com/theme-next/hexo-theme-next themes/next

- hexo 首页文章只显示一部分
```
# Automatically scroll page to section which is under <!-- more --> mark.
scroll_to_more: true
```
- hexo 添加站内搜索

  1、 安装相关插件  `npm install hexo-generator-searchdb --save`

  若有fsevents相关警告可不必理会，此时已经安装好了

  2、 修改根目录下的_config.yml，添加以下内容
  ```
  search:
    path: search.xml
    field: post
    format: html
    limit: 10000
  ```

  3、 修改next主题目录下的_config.yml，将local_search的false改为true
  ```
  local_search:
    enable: true
  ```

- hexo 写文章时用到图片如何处理

  1、 安装相关插件  `npm install hexo-asset-image --save`

  2、 修改根目录下的_config.yml，将post_asset_folder:这个选项设置为true

- hexo 修改文章底部的#号标签
  
  修改模板/themes/next/layout/_macro/post.swig，搜索 `rel="tag">#`，将其中的 # 换成`<i class="fa fa-tag"></i>`

- hexo 添加置顶

  1、 安装相关插件
```
npm uninstall hexo-generator-index --save
npm install hexo-generator-index-pin-top --save
```

  2、 在需要置顶文章的front-matter中加上`top: true`

  3、 修改模板/themes/next/layout/_macro/post.swig，在`<div class="post-meta">`标签下，添加如下代码：
  ```
  {% if post.top %}
  <i class="fa fa-thumb-tack"></i>
  <font color=7D26CD>置顶</font>
  <span class="post-meta-divider">|</span>
  {% endif %}
  ```

### 5、其他事项
- powershell无法运行hexo，报错如下
```
hexo : 无法加载文件 C:\Users\Administrator\AppData\Roaming\npm\hexo.ps1，因为在此系统上禁止运行脚本。
```
  解决方法： 

  1、 以管理员身份打开powershell

  2、 `set-ExecutionPolicy RemoteSigned` 更改权限为A 3

  3、 通过 get-ExecutionPolicy 查看当前的状态
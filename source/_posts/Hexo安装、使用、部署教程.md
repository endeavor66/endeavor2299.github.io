---
title: Hexo安装、使用、部署教程
date: 2020-11-22 12:52:24
tags: 技术总结
---

### 1、基础环境（预先安装）

+ git

+ nodejs

  + 官网下载地址：[nodejs.org]()
+ 安装包包含 nodejs + npm，直接下一步，即可完成安装。

``` bash
# 检查安装是否成功
$ git -v
$ node -v
$ npm -v

# 更换下载源（提高下载速度）
$ npm config set registry https://registry.npm.taobao.org
```

### 2、Hexo 安装

```bash
# 1、安装 hexo
$ npm install -g hexo-cli

# 2、新建工作目录，存放hexo的配置文件、主题、博客（自己写的）等
$ mkdir blog/
$ cd blog/

# 3、初始化hexo环境(必须进入一个空目录进行初始化！)
$ hexo init

##########  至此，hexo安装完成！ #########
```

### 3、Hexo 使用

```bash
# 1、新建博客文件，生成的文件存放在 blog/source/_post/文件名.md
$ hexo n '文件名'

# 2、自定义“文件名.md”内容
使用本地markdown工具进行编辑

# 3、文件渲染
$ hexo g

# 4、本地环境测试（hexo提供的测试服务器，将本地编写的博客文件渲染并展示）
$ hexo s  #（浏览器输入：localhost:4000即可查看）
```

### 4、Hexo 部署

``` bash
# 1、安装 hexo-githubPage 插件
npm install --save hexo-deployer-git

# 2、新建仓库，名称必须为：{github用户名}.github.io

# 3、复制该仓库的路径

# 4、编辑 blog/_config.yml文件
deploy:
  type: 'git'
  repo: '仓库地址'
  branch: '分支名'

# 5、部署到github page
$ hexo d
```





### 5、Hexo 个性化

#### 1) 更换主题

```bash
# 1、从github克隆第三方主题，保存到：blog/theme/主题名
$ git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia

# 2、配置 blog/_config.yml文件
theme: yilia

# 3、保存提出
$ hexo clean  # 清空缓存 
$ hexo g 		# 重新渲染 
$ hexo s 		# 测试用
$ hexo d 		# 部署到github page
```




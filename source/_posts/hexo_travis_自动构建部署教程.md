---
title: hexo + travis 自动化构建部署
date: 2020-11-22 20:01:46
tags: 技术总结
---

### 1、初始化本地仓库

+ master：存放 hexo 项目

```bash
# blog/ 目录建立和初始化git仓库
cd blog/
git init
git add --all
git commit -m '初始化仓库'
```

### 2、添加远程库的相关信息

```bash
# 其中origin为远程库地址别名
git remote add origin '远程库地址'
```

### 3、travis 开启仓库监听

（[Travis CI - 官网](https://travis-ci.org/)）

![1606047440178](C:\Users\endeavor\AppData\Roaming\Typora\typora-user-images\1606047440178.png)

### 4、GitHub添加Token "GH_TOKEN" 。

+ **目的： 授权travis操作github仓库的权限**

1）头像 -> settings -> Developer settings -> Personal access tokens -> Generate new token

![1606047707789](C:\Users\endeavor\AppData\Roaming\Typora\typora-user-images\1606047707789.png)

2）填写 token 名，勾选权限（repo 仓库的操作权限，包括读写文件）

![1606047799281](C:\Users\endeavor\AppData\Roaming\Typora\typora-user-images\1606047799281.png)

### 5、添加.travis.yml文件

```yml
# .tarvis.yml
language: node_js # 指定语言环境
node_js:
  - "13" # 指定 NodeJS 版本

# 安装package.json描述的依赖
install:
  - npm install

# 清理和生成静态资源
script: 
  - hexo clean
  - hexo generate 

after_success: 
  # 找到静态资源
  - cd ./public
  - git init
  # user.name 和 user.email 让 travis 能登录你的 github
  - git config user.name "endeavor2299"
  - git config user.email "1932317892@qq.com"
  - git add .
  - git commit -m "docs:update articles"
  # GH_TOKEN 是 github 允许 travis 访问生成的凭证
  # GH_REF 告诉 travis 往哪个仓库推送代码，具体值下面配置
  - git push --force --quiet "https://${GH_TOKEN}@${GH_REF}" master:master
  
branches: # 指定要构建的分支
  only: # only 表示只构建以下分支
  - develop
  
env:
  global:
    # 定义往哪个仓库推送代码，注意事项见下面
    - GH_REF: github.com/endeavor2299/endeavor2299.github.io.git
```

### 6、将.travis.yml推送到远程仓库

+ 触发构建：commit 中包含 .travis.yml 会自动触发 travis ci 的构建
+ 远程仓库一共包含两个分支
  + master ：存放 hexo 渲染完成的静态文件 （结果区，存放生成的博客页面静态资源）
  + develop  :  存放 hexo 工程文件（工作区，将markdown渲染为静态资源）

```bash
# 本地commit 
git add .travis.yml
git commit -m 'add .travis.yml'

# 推送到远程库
# git push <远程仓库别名> <远程仓库分支>
git push origin develop
```

### 7、构建结果

+ 回到 travis ci 页面，会发现自动构建执行

![1606048564143](C:\Users\endeavor\AppData\Roaming\Typora\typora-user-images\1606048564143.png)
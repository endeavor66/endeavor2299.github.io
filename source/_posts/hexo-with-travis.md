---
title: hexo + travis 自动化构建部署
date: 2020-11-22 20:01:46
tags: 技术总结
---

1、初始化本地仓库

+ master：存放 hexo 项目

```bash
# 在blog/目录建立git仓库
cd blog/
git init
git add --all
git commit -m '初始化仓库'

git branch develop
```


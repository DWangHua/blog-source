---
title: 使用Hexo和GithubPage搭建博客
date: 2018-02-20 21:02:35
tags:
---

# 环境准备
1. git bash (windows用户)
2. node.js
3. 通过npm全局安装hexo `npm install hexo -g`

# github准备
1. 创建一个仓库，仓库名称为`yourname.github.io`，比如你注册github时的用户名是12345，那么此时仓库的名称就应该是 `12345.github.io`
2. 通过gitbash生成ssh-key，在gitbash中键入`ssh-keygen -t rsa -C youremail@example.com`
3. 将上一步生成的id_ras.pub的内容上传到github上(登录状态下前往<https://github.com/settings/keys>)，点击 New SSH key，将id_ras.pub的内容复制进去
4. 进入gitbash，通过`ssh -T git@github.com`验证ssh-key是否添加成功

# hexo配置
1. 首先通过`hexo init [folder]`命令创建一个文件夹
2. 进入上一步创建的文件夹，找到`_config.yml`文件，修改一些配置项
```
deploy
  type: git
  repo: https://github.com/YourgithubName/YourgithubName.github.io.git
  branch: master
```
3. 安装hexo-deployer-git，`npm install hexo-deployer-git --save`
4. 运行 `hexo deploy` 命令
5. 进入开始时创建的仓库，打开GitHub Pages功能(可能之前就已经打开了)
6. 访问githuapages，你就能看到你的博客了！

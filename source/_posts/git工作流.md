---
title: git工作流
date: 2018-06-13 17:21:46
comments: true
tags:
    - git
    - fork
---

### fork

1.首先点击frok按钮，将代码fork到自己的私有仓库
2.拉取代码到本地文件
```bash
git clone git@gitlab.zeaho.com:yuanlin/gitflow.git && cd gitflow
```
3.添加远程地址名字，默认clone地址会设为origin
```bash
git remote add upstream git@gitlab.zeaho.com:frontend/gitflow.git && git remote -v
//这里的upstream代表远程上线公用仓库
```
4.拉取远程上线最新代码，将代码push到自己的仓库
```bash
git pull upstream master && git push origin master
```
5.基于本地开发新的分支
```bash
git checkout master && git checkout -b feature/SAAS-6666
```
6.将改动代码提交到本地仓库
```bash
git add . && git  commit -m "commit message" && git push origin feature/SAAS-6666
```
7.合并代码 merge request
8.同步主分支代码删除本地分支
```bash
git checkout master && git pull upstream master && git push origin master

git  branch -D feature/SAAS-6666 && git push origin :feature/SAAS-6666
```
9.内测代码，将代码提交到测试服
```bash
git checkout master && git checkout -b hotfix/SAAS-8888

// 修改代码

git add . && git  commit -m "commit message" && git push origin hotfix/SAAS-8888
//内测时的master分支 只merge hotfix分支 不merge feature分支!
//内测“merge request -> review & merge -> 同步”与开发相同
```
10.发布到正式服
```bash
git checkout master && git tag v0.0.1

git push upstream v0.0.1
```
11.同步
```bash
git fetch upstream && git push origin --tags
```
---
layout: post
title: "如何加密公开github"
tags: [github]
---

##	安装

**For Linux**

	$git clone https://github.com/hilr/git-encrypt.git
	$cd git-encrypt 
	$chmod 755 gitcrypt
	$sudo ln -s "$(pwd)/gitcrypt" /usr/local/bin/gitcrypt

**For Windows**

TODO

## 创建一个Git源. 

**1.** 创建一个没有初始化的git源.
**2.** 执行以下命令:

	$mkdir repo
	$cd repo
	$git init 
	$gitcrypt init 
	$touch README
	$git add README 
	$git commit -m "first commit" 
	$git remote add origin https://github.com/hilr/repo.git
	$git push origin master

**3.** 备份repo/.git/config，此文件用于解密 

## 本地克隆git源

**1.** 使用共享的config文件替换本地的文件。

**2.** 执行以下命令来解密： 

	$git clone -n https://github.com/hilr/repo.git
	cp config_backup repo/.git/config
	cd repo 
	git reset --hard HEAD

完成

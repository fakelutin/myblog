---
title: Windows配置go语言
description: Windows配置go语言
date: 2024-11-20 18:02:40+0000
categories:
  - window
tags:
  - setup
---

# Windows 配置go环境

##### 本笔记参考于CSDN上一篇教程，<u><a href="https://blog.csdn.net/xuezhe5212/article/details/139327521">点击次处</a></u>查看原教程

## 1.go的下载

官网下载：https://golang.google.cn/  <u>[点击此处](https://golang.google.cn/dl/go1.23.3.windows-amd64.msi)</u>下载

    *如果嫌慢的话也可以尝试下面这个*

Alist云端下载：<u>[点击此处](http://47.97.115.73:5244/%E7%BD%91%E7%9B%98%E8%B5%84%E6%BA%90/go1.23.3.windows-amd64.msi)</u>跳转

## 2.go的安装

1. 双击.msi文件打开

2. 点击next

3. 点击next

4. 设置自己喜欢的路径后，点击next

5. 点击install

6. 这个时候后弹出来一个窗口，询问是否安装，此时点击 是 即可

7. 点击finish

## 3.检查go的文件

    此时进入刚刚安装的go的根目录，核对以下文件

```
api
bin
doc
lib
misc
pkg
src
test
codereview.cfg
CONTRIBUTING.md
go.env
LICENSE
PATENTS
README.md
SECURITY.md
VERSION
```

    核对后，进入bin文件夹，打开go.exe进入go编译器，若能正常运行进入下一步

## 4.配置go环境

1. 在设置中找到<环境变量>(不同版本系统位置不同，紧粗略说明)

2. 进入<系统属性>后，点击右下角<环境变量>

3. 在下方的<系统变量>中找到<Path变量>，双击打开

4. 在列表中查看，若没有出现<\go\bin>格式的路径，则进行第五步，有则跳过

5. 找到安装的go的bin文件夹，复制改路径，回到<编辑环境变量>界面，点击右上角的<新建>，粘贴路径，点击右下角<确定>即可

## 5.转移文件安放位置(选做)

    若不想在go的根目录下存储代码的话，可以根据如下操作：

1. 在想存储代码的地方创建一个文件夹(不包含非法字符和中文)

2. 在此文件夹中再创建3个文件夹，名称及功能如下：
   bin : 可执行文件存储位置
   pkg：生成的包文件的位置
   src : 项目的位置

3. 修改环境变量：
   
   1. 打开<环境变量>,找到上方的<用户变量>中的<GOPATH>
   
   2. 双击打开，复制之前创建的文件夹位置并粘贴替换到下面那一行的路径(变量值)
   
   3. 找到<GOROOT>，若无则新建一个即可，变量值为go的根目录
   
   4. 找到<GOBIN>若无则创建，变量值为创建的文件夹下的bin地址

4. 测试：
   在cmd下运行
   ` go run app.go`
   若成功运行则完成安装



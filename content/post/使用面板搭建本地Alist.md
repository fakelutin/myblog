---
title: AList宝塔面板搭建,美化并挂载到阿里云盘
description: Alist在宝塔面板中的搭建，美化，本地存储及阿里云盘Opne的设置
date: 2024-11-15 17:00:00+0000
categories:
  - linux
tags:
  - alist
---

# Alist在宝塔面板中的搭建，本地存储及阿里云盘Opne的设置
## Alist
### 下载 ：
1. 使用宝塔Linux面板（详情可前往链接）中的软件商店进行傻瓜式下载（仅针宝塔面板生效的）
2. 前往Alist官网获取更多详情，若想下载请移步此处
3. 可使用1panel 平替宝塔面板，详情请点击此处查看安装教程，并前往软件商店进行安装
### 1panel/宝塔面板使用
在软件商店里点击alist，再点击启动即可
Docker的可以选择端口，例如12345，而不是Alist默认的5244
### 访问
复制<服务状态-alist控制台访问地址>中的链接打开即可,或者在所在服务器后输入端口（默认端口为：5244）
### 登陆
自己看
### 本地存储配置
点击正下方<管理>，进入"AList管理"页面，点击<存储>，点击<添加>
驱动选择<本机存储>（在蓝奏云，分秒帧之间）
挂载路径填入</"name">格式（此处为网盘中显示的文件夹）
根文件夹路径填入</"RealName">(此处为网盘读取的根目录，要填本地存在的文件夹)
其余不需要进行多余操作，记得选择排序即可
### 查看：
点击左侧<主页>即可返回网盘主页，可以看到刚刚添加的文件夹
需要注意的是，挂载路径填入的最后一位，会表现为顶替 根目录的头路径
### 拓展：
可以重复上述<配置存储>操作建立多个文件夹
需要声明的是，每个存储只会读取一个根目录
### 设置用户访问：
在<Alist管理>界面中，点击<用户>，点击<guest-编辑>，启用即可
## 阿里云存储配置：
获取更多详细教程，请阅读官方教程
进入Alsit管理界面，选择存储，选择添加，驱动选择`阿里云盘Open``
需要设置的如下：
> 挂载路径：

也就是网盘中显示的名字
### 云盘类型
- 资源库：指云盘内除备份文件夹以外的文件夹
- 备份盘：指云盘内的备份文件夹
- 根文件ID：指用网址表示的文件夹代码
### 获取方式：
通过网页进入阿里云盘，进入你要导入的文件夹，例如https://www.alipan.com/drive/file/all/25a，其中25a就是文件夹的代码（这个位置的代码即可），然后将此填入即可
刷新令牌：
点击此处进入获取
操作方式：
点击 Go to login，这时候如果已经在网页上登录了阿里云盘，则在跳转后点击允许，然后便会自动获得refreshToken，复制后填入即可
## 其他：
1. 不建议启用  秒传  功能，此功能会预存储文件进服务器，会造成不必要的占用，属于是用空间换取时间
2. 其余设置不重要，按喜好设置即可
3. 保存后回到 主页 就能看到存储进的文件夹了
## Alist美化
在Alist管理界面，点击设置，点击全局，注意看到自定义头部和自定义内容
> 可以去网上搜索Alist美化，然后去复制别人的
> 想自制的建议去搜索CSS文件相关教程，这里提供一个参考
> 下面内容中有可以参考的简化的头文件以及自定义内容，是一个渐变背景，也就是本人的网盘使用的简易背景
> 配置好后记得翻到最下面 保存

附件：本人使用的简易头文件及自定义内容

头文件
```
<script src="https://polyfill.io/v3/polyfill.min.js?features=String.prototype.replaceAll"></script>
 
<link rel="stylesheet" href="https://npm.elemecdn.com/lxgw-wenkai-webfont@1.1.0/lxgwwenkai-regular.css" />
 
<style>
.notify-render .hope-close-button{
	display: none;
}
 
#canvas-basic {
	position: fixed;
	display: block;
	width: 100%;
	height: 100%;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	z-index: -999;
    backdrop-filter: blur(10px)!important;
}
 
  #root > .header {
    background: rgba(255, 255, 255, 0);
  }
  .hope-ui-light .body > .nav {
    background-color: rgba(255, 255, 255, 0.2);
    border-radius: var(--hope-radii-xl);
  }
  .hope-ui-dark .body > .nav {
    background-color: rgb(0 0 0 / 50%);
    border-radius: var(--hope-radii-xl);
  }
  .body > .nav::after {
    display: none;
  }
 
.obj-box.hope-stack.hope-c-dhzjXW.hope-c-PJLV.hope-c-PJLV-iigjoxS-css{
background-color:rgb(0 0 0 / 50%) !important;
}
.hope-c-PJLV.hope-c-PJLV-iiuDLME-css{
background-color:rgb(0 0 0 / 50%) !important;
}
.obj-box.hope-stack.hope-c-dhzjXW.hope-c-PJLV.hope-c-PJLV-igScBhH-css {
background-color: rgba(255, 255, 255, 0.2) !important;
backdrop-filter: blur(10px)!important;
 
}
.hope-c-PJLV.hope-c-PJLV-ikSuVsl-css{
background-color: rgba(255, 255, 255, 0.2) !important;
backdrop-filter: blur(10px)!important;
}
.hope-c-ivMHWx-hZistB-cv.hope-icon-button{
background-color: rgba(255, 255, 255, 0.2) !important;
backdrop-filter: blur(10px)!important;
}
.hope-c-PJLV-ijgzmFG-css{
background-color: rgba(255, 255, 255, 0.2) !important;
backdrop-filter: blur(10px)!important;
}
.hope-ui-light pre{
    background-color: rgba(255, 255, 255, 0.2) !important;
    backdrop-filter: blur(10px)!important;
}
.hope-ui-dark pre {
    background-color: rgba(255, 255, 255, 0) !important;
    backdrop-filter: blur(10px)!important;
}

*{font-family:LXGW WenKai}
*{font-weight:bold}
body {font-family: LXGW WenKai;}
 </style>
```


自定义内容：
```
<canvas id="canvas-basic"></canvas>
<script src="https://npm.elemecdn.com/granim@2.0.0/dist/granim.min.js"></script>
<script>
var granimInstance = new Granim({
    element: '#canvas-basic',
    direction: 'left-right',
    isPausedWhenNotInView: true,
    states : {
        "default-state": {
            gradients: [
                ['#a18cd1', '#fbc2eb'],
                 ['#fff1eb', '#ace0f9'],
                 ['#d4fc79', '#96e6a1'],
                 ['#a1c4fd', '#c2e9fb'],
                 ['#a8edea', '#fed6e3'],
                 ['#9890e3', '#b1f4cf'],
                 ['#a1c4fd', '#c2e9fb'],
                 ['#fff1eb', '#ace0f9']
           
            ]
        }
    }
});
</script>
```

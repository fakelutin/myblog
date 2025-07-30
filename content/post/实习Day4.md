+++
title: '实习记录Day4'
date: 2025-07-24T22:00:00+0000
draft = false
+++

# 实习Day4

## 预计学习任务清单：

- [x] 查看昨天实现的爬虫并解决认证问题

- [x] 尝试完成sql测试注入插件

- [x] 使用sqlmap完成sql测试

- [ ] 使用phpstudy完成sqlmap的测试

- [ ] 

## 日程记录

1. 尝试运行爬虫取得成功，并且解决认证问题，方法是在url后面直接加上`/api-key`即可。但是现在看不懂爬虫爬出来的东西有什么作用，只知道爬出来的东西是种漏洞。

2. 根据昨天查找的资料，也就是这篇文章：[使用Burp Suite和Python进行自动化漏洞挖掘—SQL测试注入插件_burp中sql插件-CSDN博客](https://eziyu.blog.csdn.net/article/details/130559213?spm=1001.2014.3001.5502) ，尝试完成sql注入插件测试。

3. 遇到困难，代码中import java无法被识别，经查询是需要导入到burp中
   
   导入时出现报错，先交给ai进行修改。修改后报错没有变化。
   
   最后查出2个问题
   
   1. 不支持中文，也就是没有ascii码支持
   
   2. 优化的时候使用了python 3.7的内容，但是Jython只识别到python 2.6
   
   实际上这些问题作者甚至都提到过(没眼力见)
   
   成功导入后没有显示出那个拓展，但是可以将包发送给插件
   
   尝试将源代码导入，删去中文字符后能正确的导入并显示出来。
   
   导入后依旧不能使用。将包发给插件后，插件的名称之间变红并且没有任何输出，估计是不能用的

4. 记得作者提到过他写的这个不如sqlmap，尝试用sqlmap去完成sql注入工作
   
   初步参考这个文章 [SQL注入sqlmap联动burpsuite之burp4sqlmap++插件 - smileleooo - 博客园](https://www.cnblogs.com/smileleooo/p/18063933) 
   
   花了相当的时间查找config在哪开启，后来随后一点，将一个包发给`sqlmao4burp++`就打开了，无敌了。
   
   尝试着使用这个工具，目前有以下结论：
   
   1. 如果是拦截的，那么要先发给repeater才能发给sql
   
   2. 如果发送给sql的包里没有相应的参数，那么就会报错。比如访问alist，但是没有给用户和密码的参数，那么它就会报错。
   
   3. 成功访问进去了，但是如果该包没有sqlmap能注入的漏洞，那么就会有包含如下内容的提示
      `[CRITICAL] all tested parameters do not appear to be injectable`

5. 看了一圈，自学的文章集都很贵，不如接着看看bp，同时也从之前的文章中找到了一份免费的教程 [Burp Suite 实战指南](https://t0data.gitbooks.io/burpsuite/content/) 接着开始学习。学了会发现太老了，而且其实不算是很有用，毕竟学到现在了都。有点不知道该学啥了。(求明天换个员工来值班吧，想问问新的东西了)

6. 转去看看sqlmap是个啥到底。目前参考文章[sqlmap的安装及使用教程 - tuuli - 博客园](https://www.cnblogs.com/tuuli/p/17586592.html) 配套文章 [搭建本地DVWA靶场教程 及 靶场使用示例 - tuuli - 博客园](https://www.cnblogs.com/tuuli/p/17586575.html) 
   
   MD，给坑了，这个小皮面板中要下的东西是phpStudy(这东西下载好慢，然后下载失败了一次，然后重下又快了)，而不是什么产品，意难平。可以考虑考虑跳过这个再去看代码审计的内容了

7. 代码审计也需要MySql，所以老老实实下载一个吧

8. 安装DVW5时出现问题，访问 http://localhost/Dvwa-master 时出现404报错，明天需要完成这个内容

### 人员记录

石哥，了解到他老家是安庆的

了解到项目经理 已经结婚并且在东二十埠买了房。

### 可改进的地方

1.

2.

3.

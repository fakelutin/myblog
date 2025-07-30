+++
title: '实习记录Day3'
date: 2025-07-23T22:00:00+0000
draft = false
+++

# 实习Day3

## 预计学习任务清单：

- [x] 尝试实现Burp和Python的自动化漏洞发掘

- [x] 安装新的jdk与burpsuite

- [x] 实现对手机的拦截

- [ ] 实现hackvertor的ai使用

## 日程记录

1. 按照昨天查找的资料，参考这篇文章实现burpsuite自动化。[使用Burp Suite和Python进行自动化漏洞挖掘_burp怎么和python的代理池结合呢?-CSDN博客](https://blog.csdn.net/weixin_44556964/article/details/130515810) 。
   
   参考这个文章时的注意事项：
   
       1. 不需要查看官网 https://portswigger.net/burp/extender 的内容
   
       2. 其中Jython部分下载要下载standalone版本
   
       3. 不需要去官网下载任何Bapp Store的内容，可以直接在burpsuite内下载
   
       4. burpsuite内下载的拓展似乎没法更改扩展类型(指将Java改为Python)
   
       5. 找到了这个拓展[GitHub - modzero/mod0BurpUploadScanner: HTTP file upload scanner for Burp Proxy](https://github.com/modzero/mod0BurpUploadScanner) 作为一个jython是否安装好的检测

2. 在按照步骤走的时候，到 **开启Burp Suite REST API的默认端口**这一步出现重大问题，无法进行**点击 "Add" 按钮，选择 "Python" 作为扩展类型，然后浏览并选择 "burp-rest-api.py" 文件。此文件位于 Burp Suite 安装目录中的 "Extender" 文件夹中。单击 "Next"，然后单击 "Close"。** ,导致进度停滞。
   
   初步发现解决办法，直接找到**burp-rest-api.py** 的github下载一份即可
   [Releases · vmware/burp-rest-api · GitHub](https://github.com/vmware/burp-rest-api/releases) 
   
   解决失败，添加为拓展时出现报错如下
   
   ```bash
   java --add-opens=java.desktop/javax.swing=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED -cp "burpsuite_pro.jar;burp-rest-api-2.3.2.jar" org.springframework.boot.loader.launch.JarLauncher
   Unrecognized option: --add-opens=java.desktop/javax.swing=ALL-UNNAMED
   Error: Could not create the Java Virtual Machine.
   Error: A fatal exception has occurred. Program will exit.
   ```
   
   通过询问ai得知，似乎是因为jdk版本过低导致的，使用了电脑里遗留的jdk24重新安装，并按照这篇文章重新写了环境变量 [Burp Suite安装配置详解（附Java 环境安装）-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2105237) 
   
   现在再用就正常了

```bash
java --add-opens=java.desktop/javax.swing=ALL-UNNAMED -version
java version "24.0.1" 2025-04-15
Java(TM) SE Runtime Environment (build 24.0.1+9-30)
Java HotSpot(TM) 64-Bit Server VM (build 24.0.1+9-30, mixed mode, sharing)
```

3. 更换为新的jdk后，无法直接启动burpsuite，干脆寻找最新的burpsuite版本，参考这篇文章 https://blog.csdn.net/m0_52985087/article/details/140299827 
   
   需要下载的资源的地址：
   
   [burpsuite官网](https://portswigger.net/burp/releases) 
   
   [汉化github](https://github.com/Leon406/BurpSuiteCN-Release/releases) 
   
   [注册机阿里云盘](https://www.alipan.com/s/2ApWGFKVbi3) 提取码: 9f50（讨厌国内的云盘）
   
   按照文章指引完成安装

4. 似乎没法完成预定目标了，因为burp-reset-api.jar启动需要正确的证书信息。

5. 休息的时候看到这篇文章，跟着做了下手机的代理以及bp拦截手机
   
   [利用Burp Suite进行移动应用程序渗透测试_手机安装burp证书-CSDN博客](https://blog.csdn.net/weixin_44556964/article/details/130489161?spm=1001.2014.3001.5501) 
   
   开了拦截后手机跟我说 该网络不可上网 (XD)  
   
   记得安装证书，不然上网时一直有提示**不可信任**的弹窗

6. 放弃python，因为那个教程确实有点老了(2023年的)，索性转去试试ai的插件。参考这篇文章
   
   [Burp Suite + AI 究竟有多强？最新插件Hackvertor的使用技巧_burpsuite ai-CSDN博客](https://blog.csdn.net/weixin_43847838/article/details/146186648) 
   
   hackvertor的配置在最上方的导航栏，找半天

7. 在寻找加入hackvertor的ai的api时，意外找到了REST API，似乎就是之前卡住我做python的部分。再试试

8. 现在被代码卡住了。代码一开始运行正常，并且bp也能收到发来的包，但是放行后却又如下报错
   
   ```bash
   PS D:\burpPython> python Test1.py
   Traceback (most recent call last):
     File "D:\burpPython\Test1.py", line 32, in <module>
       task_id = response.json()['task_id']
   ```
   
   经过问询应该为api的问题，随后便在REST API中建立了新的api，并交给ai进行优化
   
   头回使用，这continue真高级吧(说7不说8，文明你我他)

9. 依旧不行，无法正常启用，问题在于api密钥并没有正确地进行认证

10. 关闭api认证，且将目标更改为我自己的服务器后，可以正常启动，启动后会在burpsuite的仪表盘界面，显示出一个爬虫程序。由于下班了，没有细看。

### 人员记录

石哥，了解到昨天的那位同龄的是合肥职业学校的

（不过u1s1，现在普高直接出来的都不如职高的，难评）

### 可改进的地方

1.

2.

3.

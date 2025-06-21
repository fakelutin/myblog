+++
title = 'MC ATM9服务器Windows端开设教程'
date = 2025-06-21
draft = false
+++


# MC ATM9 WINDOWS 开服

## 0.下载JAVA

[点击这里](https://download.oracle.com/java/24/latest/jdk-24_windows-x64_bin.exe)，跳转到ORACLE官网中下载JAVA21的WINDOWS版本

找到下载的文件，双击运行，无脑下一步即可

安装完成

## 1.获取服务器端

[点击这里进入]([Download All the Mods 9 - ATM9 - Minecraft Mods &amp; Modpacks - CurseForge](https://www.curseforge.com/minecraft/modpacks/all-the-mods-9/download/6451435))CurseForge中ATM9 客户端的下载界面

进入链接后会自动下载，大小大约为1GB，建议挂科学下载，速度会快一点

下载好后解压

## 2.初始化服务器端

双击<startserver.bat>启动windows批量处理文件，随后等待其完成工作

当出现<eula.txt>文件并提醒Crtl+C停止操作时，Crtl+C停止终端，并输入Y同意推出，岁哦胡双击该文件，并将其中第三行的<eula=false>改为<eula=true>

再次双击<startserver.bat>

等待批量处理文件操作结束

这次过程会非常长，要耐心等待，不过可以注意到，如果出现<Preparing spawn arae 0%>的字样，则说明正在进行地图生成，马上将结束操作

## 3.设置服务器选项

在服务器所在的列表中<server.properties>，右键然后以<文本文件>打开，随后进行编辑

这里只强调点的设置（ture为允许，false为不允许）

```properties
allow-flight=true //允许飞行

difficluty=hard //设置难度为困难

online-mod =false //关闭正版验证

query.port=25565 //端口开放于 25565

spawn-npcs=true //允许生成村民
```

设置好这些即可

随后再次启动<startserver.bat>，每次启动都需要加载相当的资源，请耐心等待

当出现

```bash
Dedicated server took 162.676 seconds to load
```

这种字样时，则说明开服完成，至于可能出现的

```bash
[minecraft/MinecraftServer]: Can't keep up! Is the server overloaded? Running 2370ms or 47 ticks behind
```

不需要管，只是要注意自己服务器的内存状况，该关闭的后台请注意关闭。

更多配置文件的设置的参考请[前往这里]([Minecraft 服务器server.properties属性文件介绍 (最详细 最全 汉化) - 哔哩哔哩](https://www.bilibili.com/opus/422753987430124575)) 

## 4.作为服主的一些小贴士

![](C:\Users\yihan\AppData\Roaming\marktext\images\2025-06-18-22-41-55-image.png)

在这个服务器的终端中，可以直接输入指令，比如/time set 1000等等，不过记得别给其他人权限。

此外，在终端中输入<stop>能停止服务器运行，再输入Ctrl+C能进行退出，退出时要输入Y进行确认。

<u><mark>一定别直接点击右上角退出</mark></u>，会造成存档回档甚至存档崩溃(特别强调有瓦尔基里MOD时)。



## 5.存档转移

在两个不同的主机，使用同一种整合包的服务器端时，可以通过将图中所示文件夹打包发给对方，从而实现存档的同步。

同理，想要保存存档也只需要压缩world文件夹，然后将压缩包放在你想保存的地方即可。

![](C:\Users\yihan\AppData\Roaming\marktext\images\2025-06-20-19-09-41-image.png)

## 6.内网穿透隧道

### 6.1ANTAPP(已废弃，太贵了)

NATAPP官网教程: https://natapp.cn/article/natapp_newbie

如果不适用内网穿透，那么本机所开设的服务器只能在一个局域网内被访问，因此，如果想开到公网上去，就必须使用内网穿透。

选用NATAPP进行内网穿透，[点击这里前往官网](https://natapp.cn/)

window_x64版本下载：[点击这里](https://download.natapp.cn/assets/downloads/clients/2_4_0/natapp_windows_amd64_2_4_0.zip)

下载好后，解压到一个文件夹中，随后下载配置文件：[点击这里](http://download.natapp.cn/assets/downloads/windowsconfig/config.ini) (对应windows版本)，下载好后和之前下的东西放一个文件夹里面

随后在官网中注册并登录，购买需要用的套餐，记得注意所选的<隧道协议>和<本地端口>。

由于进行的是ATM9的开服，所以隧道协议选择`TCP`和`25565`(与服务器文件server.properties中的`query.port= `一致即可)

如果没有稳定的链接的需求，可以使用免费的。

购买好套餐后，在<我的隧道>中可以看到购买的隧道，复制图中的authtoken



随后打开下载的config.ini ，如下所示的`XXXXXXX`位置，粘贴authtoken

```textile
#将本文件放置于natapp同级目录 程序将读取 [default] 段
#在命令行参数模式如 natapp -authtoken=xxx 等相同参数将会覆盖掉此配置
#命令行参数 -config= 可以指定任意config.ini文件
[default]
authtoken= XXXXXXXXXXX                    #对应一条隧道的authtoken
clienttoken=                    #对应客户端的clienttoken,将会忽略authtoken,若无请留空,
log=none                        #log 日志文件,可指定本地文件, none=不做记录,stdout=直接屏幕输出 ,默认为none
loglevel=ERROR                  #日志等级 DEBUG, INFO, WARNING, ERROR 默认为 DEBUG
http_proxy=                     #代理设置 如 http://10.123.10.10:3128 非代理上网用户请务必留空
```

保存并退出，随后运行`netapp.exe`即可开通隧道

### 6.2樱花内网穿透

参考教程: [Minecraft樱花内网穿透（Natfrp）联机教程](https://www.bilibili.com/video/BV1DdF4eJEBm/?spm_id_from=333.337.search-card.all.click&vd_source=1ea9ebc6d09911a607e42b0401057c5a) 
樱花内网穿透官网：[点击此处]([SakuraFrp 4.0](https://www.natfrp.com/user/)) 

1.登录官网并注册账户，注册完成后会跳转到一个界面，随后点击`Sakura Frp` 

2.点击图中所示的`用户`

![](C:\Users\yihan\AppData\Roaming\marktext\images\2025-06-20-20-21-42-image.png)

随后点击实名认证

![](C:\Users\yihan\AppData\Roaming\marktext\images\2025-06-20-20-22-09-image.png)

然后按照指引进行认证即可。(提示，会要求在支付宝中支付1块钱)

3.随后点击此处，前往软件下载界面，点击此处下载最新的Windows版本，下载后进行安装

![](C:\Users\yihan\AppData\Roaming\marktext\images\2025-06-20-20-24-24-image.png)

4.根据安装程序的指引，无脑下一步即可(没办法改路径)

5.返回首页，复制访问密钥

![](C:\Users\yihan\AppData\Roaming\marktext\images\2025-06-20-20-27-31-image.png)

填入`SakuraLauncher`(刚安装的程序)的`设置` 中的`访问密钥`，并登录。如果是服务器主机的话，即可开启图中的`启动器开机自启`。

![](C:\Users\yihan\AppData\Roaming\marktext\images\2025-06-20-20-29-26-image.png)

6.随后返回隧道界面，点击加号创建隧道

![](C:\Users\yihan\AppData\Roaming\marktext\images\2025-06-20-20-31-07-image.png)

选择距离所有人平均距离最近的节点，隧道类型选择TCP隧道，随后按照图中配置即可

![](C:\Users\yihan\AppData\Roaming\marktext\images\2025-06-20-20-34-50-image.png)

点击创建即可

7.点击这个以启动隧道，启动后右下角会弹出一个提醒，提示隧道启动成功

![](C:\Users\yihan\AppData\Roaming\marktext\images\2025-06-20-20-36-03-image.png)

然后查看日志中是否有`TCP隧道启动成功`的字样

![](C:\Users\yihan\AppData\Roaming\marktext\images\2025-06-20-20-37-42-image.png)

8.随后点击图中所示的链接进行复制，发给其他人，让他们加入即可

s![](C:\Users\yihan\AppData\Roaming\marktext\images\2025-06-20-20-39-58-image.png)

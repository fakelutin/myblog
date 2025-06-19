+++
title = 'MC ATM9 WINDOWS 开服'
date = 2025-06-19
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

---
title: '实习记录Day0'
date: 2025-07-21 22:00:00+0000
draft = false
---

# 实习Day1

## 预计学习任务清单：

- [x] 在WINDOWS上安装好`wechat`  `任意代码编辑工具`并连接进 `Deepseek API`

- [x] 了解并初步学习使用 `BurpSuite` 

- [x] 了解并初步学习`免杀`

## 日程记录

1. 到达公司的基层管理所在地区，并对协议进行签字，要注意有保密协议存在，同时也要记得找家里人办建行的卡，似乎有工资，但是我记得之前是说没有的，那估计是没有的，给了也不能要

2. 尝试在Fedora上安装wechat，并将deepseek接入Zed。遗憾wechat与Fedora的适配不够好，只能作罢

3. windows上没有稳定版本的Zed，只能用VScode作为工具了，查询得到`continue`与`Roo code`是可用的AI接入插件

4. （X）但是使用中`Roo code`是独立地使用费用，而不会用api官网地费用，这个不能接受

5. 简单测试了一下，就花了0.05￥,价格可以接受

6. 中午去yhc家坐会，好好寻思寻思。

7. 有错误，`Roo code`也是使用api平台地费用，显示地美元是虚假的，实际上为￥。

8. 下载BurpSuite,参考资料为 [BurpSuite v2.1（含中文版）的保姆级安装与使用]([BurpSuite v2.1（含中文版）的保姆级安装与使用_burpsuite中文版-CSDN博客](https://blog.csdn.net/m0_63100066/article/details/128355365)) 

9. 安装完成后，再根据这篇文章 [BurpSuite v2.1的使用(修改代理篇）-CSDN博客](https://blog.csdn.net/m0_63100066/article/details/122814875?spm=1001.2014.3001.5502) 按部就班地完成Zen(Firefox内核，也可以用) 中`Foxy Proxy`插件的下载与配置，并完成证书的安装与导入

10. 在`Foxy Proxy`额外配置HTTPS的代理，随后在自签证书正确的情况下可以完成对HTTPS的抓包。具体使用方面可以参考这篇文章的后半部分 [渗透测试工具Burp Suite详解-CSDN博客](https://blog.csdn.net/Waffle666/article/details/111083913) ；
    
    1. 询问ai来学习抓包的信息，内容如下：
       
       第一个包：
       
       ```http
       GET / HTTP/1.1
       Host: blog.toceo.ddns-ip.net
       User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:140.0) Gecko/20100101 Firefox/140.0
       Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
       Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
       Accept-Encoding: gzip, deflate
       Sec-GPC: 1
       Connection: close
       Upgrade-Insecure-Requests: 1
       Sec-Fetch-Dest: document
       Sec-Fetch-Mode: navigate
       Sec-Fetch-Site: none
       Sec-Fetch-User: ?1
       Priority: u=0, i
       ```
       
       GET为**请求行**，包含请求方法及路径，`/`表示根路径，`HTTP/1.1`为使用1.1版本的HTTP
       
       Host及其之后的内容为**请求头**，
       
           Host包含目标主机，一般为域名
       
           User-Agent为客户端标识，包含有浏览器，操作系统以及渲染引擎
       
           Accpet为可接受的内容类型，根据顺序划分优先级，`,` 隔开
       
           Accept-Language为语言偏好，按顺序划分优先级，`;`隔开
       
           Accept-Encoding为支持的压缩格式，即可以处理的压缩格式
       
           Sec-GPC为隐私控制，`1`表示不追踪隐私选项，`0`则表示追踪
       
           Connection为TCP连接控制，`close`表示请求后立刻关闭TCP连接，`keep-alive`表示持续连接
       
           Upgrade-Insecure-Requests为安全升级请求，`1`表示希望将`HTTP`升级为`HTTPS` 
       
           Sec-Fetch-Dest为请求目标类型，这里的`document`表示请求一个完整的HTML文档
       
           Sec-Fetch-Mode为浏览器导航请求，``navigate`` 表示导航请求，用于加载网页
       
           Sec-Fetch-Site为跨站关系，`none`表示非跨站
       
           Sec-Fetch-User为用户出发标志，`?1`表示用户主动触发，`?0`或不存在该头，则表示非用户触发，一般为脚本，比如`<img>`或者`fetch()` ，一般需要注意防范。
       
           Priority位资源优先级，`u` 代表urgency(紧急度)，数值越小优先级越高, `u=0`表示最高优先级请求，一般用于浏览器，`i`表示主文档
       
       第二个包：
       
       ```http
       GET /canonical.html HTTP/1.1
       Host: detectportal.firefox.com
       User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:140.0) Gecko/20100101 Firefox/140.0
       Accept: */*
       Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
       Accept-Encoding: gzip, deflate
       Cache-Control: no-cache
       Pragma: no-cache
       Sec-GPC: 1
       Connection: close
       ```
       
       实际上这个是Firefox 浏览器用于**强制门户检测(Captive Portal Detection)** 的机制，用于浏览器定期发送此请求检测网络是否被劫持
       detectportal.firefox.com为火狐的专用检测域名，canonical.html为检测的端点
       
       Cache-Control与Pragma都设置为`no-cache`表示禁用缓存，实现每次请求都强制从服务器获取最新的响应，并防止缓存干扰网络状态检测
       
       Accept设置为`*/*`表示不接受任何类型的响应内容
       
       Connection:设置为`close`可以保证每次都为全新的会话
       
       第三个包:
       
       ```http
       GET /success.txt?ipv6 HTTP/1.1
       Host: detectportal.firefox.com
       User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:140.0) Gecko/20100101 Firefox/140.0
       Accept: */*
       Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
       Accept-Encoding: gzip, deflate
       Sec-GPC: 1
       Connection: close
       Priority: u=4
       Pragma: no-cache
       Cache-Control: no-cache
       /*************分*************界*************线*******/
       GET /success.txt?ipv4 HTTP/1.1
       Host: detectportal.firefox.com
       User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:140.0) Gecko/20100101 Firefox/140.0
       Accept: */*
       Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
       Accept-Encoding: gzip, deflate
       Sec-GPC: 1
       Connection: close
       Priority: u=4
       Pragma: no-cache
       Cache-Control: no-cache
       ```

            这个是上面的那个包的后续，为ipv6与ipv4的检测.方式是通过发送指定的检测文件

            与上面包不同的部分：

                请求行包括检测文件/success.txt?ipv6(4)，也就是网络检测包

                Priority: u=4，低优先级

11. 了解到运维需要考证，并且信息安全专业即可。
12. 学习免杀，目前正参考该文章及其系列内容[远控免杀从入门到实践（1）：基础篇 - FreeBuf网络安全行业门户](https://www.freebuf.com/articles/system/227461.html) 
13. 注意到博主极力推荐Shellter，明日考虑查看

### 人员记录

主要工作为检测代码是否有安全漏洞，面向网络安全专业。

项目经理：程叔

员工：吴哥

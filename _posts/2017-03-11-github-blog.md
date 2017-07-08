---
layout: post  
title: "get新技能－利用github搭建个人博客"  
date: 2017-03-11 16:04:23 +0700  

---


`github` `个人博客`  

前段时间闲来无事，决定学习下怎么使用github，偶然间发现它还有搭建个人博客的功能，于是决定折腾一下，发现其实也没那么难，喜欢折腾的同学可以试一试，先附上自己的博客地址：[www.wangyingzhen.top](http://wangyingzhen.top)。
   
总结起来可以分为以下几步：  
1.注册github账号，并学会简单的使用  
2.fork一个博客模版，修改里边的配置信息  
3.上传markdown格式的博客  
4.修改个性域名  
ok,enjoy yourself!  
熟悉gthub的同学，半个小时就能搞定所有步骤，不熟悉的只有慢慢摸索咯，其实也蛮简单的。

**注册github账号**  
进入[github官网](https://github.com),填写个人邮箱，注册账号，起一个优雅的名字，easy;  
下载mac or win 版的[github desktop](https://desktop.github.com)客户端,可以在本地修改代码或博客，与网页版互传。不过大神一般都不用客户端，直接用命令行的，新手可以用客户端来过渡下；  
尝试着新建一个仓库，并上传一些文件吧。  
客户端使用说明（上传并同步文件）  
![tupian](/static/img/github.png)

**fork一个博客模版**  
可以在[jekyll模版主题](http://jekyllthemes.org)挑选喜欢的模版，也可以直接fork我的[模板](https://github.com/wangyz666)。	  
![tupian](/static/img/githubweb.png)  
点击setting改一下名称，必须是xx.github.io这种形式的，xx就是你的github账户名。（修改之后就可以用xx.github.io登录博客了，到这里就可以小小的enjoy一下了，不过网页里的东西还是别人的，需要修改成自己的。）
修改配置文件信息(如_config.yml,about.md,index.html等等)，虽然很多语法可能都不懂，不过简单的配置信息，聪明的你肯定一看就明白咯。  

**上传markdown格式的博客**  
配置文件中有一个_posts的文件夹，是用来存放博客的，要强调以下几点 
1.文件必须是markdown格式的（markdown是个什么东东可以自行百度，语法挺简单），有一堆可以编写markdown的文件，mac下推荐mou。  
2.文件必须命名为2012-08-25-hello-world.md这种模式，否则网页上无法正常显示博客。  
3.不同的模版对博客格式有不同的要求，具体可以细看下博客模版的使用说明。  
4.markdown添加本地图片的时候有些麻烦，一种是利用图床（网上有软件，使用起来比较麻烦），另外一种可以直接写图片的相对路径，如图片和博客在同一个文件夹直接(./picture.png)就可以。  
然后把写好的markdown文件放入_posts，用上面的方法同步到github上，再去刷新博客就可以看到了。  
至此，一个简单的个人博客就这样搭建完成咯，如果还想更换博客的域名就往下看咯。  

**修改个性域名**  
去网上购买一个域名，解析一下，我买的top后缀的域名，第一年只需要5块钱。  
![tupian](/static/img/ym.png)  
解析域名：在这里我们利用的是CNAME纪录方式，主机记录填www或@，也可以新增一个解析（一个填www，一个填@，这样别人在域名前加不加www都可以进入博客了），记录值就填你的博客地址：XX.github.io
最后一步，在博客的配置文件主文件夹里添加一个CNAME文件（不要任何后缀），里边写上注册的域名，我的是wangyingzhen.top 不要www也不要http）  

**搭建过程中的问题**  
新手搭建博客的时候肯定会遇到各种问题，阿杰鲁，记得查看自己的邮箱，一般的错误github都会发邮件提示你，比如这篇博客刚试了半天怎么也传不上去，后来才想到去邮箱看一下，果然github早就发邮件提示日期格式不对。  
![tupian](/static/img/p2.png)   
![tupian](/static/img/p1.png)   

**Enjoy yourself!**  
至此，一个优雅的博客就这样搭建好了，此教程针对刚入门的小白，懂web的同学可以自己编写博客模版哦,另外不同的模板可能还有许多不同功能要摸索下如何使用。

如何搭建博客是次要的，关键是要时常用博客记录自己的学习心得，分享自己的经验！  
欢迎与我交流！ 

-----
*Author*: 王英珍   
*qq*: 296085360  
*email*: wangyz666@outlook.com  
*blog*: www.wangyingzhen.top  
*github*: https://github.com/wangyz666
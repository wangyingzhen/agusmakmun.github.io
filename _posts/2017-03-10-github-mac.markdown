---
layout: post  
title:  "如何在mac上更换github账户"  
date:   2017-03-09 00:18:23 +0700  

---

`github`


对于刚刚接触github的人，想要更改mac中配置的账户是一件让人挺头疼的事。  
其实更改账户很简单，只需要按照以下步骤进行：  
1. 生成新账户的ssh key 
   
	$ ssh-keygen -t rsa -C "youremail" 
	
接下来存储key的时候最好不要使用原有的id_rsa这个名字，尽量使用一个新名字，例如id_rsa_work等；生成的id_rsa_work和id_rsa_work_pub可能不在.ssh文件夹下，去上一层找一下，mv到.ssh文件夹下。
2.把d_rsa_work_pub添加到网页版的github上

3.告诉ssh 新key的位置
  
		$ ssh-add ~/.ssh/id_rsa_work

4.在.ssh/下配置config

		$ vi .ssh/config 写入以下内容
			Host github_work
  			HostName github.com
  			IdentityFile ~/.ssh/id_rsa_work
  
  
 如果是添加一个账户，就这样写
 
 		Host github.com
  		HostName github.com
  		IdentityFile ~/.ssh/id_rsa

		Host github_work
  		HostName github.com
  		IdentityFile ~/.ssh/id_rsa_work
  		
5.测试

		ssh git@github.com
		
-------------
*Author*: 王英珍   
*qq*: 296085360  
*email*:wangyz666@outlook.com  
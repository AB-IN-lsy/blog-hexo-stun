---
title: SSH免密登录
tags:
  - SSH
  - Linux
  - Ubuntu
  - Hadoop
categories:
  - [Linux]
  - [Project]
toc: true
top: true
quicklink: true
math: true
sidebar: true
copyright: true
reward: true
photos:
  - https://oss.ab-in.cn/Pictures/ssh.png
date: 2022-01-06 22:42:27
---

{% note info %}
**摘要**
SSH免密登录原理以及实现的两种方法
{% endnote %}
<!-- more -->

<font color=#000000	size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

@[TOC](文章目录)	


# <font color=#6495ED size=6>SSH 免密登录</font>

![在这里插入图片描述](https://img-blog.csdnimg.cn/5aa0a19ede5047538fa0c3ebe55a9fe3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQl9JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


关于**免密登录**，**原理是**：

**将$A$主机的$ida\_rsa.pub$添加到$B$主机的$authorized\_keys$中，这样从$A$主机就可以免密登录$B$主机** （`ssh-copy-id`的源码基本就是这个意思）

比如我想从$wsl$登到**服务器**，那么我就先在$wsl$`ssh-keygen -t rsa`创建公钥和私钥，然后将$wsl$的公钥添加到**服务器**的$authorized\_keys$中即可，第一次填写$yes$会将公钥填写到$wsl$的$known\_hosts$中
![在这里插入图片描述](https://img-blog.csdnimg.cn/b89b489baae141909de1b21f0e948221.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQl9JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)
所以具体的操作：
* **第一种**：可以参考**原理**的操作（之前在不懂如何更快速的方法前，一直是这么配置的） 
 
 	比如在$Windows$终端，没有`ssh-copy-id`命令，那么就得手动进行配置
* **第二种**：举例：**想从$A$主机登录到$B$主机**
	* 在$A$主机中先生成公钥私钥
	 

		```bash
		ssh-keygen -t rsa
		```
	*	在~.ssh下创建$config$文件，并输入以下关于主机的信息
		* `Host`: 配置免密登录时的**别名**，比如我这里配置`AB-IN`，那么以后就可以用`ssh AB-IN` 进行登录
		* `Hostname` : 即主机公网IP地址
		* `User` : 登录进的用户
		* `Port` ：需要连接的端口（可选）
	 ![在这里插入图片描述](https://img-blog.csdnimg.cn/d39306903c454cb987e4e2e5bc0995c5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)

	* 接下来运行命令即可，命令的含义基本就是上面讲的原理，这里就可以用**别名**了，当然也可以`ssh-copy-id root@AB-IN`
	 

		```bash
		ssh-copy-id AB-IN
		```

 
	

在$Hadoop$集群操作中，$ssh$免密登录还是比较重要的
另外就是$git$了，$git$本身就是架构的$ssh$，把公钥传上去就好了，如果不传，也是要输密码的

  


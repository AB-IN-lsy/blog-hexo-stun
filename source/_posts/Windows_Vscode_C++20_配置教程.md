---
title: Windows Vscode C++17/20 配置教程
tags:
  - vscode
  - windows
  - msys2
  - mingw64
  - C++
categories:
  - [ACM]
  - [Project]
toc: true
top: true000000000000
quicklink: true
math: true
sidebar: true
copyright: true
reward: true
date: 2022-01-05 21:10:21
photos: 
  - https://oss.ab-in.cn/Pictures/g%2B%2B17.png
---
{% note info %}
**摘要**
gcc 8.1.0升级至11.2.0
{% endnote %}

<!-- more -->
<font color=#000000	size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

@[TOC](文章目录)	

$ps:$如果下到D盘，那么路径都和我一样，如果下到C盘，别忘了改路径！
# <font color=#6495ED size=6 >Windows Vscode C++17/20 配置教程</font>

## <font color=#FFA500 size=5>起因</font>

在博主打比赛时，对$map$进行$auto$的遍历操作，会导致编译警告，即$Warnning$，显示只有$c++17$可以用这个特性，但是可以编译，只是会用错误波浪线和编译警告

由于一开始不知道$gcc$版本十分旧，一直用的是$codeblocks$里自带的$mingw64$，而且也不知道$mingw$常年不更新版本，就冒然在$coderunner$中修改了命令，将$c++11$改成了$c++17$

```powershell
cd "d:\Code\Vscode\ACM\CF\2021.10.9\" ; if ($?) { g++ -std=c++17 a.cpp -o a } ; if ($?) { .\a }
```

结果：（由于博主已经配置完了，就拿$codeblocks$做个错误演示）

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-8ltJ0Yte-1633781781366)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009193659059.png)\]](https://img-blog.csdnimg.cn/aeaca3509882464f9f78d66e043fc0d1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


貌似就是$fs\_pash.h$有问题，搜了很久也没个说法

于是博主开始研究怎么升级$gcc$版本，可以使用$c++17$

* 目前$gcc$版本：$8.1.0$
* ![在这里插入图片描述](https://img-blog.csdnimg.cn/432d640344c14d439f486bd06baf90bd.png)


## <font color=#FFA500 size=5>下载MSYS2</font>

* ### <font color=#000000 size=4 face=粗体>介绍MSYS2</font>

  > 由于 MinGW 本身仅代表工具链，而在 Windows 下，由于Windows的terminal cmd窗口使用感受太差，以及配套的命令行工具不够齐全，因此，MinGW 开发者从曾经比较旧的 Cygwin 创建了一个分支，也用于提供类 Unix 环境。但与 Cygwin 的大而全不同，MSYS 是冲着小巧玲珑的目标去的，所以整套 MSYS 以及 MinGW，主要以基本的 Linux 工具为主，大小在 200M 左右，并且没有多少扩展能力。
  >
  > 由于 MinGW 万年不更新，MSYS 更是，Cygwin的许多新功能 MSYS 没有同步过来，于是 Alex 等人建立了新一代的 MSYS 项目。仍然是 fork 了 Cygwin（较新版），但有个更优秀的包管理器 pacman，有活跃的开发者跟用户组，有大量预编译的软件包（虽然肯定没有Cygwin多）

  **msys2是一款跨平台编译套件，它模拟linux编译环境，支持整合mingw32和mingw64，能很方便的在windows上对一些开源的linux工程进行编译运行。**

  

* ### <font color=#000000 size=4 face=粗体>官网下载</font>

  [MSYS2](https://www.msys2.org/)

  ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-Pu3yUK1x-1633781781372)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009192455303.png)\]](https://img-blog.csdnimg.cn/274cbebe45e7477fbfd23161b8e92108.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


  接着跟着教程走

  安装: [msys2-x86_64-20210725.exe](https://github.com/msys2/msys2-installer/releases/download/2021-07-25/msys2-x86_64-20210725.exe)

  我的安装路径为 `D:\msys64`

* ### <font color=#000000 size=4 face=粗体>安装mingw64</font>

  由于$msys2$是个工具链，我们还是要从这个编译套件中下载$mingw64$

  ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-7HG9dqBS-1633781781377)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009194452711.png)\]](https://img-blog.csdnimg.cn/4875e392eeee4a5fb45eabebb942795f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


* ### <font color=#000000 size=4 face=粗体>安装gcc gdb make</font>

  查找$gcc$，找到$win$版本的$gcc$

  ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-FCwMPNGL-1633781781380)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009194731566.png)\]](https://img-blog.csdnimg.cn/37202b9ebb9942aaa35eaf408053a2e5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


  根据自己的电脑的$OS$选择版本，这里我选择$mingw-w64-x86\_64-gcc$

  ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-KareIIVW-1633781781381)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009194853029.png)\]](https://img-blog.csdnimg.cn/3e1c8a5aada94b3dba1e7926e93ea2dc.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


  可以看到安装需要的命令

  ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-CBKZm1Jg-1633781781383)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009195103816.png)\]](https://img-blog.csdnimg.cn/03caaba10c704e9ebc4959e6ea2f6c5f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


  如果安装完成，打开$msys2$，并进行更新（如果需要换源，可以百度自行搜索）

  ```bash
  pacman -Syu --disable-download-timeout
  ```

  ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-fSzPIzB7-1633781781384)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009195201764.png)\]](https://img-blog.csdnimg.cn/f052dc99a54f4a619aa2c6c430470fc0.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


  

  之后去往安装的路径，可以看到$msys2.exe$

  ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-6aSX784l-1633781781385)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009195339471.png)\]](https://img-blog.csdnimg.cn/871b716aa19f4edba0f3a763faa779a2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


  

  打开并继续进行更新

  ```bash
  pacman -Syu --disable-download-timeout
  ```

  之后进行$gcc,gdb,make$的安装

  ```bash
  pacman -S mingw-w64-x86_64-gcc  --disable-download-timeout
  pacman -S mingw-w64-x86_64-make  --disable-download-timeout
  pacman -S mingw-w64-x86_64-gdb  --disable-download-timeout
  ```

  最后，再进行一次更新

  ```bash
  pacman -Syu --disable-download-timeout
  ```

* ### <font color=#000000 size=4 face=粗体>设置环境变量</font>

  之前大家应该都设置过，这里就不细说了

  直接将原有的路径替换为`D:\msys64\mingw64\bin`即可

## <font color=#FFA500 size=5>Vscode配置</font>

* ### <font color=#000000 size=4 face=粗体>Vscode插件</font>

	![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-IusDsG4Q-1633781781387)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009195855186.png)\]](https://img-blog.csdnimg.cn/0bd70bb8e9034b71b79d46883d78b119.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_10,color_FFFFFF,t_70,g_se,x_16)


	插件首先要配置好，这里推荐$coderunner$，自定义命令

* ### <font color=#000000 size=4 face=粗体>配置cpp</font>

  ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-AFVAbLSS-1633781781389)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009200115528.png)\]](https://img-blog.csdnimg.cn/d085ed2f159944109cce67d9b39cf17a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


* ### <font color=#000000 size=4 face=粗体>配置 coderunner</font>

  打开$settings.json$，找到$coderunner$的配置选项处

  ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-jEboD2Z1-1633781781389)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009200237900.png)\]](https://img-blog.csdnimg.cn/edca4b286af54bee8a4f4d860848198f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


  ```json
  "code-runner.executorMap": {
      "javascript": "node",
      "java": "cd $dir && javac $fileName && java $fileNameWithoutExt",
      "c": "cd $dir && gcc $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
      "cpp": "cd $dir && g++ -std=c++17 $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
      "objective-c": "cd $dir && gcc -framework Cocoa $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
      "php": "php",
      "python": "cd $dir && python -u $fileName"
  }
  ```

* ### <font color=#000000 size=4 face=粗体>配置 C/C++ IntelliSense</font>

  为了不让波浪线的出现，要设置标准

  

  ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-CRQp3Qxv-1633781781390)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009200428645.png)\]](https://img-blog.csdnimg.cn/fd18855e663c4c94a5b2d82427bb4535.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)
  即$.vscode$的文件夹中的，配置$c\_cpp\_properties.json$文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/3eab335198a947fab4946665cba01d70.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


* ### <font color=#000000 size=4 face=粗体>配置 Debug</font>

  修改本地文件夹下的$launch.json$和$task.json$

  ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-rltU99FL-1633781781390)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009200930260.png)\]](https://img-blog.csdnimg.cn/9087f53e15ab41729063ec88f1c403ea.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


  ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-kjc8RA7j-1633781781391)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009200938234.png)\]](https://img-blog.csdnimg.cn/f08342220ebb42138fa10ef285fd68d7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


大功告成



## <font color=#FFA500 size=5>效果</font>
版本$11.2.0$
![在这里插入图片描述](https://img-blog.csdnimg.cn/e44cf9059cf54fefa214b8075c500832.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)

$Vsc$编译界面
![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-xqCiD9Rh-1633781781392)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009201510630.png)\]](https://img-blog.csdnimg.cn/70e2a22e4b1e472d9c224aaed4022a71.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-9tgtJvGF-1633781781392)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20211009201537573.png)\]](https://img-blog.csdnimg.cn/3ba59b9b3b4444539f9679321fb38e3d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)

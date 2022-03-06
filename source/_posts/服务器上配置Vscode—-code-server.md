---
title: 服务器上配置Vscode
tags:
  - Vscode
  - Linux
  - Code-server
categories:
  - [ACM]
  - [Project]
toc: true
quicklink: true
math: true
sidebar: true
copyright: true
reward: true
photos:
  - https://oss.ab-in.cn/Pictures/code-server.png
date: 2022-01-06 22:37:18
---

{% note info %}
**摘要**
Code-server及配置注意事项
{% endnote %}
<!-- more -->


<font color=#000000	size=3 face=楷体>Powered by:**NEFU AB-IN**</font>


<font color=#6495ED size=5>Vscode已经出网页版啦！！！</font>
网址：[vscode.dev](https://vscode.dev/)

@[TOC](文章目录)	
# <font color=#6495ED size=6>服务器上配置Vscode</font>

大体就是这样的![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-VKpUz3IO-1630924451547)(C:\Users\liusy\Pictures\屏幕截图 2021-09-06 173943.png)\]](https://img-blog.csdnimg.cn/6da5836558404889a02acd28ba17caa5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQl9JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)


* ## 工具

  * 服务器 
  * $code-server$ [github_code-server](https://github.com/cdr/code-server)

* ## 教程

  [Code Server -- VSCODE 服务器版 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/62570740?utm_oi=41299306610688)

* ## 注意事项

  * 由于我的服务器配置比较拉，是1核2G的，所以加载可能会很慢，建议在操作的时候尽量慢点操作，安装插件和创建文件夹尽量慢一点，不然可能出现下面这个错误

    ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-vNxPPAbq-1630924451551)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20210906172001362.png)\]](https://img-blog.csdnimg.cn/2a62f87f7d17468e857a362497120fa8.png)


    $google$也查了，$github$也查了，也没给出一个河里的解释和解决办法

    我一开始以为是服务器待机长了自动退出进程，然后导致写入流断了，所以我尝试了后台运行

    

    **screen命令**，即使网络连接中断，用户也不会失去对已经打开的命令行会话的控制。
    

    ```bash
    screen -S <session name> #创建某一对话
    screen -ls #可以看到目前现有的screen的会话
    screen -r <session name> #回到某一对话
    Ctrl + a + d #返回主窗口
    ```

    我配置时打的命令

    ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-x9hMC55K-1630924451555)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20210906172618325.png)\]](https://img-blog.csdnimg.cn/fadf2f6342104e7e832fd951e081b659.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQl9JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)
	或者用**tmux**，在我的别的博客有记录，[链接](https://blog.csdn.net/qq_45859188/article/details/116903399)

  * 启动的脚本
  

	```bash
	cd ~/code-server-3.11.1-linux-amd64
	export PASSWORD="xxxxxx"
	./code-server --port 7777 --host 0.0.0.0 --auth password
	```

  * 另外还有一种方法后台运行，就是宝塔界面自带的**Supervisor管理器**
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/07ce358861874e1e9eb22f31ea649ea7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQi1JTg==,size_20,color_FFFFFF,t_70,g_se,x_16)
	 输入启动命令并进行配置即可

  * 另外想要使用$C++$，就必须有$cpptools-linux.vsix$，从服务器没法装，所以要从$github$上下载，由于$vscode$版本不是特别新，所以**千万别下最新版本的！**，一定要看清自己的$vscode$版本，下适合的[github_cpptools](https://github.com/microsoft/vscode-cpptools/releases)

  * 推荐的插件（我很常用的）

    ![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-Wwvcacqy-1630924499902)(C:\Users\liusy\AppData\Roaming\Typora\typora-user-images\image-20210906174616699.png)\]](https://img-blog.csdnimg.cn/498de183245742f4a596099508c73a9b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATkVGVSBBQl9JTg==,size_11,color_FFFFFF,t_70,g_se,x_16)


    

  * 还有账户的登录，可以登录$github$账号，同步自己的$vscode$的$ide$配置

    

* ## Settings

  记录一下我自己的$settings.json$

  在$code-runner$里的$c,c++,python$运行命令有所更改

  * $c,c++$里的$-o$前加了$-g$，这样保证它可以$Debug$
  * $python$里加上了到该目录下进行命令，在处理$csv$文件之类的时，就不用写绝对路径了，就直接在该目录下操作即可；另外没有$python$这个命令，只有$python3$

  ```json
  {
      "editor.semanticTokenColorCustomizations":{},
      "python.pythonPath": "/usr/bin/python3",
      "editor.fontSize": 18,
      "code-runner.saveFileBeforeRun": true,
      "C_Cpp.default.compilerPath": "/usr/bin/g++",
      "C_Cpp.default.cppStandard": "gnu++11",
      "C_Cpp.default.cStandard": "c11",
      "synthwave84.disableGlow": true,
      "editor.suggestSelection": "first",
      "workbench.colorTheme": "SynthWave '84",
      "code-runner.runInTerminal": true,
      "code-runner.executorMap": {
          "c": "cd $dir && gcc $fileName -g -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
          "cpp": "cd $dir && g++ -std=c++11 $fileName -g -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
          "objective-c": "cd $dir && gcc -framework Cocoa $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
          "php": "php",
          "python": "cd $dir && python3 -u $fileName",
      },
      "editor.fontFamily": "'FiraCode Nerd Font',Consolas",
      "editor.fontLigatures": true,
      "workbench.editor.untitled.hint": "hidden",
      "fileheader.cursorMode": {
          "name":"",
          "msg":"",
          "param":"",
          "return":""
      },
      "fileheader.customMade": {
          "Author":"NEFU AB_IN",
          "Date":"Do not edit",
          "FilePath":"Do not edit",
          "LastEditTime":"Do not Edit",
      },
      "fileheader.configObj": {
          "createFileTime": true,
          "language": {
              "languagetest": {
                  "head": "/$$",
                  "middle": " $ @",
                  "end": " $/"
              }
          },
          "autoAdd": true,
          "autoAddLine": 100,
          "autoAlready": true,
          "annotationStr": {
              "head": "/*",
              "middle": " * @",
              "end": " */",
              "use": false
          },
          "headInsertLine": {
              "php": 2,
              "sh": 2
          },
          "beforeAnnotation": {
              "文件后缀": "该文件后缀的头部注释之前添加某些内容"
          },
          "afterAnnotation": {
              "文件后缀": "该文件后缀的头部注释之后添加某些内容"
          },
          "specialOptions": {
              "特殊字段": "自定义比如LastEditTime/LastEditors"
          },
          "switch": {
              "newlineAddAnnotation": true
          },
          "supportAutoLanguage": [],
          "prohibitAutoAdd": [
              "json"
          ],
          "prohibitItemAutoAdd": [
              "项目的全称, 整个项目禁止自动添加头部注释, 可以使用快捷键添加"
          ],
          "moveCursor": true,
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "atSymbol": [
              "@",
              "@"
          ],
          "atSymbolObj": {
              "文件后缀": [
                  "头部注释@符号",
                  "函数注释@符号"
              ]
          },
          "colon": [
              ": ",
              ": "
          ],
          "colonObj": {
              "文件后缀": [
                  "头部注释冒号",
                  "函数注释冒号"
              ]
          },
          "filePathColon": "路径分隔符替换",
          "showErrorMessage": false,
          "writeLog": false,
          "wideSame": false,
          "wideNum": 13,
          "functionWideNum": 0,
          "CheckFileChange": false,
          "createHeader": true,
          "useWorker": false,
          "designAddHead": false,
          "headDesignName": "random",
          "headDesign": false,
          "cursorModeInternal": false
      },
      "git.enableSmartCommit": true
  }
  ```

遇到问题再更新


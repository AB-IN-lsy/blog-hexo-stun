---
title: pom.xml 配置时出错
tags:
  - pom.xml
  - web项目配置
categories:
  - [Project]
  - [Web]
toc: true
quicklink: true
math: true
sidebar: true
copyright: true
reward: true
date: 2022-05-08 21:46:36
---

{% note info %}
**错误类型**
1. This failure was cached in the local repository and resolution is not reattempted until the update interval of nexus-aliyun has elapsed or updates are forced. 
2. Could not initialize class org.apache.maven.plugin.war.util.WebappStructureSerializer
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>


@[TOC](文章目录)

# <font color=#6495ED size=6 >pom.xml 配置时出错</font>

以下恢复完错误后，**一定要 update maven**

* ## <font color=#FFA500 size=5>错误1</font>

  * ### <font size=4 face=粗体>错误</font>

    >This failure was cached in the local repository and resolution is not reattempted until the update interval of nexus-aliyun has elapsed or updates are forced.

  * ### <font size=4 face=粗体>方法1</font>
    一般是因为上次下载的库失败导致的（可能网不好）

    去自己maven库的文件夹下，打开cmd，运行这样一条语句
    ```bat
    for /r %i in (*.lastUpdated) do del %i
    ```
    目的是，循环递归删除没下好的包
  * ### <font size=4 face=粗体>方法2</font>

    如果更新完maven还没好，可能说明库中有些版本不对，建议**把库的所有包都删了**，重新保存pom.xml，重新下包


* ## <font color=#FFA500 size=5>错误2</font>

  * ### <font size=4 face=粗体>错误</font>

    >Could not initialize class org.apache.maven.plugin.war.util.WebappStructureSerializer

  * ### <font size=4 face=粗体>方法</font>
    POM中包含有maven-war-plugin插件，插件版本太低

    在插件群的标签中，加入插件即可
    ```xml
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-war-plugin</artifactId>
        <version>3.3.1</version>
    </plugin>
    ```
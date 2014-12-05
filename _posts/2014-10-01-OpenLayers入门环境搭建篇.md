---
layout: post
title: 'OpenLayers入门--环境搭建篇'
category: 文档
tags:   OpenLayers
---

#OpenLayers入门--环境搭建篇


---
开源GIS优点多，软件部署简单方便，服务发布，跨平台，无版权限制。 
下面系列文章就从零开始介绍OpenLayers+GeoServer+uDig+PostGIS系列解决方案来替代ArcGIS全线产品(ArcGIS+ArcGIS Server+ArcGIS SDE+ ArcGIS for JavaScript API)。

**GeoServer**是 OpenGIS Web 服务器规范的 J2EE 实现，利用 GeoServer 可以方便的发布地图数据，允许用户对特征数据进行更新、删除、插入操作，通过 GeoServer 可以比较容易的在用户之间迅速共享空间地理信息。兼容 WMS 和 WFS 特性；支持 PostgreSQL、 Shapefile 、 ArcSDE 、 Oracle 、 VPF 、 MySQL 、 MapInfo ；支持上百种投影；能够将网络地图输出为 jpeg 、 gif 、 png 、 SVG 、 KML 等格式；能够运行在任何基于 J2EE/Servlet 容器之上；嵌入 MapBuilder 支持 AJAX的地图客户端OpenLayers；除此之外还包括许多其他的特性。GeoServer是一个功能齐全,遵循OGC开放标准的开源WFS-T和WMS服务器。

一、下载安装JDK和Tomcat
从网上下载java的jdk和Tomcat然后安装。如果你下载的GeoServer是2.0版本以上的话就不用安装Tomcat了。只需要安装GeoServer即可

二、下载安装GeoServer
去[官网](http://geoserver.org/)上下载安装包。GeoServer的安装很简单，其中有一步是让你引导jdk的地址，不过一般它自动会找到本机所安装的jdk的地址  
![pic](http://ww3.sinaimg.cn/large/6ff04438gw1ekplq2n63cj20ea0b175f.jpg)  

![pic](http://ww1.sinaimg.cn/large/6ff04438gw1ekpls4a7mdj20e70b1mxw.jpg)  
这一步是让你选端口1024~65535皆可  
![pic](http://ww4.sinaimg.cn/large/6ff04438gw1ekpqt0s8jvj20e90b3t9l.jpg)  
Run manually为当前用户安装GeoServer，启动和停止GeoServer需手动 。Install as a service意为为所有用户安装GeoServer，GeoServer作为Windows的一个服务

##另一种安装GeoServer的方法
1. 先安装Tomcat，从[官网](http://tomcat.apache.org/)上[下载](http://tomcat.apache.org/download-80.cgi)
2. [下载GeoServer.war包](http://pan.baidu.com/s/1kTFWjxd) (提取码:ycca)
3. 放入Tomcat的webapp目录下，启动Tomcat的时候会自动运行
![pic](http://ww1.sinaimg.cn/large/6ff04438gw1ekul926twmj20ig0byjup.jpg)![pic](http://ww4.sinaimg.cn/large/6ff04438gw1ekul9fikcij20iq0l2gt3.jpg)
4. 打开浏览器输入`http://localhost:8080/GeoServer`即可  
![pic](http://ww3.sinaimg.cn/large/6ff04438gw1ekulc6dsikj20vr0ev0vf.jpg)

**注：Tomcat发布GeoServer时候内存溢出的问题**
我在用Tomcat发布GeoServer的时候遇到了内存溢出的问题，Tomcat报错`java.lang.OutOfMemoryError: Java heap space`  
网上查了很多资料，最终用以下方法解决了。
手动设置Heap size
修改`TOMCAT_HOME/bin/catalina.bat`，在`“echo "Using CATALINA_BASE: $CATALINA_BASE"”`上面加入以下行：
`set JAVA_OPTS=%JAVA_OPTS% -server -Xms800m  -Xmx800m-XX:MaxNewSize=256m`
并修改catalina.sh
在`“echo "Using CATALINA_BASE: $CATALINA_BASE"”`上面加入以下行：
`JAVA_OPTS="$JAVA_OPTS -server -Xms800m -Xmx800m -XX:MaxNewSize=256m"`  

[原因方法具体见这里](http://jayjayjays.iteye.com/blog/278854)


 三，接下来安装**uDig**(uDig是一款开源桌面GIS软件，基于Java和Eclipse平台，可以进行shp格式地图文件的编辑和查看。uDig全称 User-friendly Desktop Internet GIS)，从网上[下载](http://udig.refractions.net/files/downloads/udig-1.2.0.exe)完后双击安装即可  
 
 到此为止，基于GeoServer的地图部署环境基本搭建完成，下一篇我将详细介绍如何基于uDig进行地图数据查看、编辑以及地图样式导出等功能。

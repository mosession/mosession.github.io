---
layout: post
title: 'GeoServer发布WMSWFS服务'
category: 文档
tags: OpenLayers
---

---

在上一篇文章中，我们介绍了[OpenLayers的环境搭建](https://www.zybuluo.com/Rico/note/34373)，接下来来介绍如何使用GeoServer发布发布一份Shapefile地图数据为WMS/WFS服务。  

在GeoServer上部署地图数据非常简单，GeoServer支持的数据格式和数据源也很多，发布和部署地图数据涉及到GeoServer的几个重要知识点：工作区、数据存储和图层等概念。这一节我们部署发布的地图数据为Shapefile。  

1. 下载 [nyc_roads.zip](http://docs.geoserver.org/stable/en/user/_downloads/nyc_roads.zip) 这是GeoServer官方网站提供的一份Shapefile测试数据，包含了部分纽约的道路信息，我们本次就使用此Shapefile来进行部署和发布。

2. 解压下载好的压缩包，然后将整个文件夹复制到GeoServer数据目录的data文件夹下。![pic](http://ww4.sinaimg.cn/large/6ff04438gw1ekt4qmvxnwj20jt06vmy3.jpg)  
>GeoServer的数据目录是文件系统中的一个目录，这里存放的是GeoServer的配置信息等。这些配置信息定义了包括GeoServer提供哪些数据服务，这些数据存放在哪里以及像类似WFS和WMS等服务是如何相互影响和提供服务的。数据目录也同样包含了GeoServer所需的众多用于各种目的的支持文件。  
如果用户没有对GeoServer的文件系统进行更改的话，那复制完成后的文件目录应该是：`geoserver/data_dir/data/nyc_roads`，然后就是四个所需的Shapefile格式文件。  
3. 如果你像上一篇文章一样安装完了GeoServer之后，点击开始持续，打开GeoServer Web Admin Page
![pic](http://ww4.sinaimg.cn/large/6ff04438gw1ekt39bush2j20bf0fi0ua.jpg)  
4. 进入GeoServer的web管理页面，第一次打开的是没有登录的，请点击页面右上角的login按钮，在新开的页面输入用户名密码默认`admin/geoserver`   
5. 部署地图数据第一个步骤即为新建一个工作区，工作区（WorkSpace）是一个用于组织类似图层数据的容器。我们常常会把一些相关的图层数据放到一个工作区里。新建工作区的操作流程为：点击左侧的WorkSpace，再点击Add New WorkSpace。![pic](http://ww4.sinaimg.cn/large/6ff04438gw1ekt4bn04a9j20w10ib0vy.jpg) 进入新建工作区的界面，在这里需要输入工作区的名字和命名空间URL。![pic](http://ww4.sinaimg.cn/large/6ff04438gw1ekt4y49drwj20ci092aak.jpg)
工作区名字就是一个标志符，用来区分你的不同的项目，而命名空间URL（Uniform Resource Identifier）通常是一个与你项目有关的超链接，如果你的服务器接入了互联网，做好了相关配置与发布，那么可以在互联网上通过这个URL来访问你的数据。最后点击提交完成创建。  
根据我们要发布的Shapefile地图数据格式，我们点选Shapefile – ESRI(tm) Shapefiles (*.shp)即可。然后按照图中所示填写好相关信息。我们要注意的是工作区应该选择我们第一步建立的，Shapefile文件的位置通过浏览选择我们在准备工作中复制到数据目录下data文件夹中的Shapefile。然后数据表的字符集应该和源数据一致，如果不知道源数据的字符集，建议选择UTF-8，保证对中文系统和用户的支持。![pic](http://ww1.sinaimg.cn/large/6ff04438gw1ekt5yxgpu0j20de0gpdhe.jpg)  
最后点击保存完成创建。
6. 创建一个图层
新建数据存储后，默认会停留在新建图层的界面，我们直接在此开始建立图层。因为只有一个图层NewYorkRoads，点击Publish(发布)进入图层编辑界面(如果你当时退出了那个界面，可以点击Layers-->add new resource-->选择NewYorkRoads-->)。图层编辑界面定义了图层的数据和发布参数。填入了名称、标题、摘要等基本信息后，我们需要定义重要的SRS信息和边框信息。
&nbsp;&nbsp;&nbsp;本机SRS是指地图数据本身的坐标参考系统，这是由地图数据本身的属性决定的，也是不可修改的。GeoServer会自动从数据文件中读取这一信息。相对应的Native Bounding Box则是根据本机SRS自动计算出来的边框，我们点击从数据中计算就能计算出来边框范围。
&nbsp;&nbsp;&nbsp;定义SRS是指我们自己想要定义显示地图数据的坐标参考系统，我们通过右边的查找按钮进行查找选择。对于国内用户来说，常用的坐标系统可以通过键入“beijing”、”xian”或者4326（WGS-84的编码序号）进行查找选择。选择确定后，通过点击“compute from nativ bounds”可以计算出在这个坐标系统下的边界。
![pic](http://ww3.sinaimg.cn/large/6ff04438gw1ekt6m3ub4tj20hi0k5q4b.jpg)![pic](http://ww1.sinaimg.cn/large/6ff04438gw1ekt6o4j4akj20jf0lltbh.jpg)
最后点击保存进行发布。
##预览
点击左侧Layer Preview 按钮  
![pic](http://ww3.sinaimg.cn/large/6ff04438gw1ekt8i11zxaj20vk0aldib.jpg)   
就可以看到效果了  
![pic](http://ww4.sinaimg.cn/large/6ff04438gw1ekt8j41xktj20a00i7jsz.jpg)  

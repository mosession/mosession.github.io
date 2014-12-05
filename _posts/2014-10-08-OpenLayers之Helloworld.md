---
layout: post
title: 'OpenLayers之Helloworld'
category: 文档
tags: OpenLayers  
---

---
#准备OpenLayers
从[官网](http://openlayers.org/)上下载OpenLayers的开发包。最新版是3.0，OL的代码已经托管到了[github](https://github.com/openlayers/ol3/releases/tag/v3.0.0)上，下载解压即可。
我下的是2.13版本.  
[OpenLayers2.X官网](http://openlayers.org/two/)  
[OpenLayers2.X on github](https://github.com/openlayers/openlayers)  
[OpenLayers2.x release下载 在线api等](http://trac.osgeo.org/openlayers/wiki/HowToDownload)

下载完成之后目录结构式这样的  
![pic](http://ww4.sinaimg.cn/large/6ff04438gw1eks2cfmesjj20f90bngmw.jpg).
安装python  
完成之后打开cmd，进入到build目录  
![pic](http://ww1.sinaimg.cn/large/6ff04438gw1eks2g31lt7j20db06v74w.jpg)  
在命令行中输入`py build.py`  

![pic](http://ww3.sinaimg.cn/large/6ff04438gw1eks2hloylgj20id0lztcx.jpg)  

这时目录下会多一个OpenLayers.js的文件  
#创建第一个地图
新建一个例子文件夹，放入OpenLayers中的 theme文件夹和img文件夹和刚才生成的OpenLayers.js并新建一个index.html文件。  
![pic](http://ww4.sinaimg.cn/large/6ff04438gw1eks2owh6d9j20ez03m3yq.jpg)  
在index.html中，添加如下代码：   

```HTML
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>My OpenLayers Map</title>
<script type='text/javascript' src='OpenLayers.js'></script>
<style>  
html, body { height: 100%; width: 100%; margin: 0;} 
</style>  
<script type='text/javascript'>
var map;
function init() {
	map = new OpenLayers.Map('map'});
	var wms = new OpenLayers.Layer.WMS(
			'OpenLayers WMS',
			'http://vmap0.tiles.osgeo.org/wms/vmap0',
			{
layers: 'basic'
}
);
	map.addLayer(wms);
	if (!map.getCenter()) {
		map.zoomToMaxExtent();
	}
}
</script>
</head>
<body onload='init();'>
<div id="map" style="z-index:0;position:absolute;left:5%;top:5%;width:90%;height:90%;"></div> 
</body>
</html>

```

![pic](http://ww1.sinaimg.cn/large/6ff04438gw1eks2ya1fd1j20xd0hkjty.jpg)  

如果你之前会ArcGIS for javascript API的话，那么上面的代码相信你都能够理解。
不过本篇只是做一个Hello World的例子，详细API和代码分析后续文章会慢慢介绍。

---
参考：  
[OpenLayers2官方主页](http://openlayers.org/two/)
[OpenLayers中文API](http://www.openlayers.cn/cnapi/files/OpenLayers-js.html)  
[OpenLayers'Blog](http://blog.openlayers.org/)  
[OpenLayers'Library](http://docs.openlayers.org/library/index.html)  
[OpenLayers'Documents](http://trac.osgeo.org/openlayers/wiki/Documentation)   
[OpenLayers'Doc](http://docs.openlayers.org/)  
[OpenLayers'APIDoc](http://dev.openlayers.org/apidocs/files/OpenLayers-js.html)  
[Examples](http://dev.openlayers.org/examples/)

---
layout: post
title: 'win764位Oracle11g使用PLSQL+Developer的解决办法'
category: 文档
tags:   Oracle
---

# win764位Oracle11g使用PLSQL+Developer的解决办法



---

Oracle64位数据库如果使用plsql的话会报错，原因是oci.dll是64位的,32位应用程序PLSQL Developer无法加载。

有说再装个32位的client，其实可以不必。

1. 安装Oracle 11g 64位
 
2. 安装32位的Oracle客户端 [instantclient-basic-win32-11.2.0.1.0](http://vdisk.weibo.com/s/BR3P_2QWYWrSh)下载instantclient-basic-win32-11.2.0.1.0.zip (一定得是32位的，不要下错了版本，Oracle官网有下载），将其解压至Oracle安装目录的Product下.这时product下多了个文件夹为"instantclient_11_2"  
![pic](http://ww3.sinaimg.cn/large/6ff04438gw1ejw89a1196j20ff04xmxi.jpg)
 
拷贝数据库安装根目录下的一个目录D:\Oracle\app\Rico\product\11.2.0\dbhome_1\NETWORK到Oracle客户端目录下D:\Oracle\app\Rico\product\instantclient_11_2（其实只需要 NETWORK\ADMIN\tnsnames.ora）
 
3. 安装PL/SQL Developer
 
安装 PL/SQL Developer，在tools->perference->Connection里面设置OCI Library和Oracle_Home，例如本机设置为：  
Oracle Home ：D:\Oracle\app\Rico\product\instantclient_11_2
 
OCI Library ：D:\Oracle\app\Rico\product\instantclient_11_2\oci.dll
 ![pic](http://ww3.sinaimg.cn/large/6ff04438gw1ejw8bpcdooj20iq0e376i.jpg)
4. 设置环境变量(修改PATH和TNS_ADMIN环境变量)
对于NLS_LANG环境变量, 最好设置成和数据库端一致, 首先从数据库端查询字符集信息


 SQL> select userenv('language') nls_lang from dual;
 NLS_LANG
 SIMPLIFIED CHINESE_CHINA.ZHS16GBK  

 
右击"我的电脑" - "属性" - "高级" - "环境变量" - "系统环境变量":
 1>.选择"Path" - 点击"编辑", 把 "D:\Oracle\app\Rico\product\instantclient_11_2;" 加入;
 2>.点击"新建", 变量名设置为"TNS_ADMIN", 变量值设置为"D:\Oracle\app\Rico\product\instantclient_11_2;", 点击"确定";
 3>.点击"新建", 变量名设置为"NLS_LANG", 变量值设置为"SIMPLIFIED CHINESE_CHINA.ZHS16GBK", 点击"确定";
 最后点击"确定"退出.

启动 PL/SQL Developer ，运行无问题。

---
layout: post
title: 'Win7下安装Ubuntu双系统'
category: 文档
tags: 杂记 
---

# Windows 7 下安装 Linux 双系统

---
Linux发行版有很多,最著名的是两个分支,一个是基于Redhat和基于它的Fedora和Centos,另一个是基于Debian的Ubuntu
初学者建议先装ubuntu
##一:准备

__软件__ :Ubuntu的iso镜像(网上很多地方都可以下载到,我下载的是14.04) , EasyBCD.exe,DiskGenius.exe 安装好以上软件

__硬件分区__:在linux系统中至少必须有两个挂载点(磁盘分区)，分别是 / 及 swap ，其余是否要将其他的挂载点独立分割出来则视你的规划需求而定  　　
我的一个swap分区分了4G      　  
＂/＂分区分了40G　　
这两个硬盘需要格式化成EXT3格式，因为NTFS是MS自家搞的,Linux不识别,而在Windows7下是无法格式化成EXT3格式的,需要专门下载软件(DiskGenius.exe)来格式化  

##二:安装
其实如果把ubuntu的iso镜像解压或者虚拟光驱加载之后可以看到一个wubi.exe,用那个也可以傻瓜式的安装ubuntu,但是以这种形式安装的ubuntu相当于是虚拟机的Linux,效率不高.而网上有用U盘安装的教程，我试了，不行。这里就介绍用硬盘来安装，虽然麻烦，但是确实可行而且用一台电脑就可以了，不用U盘和光盘 。
现在就开始了!

1.  打开EasyBCD软件,点击“Add New Entry”按钮。![图片1](http://ww1.sinaimg.cn/large/6ff04438gw1eh93ouyev0j20g70dkmys.jpg)
2. 点击“NeoGrub”标签。再点击"Install"按钮。生成一个系统引导
![图片2](http://ww1.sinaimg.cn/large/6ff04438gw1eh93qnku4tj20g70dkjte.jpg)  
3. 点击“Configure”按钮 

![图片3](http://ww4.sinaimg.cn/large/6ff04438gw1eh93yvkdphj20g70dkjtd.jpg)  
弹出menu.lst文件。 
![](http://ww2.sinaimg.cn/large/6ff04438gw1eh93zumcu9j20ky0870tx.jpg)  
4. 将以下内容写入menu.lst

title Install Ubuntu  

root (hd0,1)  

kernel (hd0,1)/vmlinuz boot=casper iso-scan/filename=/ubuntu-13.04-desktop-i386.iso ro quiet splash locale=zh_CN.UTF-8  

initrd (hd0,1)/initrd.lz    

![图片4](http://ww4.sinaimg.cn/large/6ff04438gw1eh947ekgf4j20kl04ogme.jpg)
    
5. 然后保存文件

root(hd0,1)说明ubuntu.iso的安装盘在第一块硬盘的第1个分区上。（通常情况C盘是第0个分区，某些笔记本电脑有系统保留分析，所以C盘位于第1个分区）
iso-scan/filename说明ubuntu安装盘的路径。完成Ubuntu引导的配置
6. 复制Ubuntu的引导文件
在虚拟光驱上挂载ubuntu.iso，打开挂在Ubuntu的I盘，将casper目录下的initrd.lz和vmlinuz文件复制到C盘根目录下。
![图片5](http://ww4.sinaimg.cn/large/6ff04438gw1eh94hfwh2qj205c040gll.jpg)   
![图片6](http://ww3.sinaimg.cn/large/6ff04438gw1eh94jha34aj20cv07gdh2.jpg)  
7. 完成后，重启电脑， 你就会看到有2个 启动菜单给你选择 我们选择 NeoGrub 引导加载器 这个选项。  
8. 然后稍等待一段时间 就会见到我们想要安装的 Ubuntu了。  
默认 桌面有2个文档 一个是演示的不用管 我们选择 安装Ubuntu  
记得在这之前 要按Ctrl+Alt+T 打开终端，输入代码:`sudo umount -l /isodevice`这一命令取消掉对光盘所在 驱动器的挂载（注意，这里的-l是L的小写，-l 与 /isodevice 有一个空格。），否则分区界面找不到分区。![图片7](http://ww3.sinaimg.cn/large/6ff04438gw1eh9699s59gj20bb026q34.jpg)  
9. 下面就点击 安装Ubuntu 14.04开始安装。选择语言 ![图片8](http://ww1.sinaimg.cn/large/6ff04438gw1eh96aj8ez4j20g109u0sw.jpg)   
10. 选安装类型，我们用其他选项。  
这样您可以自己创建、调整分区、或者为 Ubuntu 选择多个分区。   
![图片9](http://ww1.sinaimg.cn/large/6ff04438gw1eh96c7tt4mj204i0cpaad.jpg)   
 网上有推荐分区的方案如下(以30G为例)：  
/ 20G ext4（根分区可以大点）  
SWAP 2G
/home 8G ext4（剩下的给/home）  

11. 有的说自动联网的，最好拔下网线，安装过程中会下载语言包等文件，会要一些时间，认为可以安装好后再下载，我反正有空，就联网安装吧.   
        
![图片10](http://ww2.sinaimg.cn/large/6ff04438gw1eh96dcggo1j205q0af0sx.jpg)   
12. 安装完成！ ![图片10](http://ww2.sinaimg.cn/large/6ff04438gw1eh9bhzarsej211y0lcgof.jpg)

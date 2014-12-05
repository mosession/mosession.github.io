---
layout: post
title: 'GitHub For Windows  入门'
category: 文档
tags: 教程
---

# Github For Windows入门



---

第一步：创建Github新账户  

第二步：新建一个空的仓库  

第三步：安装Github 程序，地址：http://windows.github.com/  
这时候会多出两个应用程序快捷方式  

![pic](http://ww3.sinaimg.cn/large/6ff04438gw1ejeb8wcly6j201v04q0sk.jpg)   


第四步：配置。打开Git Shell  

输入`git config --global user.name "yourusername"` 你得改成你自己的  

输入`git config --global user.email "youremailaddress"`你得改成你自己的

输入以下命令生成密钥来验证身份  
`ssh-keygen -C 'your@email.address' -t rsa`    
这里的邮箱填你注册github时的邮箱  
![pic](http://ww4.sinaimg.cn/large/6ff04438gw1ejebg8bnq2j20if07amys.jpg)
这时在windows的用户文件夹下有个.ssh文件夹，下面有这些文件  
![pic](http://ww3.sinaimg.cn/large/6ff04438gw1ejebi000fej206s041jr9.jpg)  
把文件夹下的id_rsa.pub文件内容全部复制。   
然后打开github账户设置，如图  
![pic](http://ww1.sinaimg.cn/large/6ff04438gw1ejebo96huhj20t70e2tar.jpg)  

然后在title随便输入，key栏粘贴刚才的密钥。


第五步：在Git Shell下输入命令测试刚才的公钥是否认证正确。
`ssh -T git@github.com`  
正确结果会显示：  
![pic](http://ww2.sinaimg.cn/large/6ff04438gw1ejebpu1ir8j20ii08bq41.jpg)   
第七步：clone刚才新建的repository 到本地，输入命令：  
`git clone 地址`    
地址在这里有:  
![pic](http://ww2.sinaimg.cn/large/6ff04438gw1ejebr9cmx1j205502r747.jpg)  
复制到剪切板即可  
这时会在目录下创建仓库   

![pic](http://ww4.sinaimg.cn/large/6ff04438gw1ejebtjrs8pj20ie05hwfk.jpg)  
我这里由于是克隆的已有的仓库，如果是新建的仓库，是没有内容的。（只有一个.ssh文件夹，readme，.gitignore）  

![pic](http://ww1.sinaimg.cn/large/6ff04438gw1ejebugn3gjj207h06sjre.jpg)   
第八步：随便添加一个文件，然后切换到Git shell 命令行下，输入命令：  

```javascript
git init //初始化项目，实际初始化项目的.git文件夹
git commit -m '本次提交的注释'  //现在，你的改动已经提交到了 HEAD，但是还没到你的远端仓库
git remote add origin     https://github.com/HogwartsRico/hogwartsrico.github.com.git //如果你是第一次提交项目，这一句非常重要，这是你本地的当前的项目与远程的哪个仓库建立连接。如果不是第一次提交的话这句话不用的。
git push origin master //可以把master换成想要推送的任何分支
```  

如果执行`git remote add origin https://github.com/XX/XX.git`  
出现错误：   
fatal: remote origin already exists  
则执行以下语句：   
`git remote rm origin`   
然后再git remote add origin https://github.com/XX/XX.git 即可。   

在执行`git push origin master`时，报错：   
`error:failed to push som refs to.......`
则执行以下语句：    
`git pull origin master`  
先把远程服务器github上面的文件拉先来，再push 上去。  

#学习资料
[专为设计师而写的GitHub快速入门教程](http://www.ui.cn/project.php?id=20957)  
[github学习网站](https://try.github.io/levels/1/challenges/2)  
[使用github进行团队合作](http://xiaocong.github.io/blog/2013/03/20/team-collaboration-with-github/)  
[git简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)  
[Pro Git](http://git-scm.com/book/zh)   **推荐**    
[git在知乎上的问答](http://www.zhihu.com/question/20070065)  
[如何理解git的分布式分支](http://segmentfault.com/q/1010000000609539)  
[Git 本地仓库（Repository）详解](http://freeloda.blog.51cto.com/2033581/1413506)  
[git版本管理策略](http://www.cnblogs.com/hustskyking/p/git-improve.html)  
[git101](http://mweb.baidu.com/p/git-101.html)  
[github秘籍](https://github.com/tiimgreen/github-cheat-sheet/blob/master/README.zh-cn.md)  
[gitssh捋不清的几个问题](http://www.cnblogs.com/hustskyking/p/problems-in-git-when-ssh.html)





---
title: 如何搭建Github+Hexo博客（windows版）
date: 2016-11-29 15:38:31
tags: tutorial
---

---
这篇文章主要介绍的是如何在windows上去搭建一个Github+Hexo博客。算是我自己在搭建这样一个博客的记录。不过，我本身建起来这个博客是从MAC上进行的，这部分是自己熟悉了之后又在windows上重新部署了一遍，以实现跨平台的博客更新。
<!-- more -->

利用Hexo在Github上搭建博客主要分三部分：  
1. 环境搭建，包括node.js、git和Hexo的安装和部署；  
2. github.com中gh-pages的创建；  
3. 本地新文章的创建和发布。  
下面就这三条一一讲解。

## 环境搭建
环境的搭建和部署包括有node.js、git、Hexo三部分。
#### 下载和安装node.js
node.js的下载可以在[Node.js官网](https://nodejs.org/en/)官网进行下载。不过，墙内的下载速度极其缓慢，建议GFW内的同学翻墙下载。安装的时候一路Next就可以了。不过需要注意，在安装时将nodejs和npm都加入环境变量中。安装完在cmd中输入
 
	node -version
	npm -version

可以检查版本信息。其中npm是node.js中已经包含的内容，如果缺少的话，可以通过以下命令来手动安装：  
win:

	npm install nmp -g

#### 下载和安装git
git的安装也很简单，在[Git官网](https://git-scm.com/)下载先来之后，一路Next，留意将git添加环境变量$PATH中即可。git安装完之后有git bash、git GUI和git CMD三部分。也可以用

	git --version 
来查看所安装的git的版本信息。

#### Hexo的安装与部署
Hexo的安装可以通过npm来进行。我们在适当的文件夹中创建一块用来配置Hexo的地方，我这里使用的是

	E:
	cd dandocs\blog\danxl.github.io\hexo
注意，这里的*danxl.github.io*是我的github上的仓库名，用在这里当文件夹名是为了方便识别，也可以使用别的名字。在这个文件夹中，进行Hexo安装。

	npm install hexo-cli -g
安装过程中，会有一些WARN警告，这是因为部分内容因为GFW的关系没有办法下载资源进行安装，但这并不影响使用。然后在输入

	npm install hexo --save
	npm install hexo-generator-index --save
	npm install hexo-generator-archive --save
	npm install hexo-generator-category --save
	npm install hexo-generator-tag --save
	npm install hexo-server --save
	npm install hexo-deployer-git --save
	npm install hexo-deployer-heroku --save
	npm install hexo-deployer-rsync --save
	npm install hexo-deployer-openshift --save
以及插件部分

	npm install hexo-renderer-marked@0.2 --save
	npm install hexo-renderer-stylus@0.2 --save
	npm install hexo-renderer-feed@0.2 --save
	npm install hexo-renderer-sitemap@0.2 --save
通过执行

	hexo -v
我们可以是判断我们是不是完成了Hexo的安装。 

![githubpage1](http://ohfy7y2ev.bkt.clouddn.com/T20161129153831/Article002/jpg/hexoinstalled.PNG)
 
安装结束的Hexo我们就可以进行初始化使用了。

	hexo init
	npm install
然后npm将会自动安装Hexo运行所需要的所有组件，只需静静等待即可。  
Hexo的使用方法是先生成网页

	hexo generate
然后运行

	hexo server
在浏览器中输入<http://localhost:4000>即可看到Hexo的测试页面。

![githubpage2](http://ohfy7y2ev.bkt.clouddn.com/T20161129153831/Article002/jpg/hexofirsttime.png)

以下是Hexo的一些常用指令：

	hexo server ::abv as 'hexo s'，用于启动本地服务器，默认地址为：http://localhost:4000/。
	hexo new "新文章 1" :: abv as 'hexo n "新文章 1"'，用于新建标题为“新文章 1”的文章，当标题中有空格时需要有引号，否则引号可以省略掉。
	hexo generate ::abv as 'hexo g',生成网站静态文件到默认的public文件夹中，便于查看，或者手动部署。如果自动部署则直接用 deploy即可。
	hexo deploy ::abv as 'hexo d'，自动生成网站静态文件，并部署到设定的仓库。
	hexo clean ::清楚缓存文件db.json和已经生成的静态文件public。网站显示异常时可用此命令重置。
	hexo new page aboutme ::同样new可以简写成n，此处为新建一个标题为aboutme的页面，默认地址为：主页地址/aboutme/。页面可以为中文，但一般为英文，基本可文章一样，但是不会出现在文章列表和归档中，也不支持分类和tag。
也可将多歌指令组合在一起使用

	hexo clean && hexo s
	hexo clean && hexo d
需要删掉用命令新建的文章或者页面时，只需要将hexo/source中的对应文件删掉即可。更多命令可见[官方文件](https://hexo.io/zh-cn/docs/commands.html)


## github配置
在本地安装完所需环境之后，我们来设置github上的gh-pages页面。  
注册github账号就不赘述了，与别的网站注册没有什么差别。注册完之后，我们在创建一个仓库，名为githubusername.github.io。**注意，仓库名中一定要使用github的用户名，严格一致，这样才能最后地址生效。否则的话，最后的主页名会变成githubusername.github.com/otherusername.github.io，而不是所希望的githubusername.github.io的样子。**创建的时候记得勾选上README初始化。
![githubpage3](http://ohfy7y2ev.bkt.clouddn.com/T20161129153831/Article002/jpg/githubpage1.PNG)

点击Create repository之后
在仓库页面的最右侧tag有一个setting，
![githubpage4](http://ohfy7y2ev.bkt.clouddn.com/T20161129153831/Article002/jpg/githubpage2.PNG)

进去setting之后往下翻可以找到GitHub Pages，
![githubpage5](http://ohfy7y2ev.bkt.clouddn.com/T20161129153831/Article002/jpg/githubpage3.PNG)

点击
![githubpage6](http://ohfy7y2ev.bkt.clouddn.com/T20161129153831/Article002/jpg/githubpage4.PNG)
，便可以自动生成一个Github Page。

![githubpage7](http://ohfy7y2ev.bkt.clouddn.com/T20161129153831/Article002/jpg/githubpage5.PNG)

这样，咱们的Github Pages便生成了，主页的网址也会显示在上面，即githubusername.github.io。

然后，我们在对Hexo目录下的 _config.yml进行编辑已关联账号。
找到_config.yml中的deploy部分，修改如下

	deploy:
		type: git
		repo: git@github.com:DanXL/danxl.github.io.git
		branch: master
然后执行

	npm install hexo-deployer-git --save
即可。
## 本地创建新文章并发布
本地的环境部署好，gh-page生成之后，我们就可以写博客了。
进入hexo/source中，我们所有的文章都会以.md的格式存在_post中，这里的.md会在执行指令

	hexo generate
之后被渲染。  
首先，我们创建一篇新文章，

	hexo new <filename>
如
	
	hexo new "如何搭建Github+Hexo博客"
那么，在hexo/source/_post中就会生成一个名为“如何搭建Github+Hexo博客”的.md文件，默认的Layout是post。参数Layout会在以后在详述。
![githubpage8](http://ohfy7y2ev.bkt.clouddn.com/T20161129153831/Article002/jpg/NewArticle1.PNG)

利用Markdown编辑器，对此.md文件进行编辑即可——正如我现在所做的一样。这里推荐MarkDownPad[。](http://w3cboy.com/post/2014/10/MarkdownPad%E6%B3%A8%E5%86%8C%E7%A0%81/)这是大家认为windows上最好的Markdown编辑器了。另外，也可以考虑一个私攒的[MarkDownEditor](https://github.com/chenguanzhou/MarkDownEditor/releases)，只是墙内的同学无法下载。
然后，对于编辑完的.md文件，利用指令

	hexo generate
来渲染，并生成静态文件，可供查看。再利用

	hexo deploy
来进行部署。这里手动生成了静态文件，所以也可以把public中的内容手动push到github中对应的地方，也可以完成部署。
至此，一篇文章的创建，即完成了:tada:。




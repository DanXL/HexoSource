---
title: 如何搭建Github-Hexo博客（Mac OS Sierra版）
date: 2016-12-01 13:19:56
tags:
---
前面一篇文章说了，其实我的这个博客第一遍是从我Sierra上搭建起来的，然后再跨平台时搭建了Windows 7上的版本，并写下了上一篇教程。那，其实这个两个平台搭建基本类似，只是一些指令上的差异。  
<!-- more -->

在搭建Sierra+Github+Hexo时，主要参考了[Shumin_Wu](http://www.jianshu.com/p/fd878edb95e7)的教程，基本上算是一篇很详实的搭建教程。一直也是同样的三部分： 
1. 环境搭建，包括node.js、homebrew、git和Hexo的安装和部署；
2. github.com中gh-pages的创建； 
3. 本地新文章的创建和发布。  

## 环境搭建，包括node.js、homebrew、Hexo的安装  
#### 下载node.js并安装
node.js的安装由于网络的原因，建议还是从有效途径下载安装包后，再进行本地安装，如科学上网。不推荐使用brew来安装，会被墙掉。 
成功安装后，Terminal中执行

```shell
xiaoleis-MacBook-Pro:~xiaoleidan$node -version
xiaoleis-MacBook-Pro:~xiaoleidan$npm -version
```
可以查看node.js的版本，其中npm是node.js的安装包中所集成的。
#### 下载homebrew并安装
homebrew是OSX上用来安装或者卸载软件常用的一个软件，我们可以用来安装git。可以在[homebrew官网](http://brew.sh/index_zh-cn.html)来下载Homebrew，上面的安装方法也很详实。注意此处可能需要管理员权限sudo。否则会出现安装失败的情形。 
#### 下载git并安装
git的安装其实有几种方法，可以用[Git OSX installer](https://git-scm.com/downloads)来安装，也可以通过Homebrew或者MacPorts来安装。由于墙内下载安装包困难，MacPorts又需要XCode的支持，我在这里选择了小巧而方便的Homebrew的方法。直接输入terminal指令：

```shell
xiaoleis-MacBook-Pro:~xiaoleidan$ sudo brew install git
```
即可。
这里对terminal操作不熟悉的同学，直接下载[github desktop for mac](https://central.github.com/mac/latest)就好了。
#### 下载Hexo并安装
Hexo的安装也是参考[官网文档](https://hexo.io/zh-cn/docs/)的指导，在满足的了preacquision的Git和node.js之后，只需要利用npm进行安装即可。
在使用命令进行安装时，除了系统软件，都会安装到当前路径下。hexo和npm在安装的时候有默认的文件路径，因此我们不用刻意创建文件夹。
在安装hexo的时候有可能会遇到以下错误：

```shell
{ [Error: Cannot find module './build/Release/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }  
{ [Error: Cannot find module './build/default/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }  
{ [Error: Cannot find module './build/Debug/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }  
```

这是因为不分组件被GFW挡住了，换一个源即可：


```shell
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo --no-optional
```  
hexo 安装成功后，运行

```shell
xiaoleis-MacBook-Pro:~xiaoleidan$ hexo -v
```   
检测安装是否成功。  
另外，一些hexo的组件需要单独安装的话，使用以下命令：

```shell
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo --save  
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo-generator-index --save
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo-generator-archive --save
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo-generator-category --save
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo-generator-tag --save
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo-server --save
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo-deployer-git --save
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo-deployer-heroku --save
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo-deployer-rsybc --save
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo-deployer-openshift --save
```
以及插件部分：

```shell
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo-renderer-marked@0.2 --save
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo-renderer-stylus@0.2 --save
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo-renderer-feed@0.2 --save
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install hexo-renderer-sitemap@0.2 --save
```
安装完成之后，我们就可以使用。

对于Hexo的使用，从初始化开始：

```shell
xiaoleis-MacBook-Pro:~xiaoleidan$ hexo init
xiaoleis-MacBook-Pro:~xiaoleidan$ npm install
```
需要生成网页的话，使用命令

```shell
xiaoleis-MacBook-Pro:~xiaoleidan$ hexo generate
```
然后运行

```shell
xiaoleis-MacBook-Pro:~xiaoleidan$ hexo server
```
在浏览器中输入<http://localhost:4000>即可看到Hexo的测试页面  
![hexoserver](http://ohfy7y2ev.bkt.clouddn.com/T20161201131956/Article003/jpg/HexoServer.png)  

关于hexo的一些常见命令和Windows环境下的一样，在此就不赘述了。

## Github中git-pages的创建
这里，git-pages的创建没有区分操作系统，所以和Windows系统中介绍的一致，请参考[如何搭建Github+Hexo博客（windows版）](https://danxl.github.io/2016/11/29/%E5%A6%82%E4%BD%95%E6%90%AD%E5%BB%BAGithub-Hexo%E5%8D%9A%E5%AE%A2/)。  

## 本地文章的创建并发布
环境部署完毕，gh-page设置好之后，创建文章并发布出来即可。
想要生成一篇文章，首先我们利用

```shell
xiaoleis-MacBook-Pro:hexo xiaoleidan$ hexo new MyFirstPost
xiaoleis-MacBook-Pro:hexo xiaoleidan$ hexo new "My First Post"
```
这种方式来创建名为“MyFirstPost”和“My First Post”。注意，这里第一行没有使用引号，而第二行使用了，是因为第二行中存在有空格。当没有空格时，是可以将引号省略掉的。新生成的文件会以文件名作为标题名。  
![hexonew](http://ohfy7y2ev.bkt.clouddn.com/T20161201131956/Article003/jpg/HexoNew.png)  

同样地，hexo/source中保存了我们所生成的文章，这些文章以.md的格式保存在_post中，_post是咱们写文章所采用的layout，也可以换成别的（如_page、_draft等）。这个.md文件可以使用markdown编辑器来编辑。目前我使用的编辑器是[MacDown](http://macdown.uranusjr.com/)。利用

```shell
xiaoleis-MacBook-Pro:hexo xiaoleidan$ hexo generate
```
之后被渲染成HTML格式。然后

```shell
xiaoleis-MacBook-Pro:hexo xiaoleidan$ hexo deploy
```
来部署。这里手动生成了静态文件，所以也可以把public中的文件，推送到github对应的位置中。注意，不好包含public文件，只推送里面的文件即可。

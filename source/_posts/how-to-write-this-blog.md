---
title: how_to_write_this_blog
date: 2020-02-09 17:41:14
tags:
---

# 方案

部署个人博客的方案有很多，可以直接在博客园、CSDN上注册即用，也可使用WordPress搭建自主性更强的个人站点。对于程序员而言，GitHub Pages提供的博客方案则是一个很好的折中选择，既没有博客网站那么简单，也不需要WordPress这么高的资源投入。

基于GitHub Pages部署一个基本博客页面还是非常简单的，基本上5分钟完成。网上教程很多，这里文字简单描述下步骤：

1. 注册github账号；
2. 新建名称为xxx.github.io的repository；
3. 选择jkelly主题；

实际上到第二步时就可以登录xxx.github.io访问你的个人博客了，只是这时的博客只显示简单的文本。执行第三步后，才可以借助jkelly得到渲染后的html页面。

那接下来该如何添加我们自己的文章，甚至是评论区、浏览计数等等功能呢？

我们知道前面的简单页面是借助于github在线的jkelly转换功能，直接转换README.md文件得到的。通过修改提交README.md文件测试可以发现 ，经过几分钟延时，个人博客中就可以得到修改后的结果。

那可以通过编辑README.md文件完成博客编辑吗 。。。如果你的博客就一个文件，而且愿意用github里仅有的几个模板，不想折腾了，那也行。

GitHub Pages本质上是一个静态网站服务器，毕竟免费的，直接呈现静态网页资源负担小。所以使用GitHub Pages做博客网站一个最直接的方式就是直接写html文件。我们可以上传index.html 文件，这样访问博客时，系统便直接呈现该index，而不会再去解析README.md文件。

我们有很多方法可以得到index.html 文件，可以手写，更方便的是使用现成的框架，比如：[aopstudio.github.io](https://github.com/aopstudio/aopstudio.github.io)和[gh-pages](https://github.com/woshidandan/xiaohe/tree/gh-pages)。

使用现成的框架可玩性更高，但也相对复杂。虽然我们只需要在框架中手写一些接口页面，博客内容可以采用markdown编写后，使用docsify转换为html页面的方式降低博客协作难度，比如[基于Github Pages + docsify](https://segmentfault.com/a/1190000021494556)、[使用docsify并定制以使它更强大](https://www.cnblogs.com/aopstudio/p/10732512.html)中描述的方式。

作为后来者，我们其实已经有了更好的选择，那就是GitHub Pages提供的jkelly方案，或者hexo方案 。

jkelly和hexo均支持一次配置完成后，使用markdown编辑博客内容的方式。不同点在于jeklly的本地开发环境 配置比较麻烦，虽然GitHub Pages提供了在线生成网页，通常无需配置本地jkelly环境，即便是基于jkelly模板的开发，也可以直接提交jkelly源文件，由GitHub Pages在线完成html文件转化。但是如果想修改网页后本地预览效果，本地开发环境还是很有必要的。而且jkelly不管啥文件都直接在线自动转换了，也不便于区分草稿和正式版本。关于jkelly的使用可以参考[Creating and Hosting a Personal Site on GitHub](http://jmcglone.com/guides/github-pages/)。

考虑到jkelly开发环境的部署难度，碰巧又在[hexo模板](https://hexo.io/themes/)中看到了一个喜欢的[三栏式布局](https://yelog.org/)，最终就决定使用hexo了。

跟jkelly类似，hexo也是一个将markdown转换为静态网页的工具，不同点在于GitHub Pages内置了jkelly开发环境，我们直接上传jkelly源码即可。hexo没有GitHub Pages在线解析的支持，我们需要本地完成解析转换后，直接将得到的html页面归档至GitHub Pages中。好处是hexo是基于node.js的，开发环境相当友好。

接下来我们就部署hexo，具体看看。

# 搭建


使用淘宝NPM镜像(http://npm.taobao.org) 
$ npm install -g cnpm --registry=https://registry.npm.taobao.org



操作如下：

1. 安装 Node.js前往 https://nodejs.org/en/点击 8.9.1 LTS 下载安装打开 Command Prompt， 输入 node -v得到：v8.9.1安装成功
2. 安装 Git前往 https://git-scm.com/点击 Downloads点击 Windows一般情况，下载会自动开始。如果没有，就点击 click here to download manually安装打开 Command Prompt， 输入 git --version得到：git version 2.15.0.windows.1安装成功额外说明：如果 Git –version 指令不管用，可能需要到 Environment Variable 那里添加 Path。
3. 安装 Hexo打开 Command Prompt输入 npm install -g hexo-cli回车开始安装输入 hexo -v得到 hexo-cli: 1.0.4 等一串数据安装成功
4. 创建本地博客在D盘下创建文件夹 blog鼠标右键 blog，选择 Git Bash Here。 如果没有安装 Git，就不会有这个选项。Git Bash 打开之后，所在的位置就是 blog 这个文件夹的位置。（/d/blog）输入 hexo init 将 blog 文件夹初始化成一个博客文件夹。输入 npm install 安装依赖包。输入 hexo g 生成（generate）网页。 由于我们还没创建任何博客，生成的网页会展示 Hexo 里面自带了一个 Hello World 的博客。输入 hexo s 将生成的网页放在了本地服务器（server）。浏览器里输入 http://localhost:4000/ 。 就可以看到刚才的成果了。回到 Git Bash，按 Ctrl+C 结束。此时再看 http://localhost:4000/ 就是无法访问了。



参考https://www.jianshu.com/p/0b1fccce74e0归档hexo博客源文件。

在没有原始文件的电脑上修改
拉hexo分支的原始代码到本地
git clone ...
1
下载npm包(需要有node环境)
npm install hexo
npm install
npm install hexo-deployer-git

.gitignore文件中可见
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
这些问价和编译无关，不用提交。以后如果遇到包的 版本变更频繁 ，也可以考虑提交归档自己用对的 。

# 使用

提交markdown文件，只要不编译就不会出现在博客中。

# 完善

## 更换主题

可在[hexo主题](https://hexo.io/themes/)站点选择自己喜欢的主题，比如：[三栏式布局](https://github.com/yelog/hexo-theme-3-hexo)。 





主要参考资料 

 https://www.jianshu.com/p/1c888a6b8297?utm_source=oschina-app 

 https://hexo.io/zh-cn/docs/ 

 https://www.zhihu.com/question/59088760 

 https://www.jianshu.com/p/0b1fccce74e0 

 https://blog.csdn.net/qq_33429968/article/details/62219783 
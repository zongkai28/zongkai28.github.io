---
title: how_to_write_this_blog
date: 2020-02-09 17:41:14
tags:
---

# 方案

部署个人博客的方案有很多，可以直接在博客园、CSDN上注册即用，也可使用WordPress搭建自主性更强的个人站点。对于程序员而言，GitHub Pages提供的博客方案则是一个很好的折中选择，既没有博客网站那么简单，也不需要WordPress这么高的资源投入。

基于GitHub Pages部署一个基本博客页面还是非常简单的，基本上5分钟完成。网上教程很多，这里文字简单描述下步骤：

> 1. 注册github账号；
> 2. 新建名称为xxx.github.io的repository；
> 3. 选择jkelly主题；
>

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

![](.\img\hexo_on_github pages.jpg)

跟jkelly类似，hexo也是一个将markdown转换为静态网页的工具，不同点在于GitHub Pages内置了jkelly开发环境，我们直接上传jkelly源码即可。hexo没有GitHub Pages在线解析的支持，我们需要本地完成解析转换后，直接将得到的html页面归档至GitHub Pages中。好处是hexo是基于node.js的，开发环境相当友好。

接下来我们就部署hexo，具体看看。

# 搭建


 安装 Hexo 只需几分钟时间，有较多教程可以参考，推荐参考 [hexo官网教程]( https://hexo.io/zh-cn/docs/ )和 [hexo——轻量、简易、高逼格的博客]( https://www.jianshu.com/p/1c888a6b8297?utm_source=oschina-app )。

安装hexo步骤如下：

1. **安装 Node.js**

> - 前往 https://nodejs.org/en/，点击`8.9.1 LTS`下载；
> - 安装；
> - 打开`Command Prompt`，输入`node -v`，得到：`v8.9.1`，表明安装成功；
>

2. **安装 Git**

> - 前往 https://git-scm.com/，点击 Downloads，点击 Windows下载；
> - 安装；
> - 打开`Command Prompt`， 输入`git --version`得到：`git version 2.15.0.windows.1`，表明安装成功；
>

3. **使用淘宝NPM镜像**

- > 执行`$ npm install -g cnpm --registry=https://registry.npm.taobao.org`，切换为淘宝镜像。后续的`npm`指令替换为`cnpm`指令，可加快下载速度。

4. **安装 Hexo**

> - 打开`Command Prompt`输入`npm install -g hexo-cli`，回车开始安装；
> - 输入`hexo -v`得到`hexo-cli: 1.0.4`等一串数据表示安装成功；
>

5. **创建本地博客测试安装**

> - 在D盘下创建文件夹 blog；
> - 打开`Command Prompt`切换至blog目录；
> - 输入`hexo init`将 blog 文件夹初始化成一个博客文件夹；
> - 输入`npm install`安装依赖包；
> - 输入`hexo g`生成网页。由于我们还没创建任何博客，生成的网页会展示 Hexo 里面自带了一个 Hello World 的博客；
> - 输入`hexo s`将生成的网页放在了本地服务器；
> - 浏览器里输入 http://localhost:4000/ 就可以看到Hello World博客；
> - 回到`Command Prompt`，按`Ctrl+C`结束。此时再看`http://localhost:4000/`就无法访问了。
>

6. **发布一篇博客**

> - 继续在`Command Prompt`里，输入 `hexo new "My First Post"`；
>
> - 在`.\blog\source_posts`路径下，会有一个`My-First-Post.md`的文件。 编辑该文件后保存。
>
> - 回到`Command Prompt`，输入`hexo g`和`hexo s`后，即可在`http://localhost:4000`查看成果。
>

# 使用

## **将本地博客部署在Github上**

经过前面步骤，我们已经有了本地博客。只要把本地博客部署（deploy）到Github.io对应的Repository中就可以供其他人访问了。

1. **获取 Github 对应的 Repository 的链接。**

> - 登陆 Github，进入到名称为`xxx.github.io`的Repository中；
> - 复制URL备用；
>

2. **修改博客的配置文件**

- > 打开本地博客配置文件`./blog/_config.yml`，找到`#Deployment`，填入以下内容：

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repository: 前面一步得到的xxx.github.io的Repository地址
  branch: master
```

3. **部署**

> - 打开`Command Prompt`切换至blog目录；
> - 输入`npm install hexo-deployer-git --save`安装hexo-deployer-git，此步骤只需要做一次。
> - 输入`hexo d`，得到`INFO Deploy done: git`即为部署成功。原来Repository中的文件会被自动覆盖；
>

4. **查看成果**

- > 前往博客地址http://xxx.github.io即可访问。
  >

## 归档hexo源文件

前面转换完成的hexo网页已经推送保存至Repository对应的master分支了，那本地的hexo源文件是否也可以保存在github中呢，可以参考[利用Hexo在多台电脑上提交和更新github pages博客](https://www.jianshu.com/p/0b1fccce74e0)中的描述完成hexo源文件归档。

1. **在github io博客Repository中创建`hexo_source`分支；**
2. **clone创建的`hexo_source`分支到本地，并删除全部文件后提交，确保`hexo_source`分支目录为空；**
3. **将前面的hexo源码拷贝至本地`hexo_source`分支目录中；**
4. **打开`Command Prompt`切换至`hexo_source`分支目录，执行`hexo clean`、`git add .`、`git commit -m '提交说明'`、`git push`即可将博客hexo源码归档至github的`hexo_source`分支中 ；**

从`.gitignore`文件中可见如下文件和编译无关，不用提交。以后如果遇到包的版本变更频繁，也可以考虑提交node_modules/归档。

```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
```

## 更换电脑编辑 

在github上编辑博客的最显著的一个优势是可以充分利用git，数据保存在云端，替换电脑后也可以随时编辑博客。那如何在替换电脑时继续编辑呢？可以参照如下步骤：

1. **确认电脑上已有node和git环境。node安装非常简单，这是我们选择hexo，而不是jkelly的初衷；**
2. **拉取github io博客Repository中的`hexo_source`分支到本地；**
3. **打开`Command Prompt`，切换至`hexo_source`分支目录，执行如下命令下载必要的npm包后，就可以正常开展博客编辑和部署工作了；**

> - npm install hexo
>- npm install hexo-deployer-git
> - npm install
>

## 编辑草稿

提交markdown文件，只要不编译就不会出现在博客中。

# 完善

## 显示图片

 安装图片插件

 npm install hexo-asset-image --save 

 在_config.yml配置文件中，修改为 post_asset_folder: true， 然后新建一篇文章 

## 更换主题

可在[hexo主题](https://hexo.io/themes/)站点选择自己喜欢的主题，比如：[三栏式布局](https://github.com/yelog/hexo-theme-3-hexo)。 

这里以该三栏式布局主题为例，详细步骤如下，大概思路是把整个主题的文件克隆到我们博客的主题文件夹中，在配置文件中注明使用该主题。

获取主题。 

输入** `git clone https://github.com/iissnan/hexo-theme-next themes/next`

这样，该主题的文件就全部克隆到 D:\blog\themes\next 下面。

**2. 修改博客配置文件**

- 打开 D:\blog_config.yml
- 找到 `theme:`
- 把 Hexo 默认的 lanscape 修改成 next。 即 `theme: next`
- 找到 `# Site`，添加博客名称，作者名字等。
- 在 `language` 后面填入 en 或者 zh-Hans，选择英文或者中文。
- 找到 `# URL`, 填入 url。比如 `url: https://ryanluoxu.github.io`

填入名字后会有很风骚的 © 2017 Ryan Luo Xu 的字样出现在博客底部。



**3. 重新生成部署即可**

- 回到 Git Bash。输入 `hexo g -d`就可以了。

先把修改的内容生成网页，再部署。



**4. 查看成果**

前往 [http://ryanluoxu.github.io](https://link.zhihu.com/?target=http%3A//ryanluoxu.github.io) 即可。





主要参考资料 

 https://www.jianshu.com/p/1c888a6b8297?utm_source=oschina-app 

 https://www.jianshu.com/p/0b1fccce74e0 

 https://blog.csdn.net/qq_33429968/article/details/62219783 
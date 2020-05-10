---
title: 如何在`github pages`上部署个人博客
date: 2020-02-13 05:58:04
categories:
- 工具
tags:
- hexo
---

# 方案

部署个人博客的方案有很多，可以直接在博客园、`CSDN`上注册即用，也可使用`WordPress`搭建自主性更强的个人站点。对于程序员而言，`GitHub Pages`提供的博客方案则是一个很好的折中选择，既没有博客网站那么简单，也不需要`WordPress`这么高的资源投入。

基于`GitHub Pages`部署一个基本博客页面还是非常简单的，基本上5分钟完成。网上教程很多，这里文字简单描述下步骤：

> 1. 注册`github`账号；
> 2. 新建名称为`xxx.github.io`的`repository`；
> 3. 选择`jkelly`主题；

实际上到第二步时就可以登录`xxx.github.io`访问你的个人博客了，只是这时的博客只显示简单的文本。执行第三步后，才可以借助`jkelly`得到渲染后的`html`页面。

那接下来该如何添加我们自己的文章，甚至是评论区、浏览计数等等功能呢？

我们知道前面的简单页面是借助于`github`在线的`jkelly`转换功能，直接转换`README.md`文件得到的。通过修改提交`README.md`文件测试可以发现 ，经过几分钟延时，个人博客中就可以得到修改后的结果。

那可以通过编辑`README.md`文件完成博客编辑吗 。。。如果你的博客就一个文件，而且愿意用`github`里仅有的几个模板，不想折腾了，那也行。

`GitHub Pages`本质上是一个静态网站服务器，毕竟免费的，直接呈现静态网页资源负担小。所以使用`GitHub Pages`做博客网站一个最直接的方式就是直接写`html`文件。我们可以上传`index.html` 文件，这样访问博客时，系统便直接呈现该`index`，而不会再去解析`README.md`文件。

我们有很多方法可以得到`index.html`文件，可以手写，更方便的是使用现成的框架，比如：[aopstudio.github.io](https://github.com/aopstudio/aopstudio.github.io)和[gh-pages](https://github.com/woshidandan/xiaohe/tree/gh-pages)。

使用现成的框架可玩性更高，但也相对复杂。虽然我们只需要在框架中手写一些接口页面，博客内容可以采用`markdown`编写后，使用`docsify`转换为`html`页面的方式降低博客协作难度，比如[基于Github Pages + docsify](https://segmentfault.com/a/1190000021494556)、[使用docsify并定制以使它更强大](https://www.cnblogs.com/aopstudio/p/10732512.html)中描述的方式。

作为后来者，我们其实已经有了更好的选择，那就是`GitHub Pages`提供的`jkelly`方案，或者`hexo`方案 。

`jkelly`和`hexo`均支持一次配置完成后，使用`markdown`编辑博客内容的方式。不同点在于`jeklly`的本地开发环境配置比较麻烦，虽然`GitHub Pages`提供了在线生成网页，通常无需配置本地`jkelly`环境，即便是基于`jkelly`模板的开发，也可以直接提交`jkelly`源文件，由`GitHub Pages`在线完成`html`文件转化。但是如果想修改网页后本地预览效果，本地开发环境还是很有必要的。而且`jkelly`不管啥文件都直接在线自动转换了，也不便于区分草稿和正式版本。关于`jkelly`的使用可以参考[Creating and Hosting a Personal Site on GitHub](http://jmcglone.com/guides/github-pages/)。

考虑到`jkelly`开发环境的部署难度，碰巧又在[hexo模板](https://hexo.io/themes/)中看到了一个喜欢的[三栏式布局](https://yelog.org/)，最终就决定使用`hexo`了。

![](how-to-write-this-blog/hexo_on_github_pages.png)

跟`jkelly`类似，`hexo`也是一个将`markdown`转换为静态网页的工具，不同点在于`GitHub Pages`内置了`jkelly`开发环境，我们直接上传`jkelly`源码即可。`hexo`没有`GitHub Pages`在线解析的支持，我们需要本地完成解析转换后，直接将得到的`html`页面归档至`GitHub Pages`中。好处是`hexo`是基于`node.js`的，开发环境相当友好。

接下来我们就部署`hexo`，具体看看。

# 搭建


 安装`Hexo`只需几分钟时间，有较多教程可以参考，推荐参考 [hexo官网教程]( https://hexo.io/zh-cn/docs/ )和 [hexo——轻量、简易、高逼格的博客]( https://www.jianshu.com/p/1c888a6b8297?utm_source=oschina-app )。

安装`hexo`步骤如下：

1. **安装`Node.js`**

> - 前往 https://nodejs.org/en/，点击`12.16.1 LTS`或当前推荐的LTS版本下载；
> - 安装；
> - 打开`Command Prompt`，输入`node -v`，得到：`v12.16.1`，表明安装成功；

2. **安装`Git`**

> - 前往 https://git-scm.com/，点击`Downloads`，点击`Windows`下载；
> - 安装；
> - 打开`Command Prompt`， 输入`git --version`得到：`git version 2.15.0.windows.1`，表明安装成功；

3. **使用淘宝NPM镜像**

> - 执行`$ npm install -g cnpm --registry=https://registry.npm.taobao.org`，切换为淘宝镜像。后续的`npm`指令替换为`cnpm`指令，可加快下载速度。

4. **安装`Hexo`**

> - 打开`Command Prompt`输入`npm install -g hexo-cli`，回车开始安装；
> - 输入`hexo -v`得到`hexo-cli: 3.1.0`等一串数据表示安装成功；

5. **创建本地博客测试安装**

> - 在D盘下创建文件夹`blog`；
> - 打开`Command Prompt`切换至`blog`目录；
> - 输入`hexo init`将`blog`文件夹初始化成一个博客文件夹；
> - 输入`npm install`安装依赖包；
> - 输入`hexo g`生成网页。由于我们还没创建任何博客，生成的网页会展示`Hexo`里面自带了一个`Hello World`的博客；
> - 输入`hexo s`将生成的网页放在了本地服务器；
> - 浏览器里输入 http://localhost:4000/ 就可以看到`Hello World`博客；
> - 回到`Command Prompt`，按`Ctrl+C`结束。此时再看`http://localhost:4000/`就无法访问了。

6. **发布一篇博客**

> - 继续在`Command Prompt`里，输入 `hexo new "My First Post"`；
> - 在`.\blog\source_posts`路径下，会有一个`My-First-Post.md`的文件。 编辑该文件后保存。
> - 回到`Command Prompt`，输入`hexo g`和`hexo s`后，即可在`http://localhost:4000`查看成果。

# 使用

## **将本地博客部署在`Github`上**

经过前面步骤，我们已经有了本地博客。只要把本地博客部署（`deploy`）到Github.io对应的Repository中就可以供其他人访问了。

1. **获取`Github`对应的`Repository`的链接。**

> - 登陆`Github`，进入到名称为`xxx.github.io`的`Repository`中；
> - 复制URL备用；

2. **修改博客的配置文件**

> - 打开本地博客配置文件`./blog/_config.yml`，找到`#Deployment`，填入以下内容：

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

4. **查看成果**

> - 前往博客地址http://xxx.github.io即可访问。

## 归档`hexo`源文件

前面转换完成的`hexo`网页已经推送保存至`Repository`对应的`master`分支了，那本地的`hexo`源文件是否也可以保存在`github`中呢，可以参考[利用Hexo在多台电脑上提交和更新github pages博客](https://www.jianshu.com/p/0b1fccce74e0)中的描述完成`hexo`源文件归档。

> 1. 在`github io`博客`Repository`中创建`hexo_source`分支；
> 2. `clone`创建的`hexo_source`分支到本地，并删除全部文件后提交，确保`hexo_source`分支目录为空；
> 3. 将前面的`hexo`源码拷贝至本地`hexo_source`分支目录中；
> 4. 打开`Command Prompt`切换至`hexo_source`分支目录，执行`hexo clean`、`git add .`、`git commit -m '提交说明'`、`git push`即可将博客hexo源码归档至github的`hexo_source`分支中 ；

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

在`github`上编辑博客的最显著的一个优势是可以充分利用`git`，数据保存在云端，替换电脑后也可以随时编辑博客。那如何在替换电脑时继续编辑呢？可以参照如下步骤：

> 1. 确认电脑上已有`node`和`git`环境。`node`安装非常简单，这是我们选择`hexo`，而不是`jkelly`的初衷；
> 2. 拉取`github io`博客`Repository`中的`hexo_source`分支到本地；
> 3. 打开`Command Prompt`，输入`npm install -g hexo-cli`，安装`hexo`命令行工具；
> 4. 切换至`hexo_source`分支目录，执行`npm install`命令即可下载必要的npm包后，正常开展博客编辑和部署工作了。因为`hexo`依赖的包都记录在`package.json`文件中了，`npm install`命令可直接根据列表安装所需要的包；
> 5. 执行`hexo g`编译网页，执行`hexo s`本地预览，执行`hexo d`推送部署；
> 6. 执行`hexo clean`后清除缓存文件，即可将源文件归档至`github`；

## 编辑草稿

我们已经知道`hexo`实际上是一款将`markdown`转换为`html`的工具，所以如果刚开始编写一篇文章，并且编辑多次后才提交可以采用如下工作方式。

> 1. 打开`Command Prompt`，切换至拉取的博客`Repository`中的`hexo_source`分支；
> 2. 执行`hexo new draft`创建待编辑文章，编辑完成后`commit`至本地'Repository'，或`push`至`github`。该步骤可多次执行直到文章编辑完成；
> 3. 执行`hexo d`发表博客;

# 完善

## 显示图片

 测试后会发现，使用`markdown`传统方式添加的图片是无法正常在网页端显示的，这是因为`hexo`无法正确的将本地图片路径转换为网页文件中的格式。这是我们就需要借助`hexo-asset-image`工具完成文件路径的转换，步骤如下：

1. **打开`Command Prompt`执行如下命令安装图片路径转换工具`hexo-asset-image`。注意我们并未使用官方推荐的方式`npm install hexo-asset-image --save`，实测发现官方包有问题，无法显示图片。网上有仓库解决了该问` https://github.com/xcodebuild/hexo-asset-image`，为了避免该库后续变化，我已fork至自己账户中 。执行完该命令后会在包列表`package.json`中添加相关信息，换电脑或重新下载后只要执行`npm install`即可。**

> - `npm install https://github.com/zongkai28/hexo-asset-image --save`

2.  **在`config.yml`配置文件中的`post_asset_folder`属性修改为`true`.**

3. **使用`hexo new post test`命令新建一篇文章，可以发现在`_post`目录下同时出现了`test.md`文件和`test`文件夹，此时在`test.md`中使用`![](test/test.jpg)`即可在`markdown`和`html`中均正常显示图片。**

## 更换主题

可在[hexo主题](https://hexo.io/themes/)站点选择自己喜欢的主题，比如：[三栏式布局](https://github.com/yelog/hexo-theme-3-hexo)。 

这里以该三栏式布局主题为例，详细步骤如下，大概思路是把整个主题的文件克隆到我们博客的主题文件夹中，在配置文件中注明使用该主题。

1. **打开`Command Prompt`切换至拉取的博客`Repository`中的`hexo_source`分支的themes目录，执行如下命令获取主题。** 

> - `git clone https://github.com/iissnan/hexo-theme-next themes/next`

**2. 修改博客配置文件`_config.yml`。**

> - 修改 `theme:`，把`hexo`默认的`lanscape`修改成`next`，即`theme: next`；
> - 修改 `# Site`，添加博客名称，作者名字等。修改`language`，填入英文`en`或者中文`zh-Hans`;
> - 修改`# URL`，填入自己的博客地址，比如 `url: https://xxx.github.io`

**3. 重新生成部署即可**

> - 回到`Git Bash`，输入`hexo g`，之后输入`hexo s`本地测试，或`hexo d`直接部署。

**4. 前往你的博客地址`http://xxx.github.io`查看成果**

# 主要参考资料 

- [hexo——轻量、简易、高逼格的博客](https://www.jianshu.com/p/1c888a6b8297?utm_source=oschina-app)
- [利用Hexo在多台电脑上提交和更新github pages博客](https://www.jianshu.com/p/0b1fccce74e0) 
---
title: how_to_write_this_blog
date: 2020-02-09 17:41:14
tags:
---



正常来说，不需要部署到我们的服务器上，我们的服务器上保存的，其实是基于在hexo通过markdown编写的文章，然后hexo帮我们生成静态的html页面，然后，将生成的html上传到我们的服务器。简而言之：hexo是个静态页面生成、上传的工具

参考https://www.zhihu.com/question/59088760，使用hexo
https://www.jianshu.com/p/1c888a6b8297?utm_source=oschina-app


教程 
https://www.jianshu.com/p/1c888a6b8297?utm_source=oschina-app
https://hexo.io/zh-cn/docs/
https://www.zhihu.com/question/59088760


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

我们有很多方法可以得到index.html 文件，可以手写，也可以借助于现成的框架，比如：https://github.com/aopstudio/aopstudio.github.io和https://github.com/woshidandan/xiaohe/tree/gh-pages。

或者也可以使用工具得到，

配置页面的选择顺序：
项目根目录的index.html > 选择的主题 > README.md文件



本地预览 jeklly比较麻烦。


github自带的jkelly较为简单，只能自动渲染readme.md文件

离线使用jkelly编译网页并且推送到git上，需要配置本地jkelly编译环境，将md转换为静态网页。

参考https://www.jianshu.com/p/53ad32e07dd3，有可能可以手动编辑_config.yml修改github上默认的jkelly配置。
但这样做 较为复杂，而且不知道 可行性。

jkellly是有自己固定的格式的 ，如下，http://jmcglone.com/guides/github-pages/里也有提到，这种手工修改方式可能也无法支持这样的复杂格式。

_posts 博客内容
_pages 其他需要生成的网页，如About页
_layouts 网页排版模板
_includes 被模板包含的HTML片段，可在_config.yml中修改位置
assets 辅助资源 css布局 js脚本 图片等
_data 动态数据
_sites 最终生成的静态网页
_config.yml 网站的一些配置信息
index.html 网站的入口


使用jkelly还存在草稿难以本地预览效果和草稿切换为正式版本的麻烦。

但jekyll貌似配置完成后，也可以不用本地编译，直接上传也行。即便是这样的话，除非有一个很好的模板 ，自己啥都不用改 ，如果稍微想调整点东西，都需要 
自己在线看效果，就很麻烦。所以虽然配置的环境只用一次，但也还是麻烦，除非有现成的docker可以用。
https://www.zhihu.com/question/59088760 提到了一种在线编辑博客的方案，表明，jkelly可以直接提交文件的因为github支持jkelly解析，也就是github内置了jkelly环境。





每个具体的文章使用docsify编写，转换为html后提交 ，文章正式发布后修改静态主页入口的方式 。
https://segmentfault.com/a/1190000021494556
https://www.cnblogs.com/aopstudio/p/10732512.html
https://www.cnblogs.com/aopstudio/p/10470684.html
https://www.cnblogs.com/aopstudio/p/10732523.html


采用这种方式实际上就是找一个实现网页的方案。

我最终的目标是用markdown方式 写博客 ，所以docsify必选。但是blog入口网页到不是必须用markdown的，考虑到jkellly使用麻烦，不选择。

但是完全手写的网页有难度，得找个好模板。
使用markdown转换的网页可能也存在不方便嵌入其他功能的问题。

最终决定用哪个，根据可用模板决定：
http://jekyllthemes.org/
https://hexo.io/themes/

比较喜欢 https://yelog.org/的风格，就用hexo了

# 搭建



# 使用



# 完善

## 更换主题

可在[hexo主题](https://hexo.io/themes/)站点选择自己喜欢的主题，比如：[三栏式布局](https://github.com/yelog/hexo-theme-3-hexo)。 





主要参考资料 

 https://www.jianshu.com/p/1c888a6b8297?utm_source=oschina-app 

 https://hexo.io/zh-cn/docs/ 

 https://www.zhihu.com/question/59088760 

 https://www.jianshu.com/p/0b1fccce74e0 

 https://blog.csdn.net/qq_33429968/article/details/62219783 
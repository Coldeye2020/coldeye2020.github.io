---
title: Hexo配置(一)
urlname: Hexo_configuration_1
date: 2021-4-3 13:20:00
categories: 
- Hexo
tags: [Hexo, Yaml, Configuration]
---

{% note info %}

**Attention**

本文撰写时的环境为`Hexo Version:5.4.0 `,`Next Version:8.2.2`

{% endnote %}

## yaml配置文件

一定要注意：yaml配置文件也是有其固定格式的，特别是要注意空格。

### 经典报错：

```yaml
can not read a block mapping entry; a multiline key may not be an implicit key
```

<!--more-->

### 报错原因：

由于yaml文件配置时，配置项的冒号与值之间未加上空格。

### 我犯的错误：

在配置SEO，修改`根目录配置文件` `theme/next/_config.yml`时

```yaml
# 错误案例
# Google Webmaster tools verification.
# See: https://developers.google.com/search
google_site_verification:vBZBS_Ucyk1uWpkEaY8fasdfasdfasoSATSjHr-k

# Bing Webmaster tools verification.
# See: https://www.bing.com/webmasters
bing_site_verification:0A53asdfassdf5103C2117Ddf5737EA0C7 

# Yandex Webmaster tools verification.
# See: https://webmaster.yandex.ru
yandex_site_verification: 

# 正确案例
# Baidu Webmaster tools verification.
# See: https://ziyuan.baidu.com/site
baidu_site_verification: code-snlfasdfgB7
```



### 经典报错：

```yaml
YAMLException: duplicated mapping key
```

### 报错原因：

一个yaml文件中，配置项出现重复。

### 我犯的错误：

在配置Live2d时，修改站点配置文件`_config.yml`时

```yaml
# 错误案例
# Live2D
## https://github.com/xiazeyu/live2d-widget.js
## https://l2dwidget.js.org/docs/class/src/index.js~L2Dwidget.html#instance-method-init
live2d:
   enable: true
   # enable: false
   scriptFrom: local # 默认
   pluginRootPath: live2dw/ # 插件在站点上的根目录(相对路径)
   pluginJsPath: lib/ # 脚本文件相对与插件根目录路径
   pluginModelPath: assets/ # 模型文件相对与插件根目录路径
   # scriptFrom: jsdelivr # jsdelivr CDN
   # scriptFrom: unpkg # unpkg CDN
   # scriptFrom: https://cdn.jsdelivr.net/npm/live2d-widget@3.x/lib/L2Dwidget.min.js # 你的自定义 url
   tagMode: false # 标签模式, 是否仅替换 live2d tag标签而非插入到所有页面中
   debug: false # 调试, 是否在控制台输出日志
   model:
     use: live2d-widget-model-koharu # npm-module package name
     # use: wanko # 博客根目录/live2d_models/ 下的目录名
     # use: ./wives/wanko # 相对于博客根目录的路径
     # use: https://cdn.jsdelivr.net/npm/live2d-widget-model-wanko@1.0.5/assets/wanko.model.json # 你的自定义 url
   model:
     scale: 1
     hHeadPos: 0.5
     vHeadPos: 0.618
   display:
     superSample: 2
     width: 300
     height: 450
     position: right
     hOffset: 0
     vOffset: -20
   mobile:
     show: true
     scale: 0.5
   react:
     opacityDefault: 0.7
     opacityOnHover: 0.2

# 正确示范
# Live2D
## https://github.com/xiazeyu/live2d-widget.js
## https://l2dwidget.js.org/docs/class/src/index.js~L2Dwidget.html#instance-method-init
live2d:
   enable: true
   # enable: false
   scriptFrom: local # 默认
   pluginRootPath: live2dw/ # 插件在站点上的根目录(相对路径)
   pluginJsPath: lib/ # 脚本文件相对与插件根目录路径
   pluginModelPath: assets/ # 模型文件相对与插件根目录路径
   # scriptFrom: jsdelivr # jsdelivr CDN
   # scriptFrom: unpkg # unpkg CDN
   # scriptFrom: https://cdn.jsdelivr.net/npm/live2d-widget@3.x/lib/L2Dwidget.min.js # 你的自定义 url
   tagMode: false # 标签模式, 是否仅替换 live2d tag标签而非插入到所有页面中
   debug: false # 调试, 是否在控制台输出日志
   model:
     use: live2d-widget-model-koharu # npm-module package name
     # use: wanko # 博客根目录/live2d_models/ 下的目录名
     # use: ./wives/wanko # 相对于博客根目录的路径
     # use: https://cdn.jsdelivr.net/npm/live2d-widget-model-wanko@1.0.5/assets/wanko.model.json # 你的自定义 url
     scale: 1
     hHeadPos: 0.5
     vHeadPos: 0.618
     
   display:
     superSample: 2
     width: 300
     height: 450
     position: right
     hOffset: 0
     vOffset: -20
   mobile:
     show: false
     scale: 0.5
   react:
     opacityDefault: 0.7
     opacityOnHover: 0.2
```





## 令人感到绝望的评论系统建立

### 流程：

1. 首先打算使用`gitalk`，根据官方文档[Comment Systems](https://theme-next.js.org/docs/third-party-services/comments.html)给出的配置一步一步进行，但最后总是提示`bad credentials`，不解，于是查看原仓库`issue`，发现也有类似的案例，但是他们都是通过“重新更新了`clientSecret`之后再输入一次来解决的，我尝试多次未果后，选择在google上找解决方案，但是根据他们的博客内容，大体也同样是刷新一次就解决了，还有一个是通过加单引号解决的（可能也是通过更新，只是博主并未意识到），所以在经历了长达2h的鏖战未果后，我无奈选择了放弃使用`gitalk`作为comment system。

2. 然后我开始查找好用的评论系统，发现很多人都推荐了`valine`，所以我开始了漫长的配置之旅

3. 我首先查看官方文档，发现文档中并未预装`valine`插件，也没有相关教程，于是我查看了valine官网，但是配置过程过于复杂，所以我决定google一份教程，但大部分的教程都指向next主题是预装了`valine`插件的，只需要修改主题配置文件，打开这一功能就可以了，这些教程最晚的时间是今年2月份的，所以我以为valine是已经预装了，但是官方文档没写而已，于是参照教程上的步骤一步一步更改了配置文件，然后就。。。

4. 更早之前的教程指向需要自己`npm`安装一下，但是我觉得不可信，所以在next官方仓库中查了一下更新内容，发现还真的有，打开发现是在最近的版本（next8.1貌似）中删除了这个`valine`，具体原因没有明确指出，但是我在`issue`中看到了网友讨论的原因。于是查看了他们第三方comment system的使用方案，根据`hexo-next-valine`的教程完成了配置，但要命的事情发生了，我`hexo s`后查看博客时发现报错`valine Code 401: 未经授权的操作，请检查你的AppId和AppKey`，我google了大量的相关教程，发现他们要么是说`AppId`和`AppKey`配置错误，要么就是说自己代码有问题，也有说是打开了`next`中的`leancloud-counter`功能导致的，但都不符合我的情况，在疯狂的一顿尝试之后我决定再次更换。

5. 但是我仍感觉不死心，所以我重新的在`issue`中查找了一番，然后找到了`valine`中被`next`下架的原因，以及网友们推荐的新的替代品`waline`，但是`waline`是最近才出来的，没有与`hexo`适配的插件，需要自己更改`html`文件，考虑到之后next hexo更新的时候可能会出现的诸多merge，我有点不想尝试了，但是在查看`waline`官网教程的时候我无意发现了这样一句：

   ![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/hexo_1.png)

   然后，我貌似发现之前报错`valine Code 401: 未经授权的操作，请检查你的AppId和AppKey`的原因了（对，没错我就是那个注册了Leancode国内版的倒霉蛋），因为这两个项目都是使用的leancloud作为自己的应用服务器，所以我考虑到可能是因为Leancloud不同区域的服务不同造成的，于是我从新注册了一个国际版帐号，结果顺利通过，不再报错，至此博客的评论系统正式建立完成。

### 我犯的错误：

在搭建`gitalk`时的错误至今仍是个谜，在搭建`valine`时的错误在于我没有考虑到同一家网站国际版和国内版的服务居然会不同，浪费了大量时间，事实上网上很多教程都是使用的国内版进行注册的，他们没有遇到这个问题应该是当时还不需要备案。

### 后续：

当然，由于潜在的安全隐患，这个博客肯定不会长期使用`valine`作为comment system，等`waline`与`hexo`适配的插件出来后，我应该会考虑使用`waline`。

## ~~退而求其次的公式渲染器~~MathJax

### 流程：

1. next官方文档是表明了支持两种公式渲染的插件，即`MathJax`以及`KaTex`，一开始我上网搜了一下两个渲染器的差别，基本都写道`KaTex`相较于`MathJax`支持更少的公式效果，但是渲染速度十分的快，鉴于此我决定采用`KaTex`来作为博客的数学公式渲染器

2. 官方文档[Math Equations](https://theme-next.js.org/docs/third-party-services/math-equations.html)是提供了两种安装方案，即[hexo-renderer-markdown-it-plus](https://github.com/CHENXCHEN/hexo-renderer-markdown-it-plus)，以及[hexo-renderer-markdown-it](https://github.com/hexojs/hexo-renderer-markdown-it)，我稍微看了下两个插件的区别，无非是前者plus版安装更为简洁，相当于对后者进行了一次封装。所以我果断选择了前者，但是配置好后发现公式的渲染效果差强人意，（就像是用正常的字体写的公式，而不是一般我们看到的像意大利斜体的公式），果然还是不如老大哥`MathJax`，所以我卸载了这个插件

3. ~~在安装`MathJax`时，需要安装渲染器[hexo-renderer-pandoc](https://github.com/wzpan/hexo-renderer-pandoc)，这和之前使用`KaTex`的安装步骤差不多，但是要命的来了，就是他需要`pandoc`本身作为dependency，我是使用的manjaro，发现是预装了这款软件的，所以我可以很轻易的就利用`MathJax`对markdown中的公式进行渲染，但是部署到github上时，我发现好像并没有效果，并且正常的markdown渲染都出了问题，所以我猜测可能是因为我使用了`CI`的原因（我并不是直接将渲染好了的文件通过`hexo d`部署到github，而是在`CI`中进行的渲染并部署的，而`CI`的虚拟机中没有预装`pandoc`所以才导致了这样的结果），于是我google了一下解决方案，貌似大家都没有使用`CI`，并没有人遇到类似的问题，我只是看到`pandoc`官方文档中写道，`github actions`支持`pandoc`，所以我推测`CI`是一定有办法使用到`pandoc`的，我稍微看看了使用案例，但考虑到还是太麻烦了，所以退而求其次，我重新回到`KaTex`的怀抱中。~~**本博客已经采用`MathJax`进行渲染，解决方案为使用`Travis CI`预装`pandoc`，详情见`/.travis.yml`文件**

4. 然后又又又出了点小问题，因为`next`主题是提供了两种方式开启公式渲染器的嘛，即每个文章都进行渲染，或者使用`front matter`的方式指定文章是否进行公式渲染，想必只要是一个真心想把博客做好的同学都会选择后者的吧，毕竟每篇都进行公式渲染的话，posts少的时候还好，但是如果posts多起来了，可能会大量增加渲染的时间，所以我使用了后者，具体的配置如下

   ```yaml
   math:
      # Default (false) will load mathjax / katex script on demand.
      # That is it only render those page which has `mathjax: true` in front-matter.
      # If you set it to true, it will load mathjax / katex srcipt EVERY PAGE.
      every_page: false
   
      mathjax:
        enable: false
        # Available values: none | ams | all
        tags: none
   
      katex:
        enable: true
        # See: https://github.com/KaTeX/KaTeX/tree/master/contrib/copy-tex
        copy_tex: false
   ```

5. 其实在配置文件中已经说明的很清楚了，需要在想要进行公式渲染的文章`front-matter`部分加入`mathjax: true`即可，但是我以为如果要使用`KaTex`的话就要把配置项改为`katex: true`，真是不做死就不会死，于是成功的又让我陷入了沉思，还好我看到了一篇文章 [ 《hexo+next公式支持---采用Katex》](https://lingr7.github.io/2019/10/03/hexo+next%E5%85%AC%E5%BC%8F%E6%94%AF%E6%8C%81---%E9%87%87%E7%94%A8Katex.html)，里面谈到即使是使用`KaTex`也要将配置想设置为`mathjax: true`才可以，至此安装和使用的基本问题解决，鉴于`katex`有特别多的限制，以后有时间可能会再写一篇来介绍，或者在这篇博文下面补充。

### 后续：

~~因为我现在对于公式渲染的要求还不大，然后其实`KaTex`本身除了渲染的效果丑一点以外，速度还是杠杠的，所以暂时应该会继续使用`KaTex`作为公式渲染器了，以后如果有机会学习了`github actions`可能会重装`MathJax`练练手。~~**本博客已经采用`MathJax`进行渲染，解决方案为使用`Travis CI`预装`pandoc`，详情见`/.travis.yml`文件**

## 关于移动端适配

其实就是响应式布局，直接把教程链接放在这吧

[Hexo博客Next主题如何在移动端上设置不同的背景](http://seikasahara.com/p/1578.html)

```css
# 电脑 + 移动端适配
body{
    background:url(/images/bg.jpg);
    background-size:cover;
    background-repeat:no-repeat;
    background-attachment:fixed;
    background-position:center;  
}

@media only screen and (max-width: 1000px) {
  body{
    background:url(/images/bg2.jpg);
    background-size:cover;
    background-repeat:no-repeat;
    background-attachment:fixed;
    background-position:center;  
  }
}

# 移动端 + safari适配（对第二段进行一下修改即可）
@media only screen and (max-width: 1000px) {
  body:before{
  content:"";
  display:block;
  position:fixed;
  top:0;
  left:0;
  bottom: 0;
  z-index:-1;
  width:100%;
  height:100vh;
  background:url(/images/bg2.png) center 0 no-repeat;
  background-size:cover;
  }
}

# 主要是safari识别不了
# background-attachment:fixed;
# background-position:center;  
# 这两项


# 当然如果考虑到像ipad这样的大屏幕，我们也需要将body部分做一些修改
body:before{
   content:"";
   display:block;
   position:fixed;
   top:0;
   left:0;
   bottom: 0;
   z-index:-1;
   width:100%;
   height:100vh;
   background:url(../images/background.jpg) center 0 no-repeat;
   background-size:cover;
}
```

## 整个博客的工作流程详解

### 整体布局：

![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/hexo_1.svg)

### 工作流程

#### 普通模式

+ 适用：在自己电脑(`windows 10`)上进行简单的写作并发表博客
+ 流程：layout中红线所示
+ 命令：`git add. `+`git commit -m "new blog"`+`git push`即可

#### 陌生环境模式

+ 适用：在别人的电脑上进行写作并发表博客

+ 流程：

  + 首先安装`git`

  + 然后配置远程仓库并拉取

    ```shell
    $git init
    
    $git remote add origin https://github.com/user/repo.git
    # Set a new remote
    
    $git 
    # Verify new remote
    > origin  https://github.com/user/repo.git (fetch)
    > origin  https://github.com/user/repo.git (push)
    
    # 拉取远程仓库
    $git pull
    
    # 切换分支
    $git checkout writer
    
    # 更改为ssh验证方式登录（如无长期需求，切勿使用这种方式）
    $ git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
    ```

  + 接下来，layout中红线所示

+ 命令：如上`命令`+`git add. `+`git commit -m "new blog"`+`git push`即可

#### 本地调试模式

+ 适用：在自己电脑(`manjaro`)上进行博客样式或者插件的调试等
+ 流程：
  + 更改配置
  + 渲染
  + 创建服务
+ 命令：`hexo g`，`hexo s`

### 工作机制详解：

#### 本地主机部分

首先通过`git`的三段命令，我们可以将除开被纳入`gitinore`文件内的所有文件和目录都`push`到github远程仓库中(`branch:writer`)

```none /.gitinore
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
```

#### Travis CI部分

1. 配置文件

   然后Travis CI检测到了`commit`后，先将仓库`pull`到服务器上，然后检查是否有`.travis.yml`，如果存在，则按照`.travis.yml`文件中的配置一步一步执行

   ```yaml /.travis.yml
   language: node_js
   
   node_js:
     - 14.16.0 
     
   cache:
     directories:
       - node_modules
   
   branches:
     only:
     - writer #源码分支名称
       
   before_install:
   - npm install -g hexo
       
   before_script:
   # 下面两行配置用户名和邮箱不写也可以
   - git config user.name "Coldeye"
   - git config user.email "948283368@qq.com"
   # 下面一行代码主要是进行了一个replace操作，即在Travis CI执行的全过程中将
   # _config.yml文件中“https://github.com/Coldeye2020/coldeye2020.github.io.git”的字段
   # replace为“https://${GH_TOKEN}@github.com/coldeye2020/coldeye2020.github.io.git”
   # 注意这个操作是严格大小写区分的，并且是全字符匹配
   # 然后${GH_TOKEN}这是一个变量，主要取决于你在Travis CI官网设置时的变量值，主要是用于github verification
   - sed -i'' "s~https://github.com/Coldeye2020/coldeye2020.github.io.git~https://${GH_TOKEN}@github.com/coldeye2020/coldeye2020.github.io.git~" _config.yml
   
   install:
   - npm install
   # 这一步是安装hexo 和 github联动的插件，只有这样hexo deploy执行时才可以执行git操作
   - npm install hexo-deployer-git --save
   
   script:
   - hexo clean
   - hexo generate
   
   after_success:
   # 将根据.config.yml文件中deploy项中的配置进行执行
   - hexo deploy
   ```

   {% note info %}

   #### Attention

   这里应该有三种方式配置`.travis.yml`文件的方式：

   1. 以`hexo`的方式(本博客采用的方案，最为简单，并且对插件`baidu_url_submitter`的支持也更简单)
   2. 以`travis ci`的方式(`Hexo`[中文官网](https://hexo.io/docs/github-pages)给出的方案)
   3. 以`github action`的方式(`Hexo`[英文官网](https://hexo.io/docs/github-pages)给出的方案)

   {% endnote %}

   ```yaml /_config.yml
   deploy:
   # deploy type设置为git,这需要首先安装插件hexo-deployer-git
   - type: git
   # 这里的repo本应该设置为"https://${GH_TOKEN}@github.com/coldeye2020/coldeye2020.github.io.git"
   # 但考虑到本项目放置在开源库下，所以仓库的Token肯定不可以写在配置文件中
   # 这里使用的trick就是在.travis.yml中用命令sed -i进行字符串替换
   # 把关键的token使用travis CI中早已经设置好的变量进行赋值，大大提高了安全性
     repo: https://github.com/Coldeye2020/coldeye2020.github.io.git
     # 设置deloy的分支为main
     branch: main
     message: "deployment"
     
   - type: baidu_url_submitter
   ```

2. 命令执行
   1. `hexo generate`命令在执行时会首先将`/source/`目录下所有开头不是下划的文件拷贝到/public/目录下（注：所有的文章均放置在`/source/_post/`目录下），对于`Markdown`和`HTML`文件则会先进行渲染然后再拷贝（如果想要指定某个`Markdown`或者`HTML`文件不进行渲染可以在站点配置文件`/_config.yml`中配置`skip_render`项）。在此过程中他会根据`markdown`文件中`front matter`段的`categories`项的值`A`来，确定渲染后得到的`HTML`文件应该放置在`/source/public/`目录下的同名`A`子目录下。如果是没有进行渲染的文件，则会保持原样放在`/public`下，其他部分(e.g.子目录`archives`,`categories`，`tags`)的生成也是差不多这么回事。同样的，`/themes/next/source/`目录下文件也会同样被copy到`/public/`目录下。
   2. `hexo deploy`命令在执行时会按照`/_config.yml`文件中的配置，将`/public/`目录下的所有文件`push`到`github 远程仓库`的`mian`分支

#### Github 远程仓库部分

+ 来自外部的`push`
  + 来自本地主机的文件将被`push`到`writer`分支
  + 来自Travis CI的文件将被`push`到`main`分支
+ 来自外部的`pull`
  + 被Travis CI`pull`
    + 若出现了`writter`分支的commit
    + 检测是否存在`.travis.yml`文件
    + 对`writer`分支中的文件进行`hexo g`操作
  + 被Vercel`pull`
    + 若出现了`main`分支的commit
    + 直接将`main`分支`pull`下来

#### Vercel 网站托管平台部分

1. 如上所示，即Github仓库中的`main`分支如果出现了`commit`则会执行部署(但缺少部署文件，所以就是简单地pull下来了)
2. 这个部分主要是提供了CDN服务，便于国内用户访问
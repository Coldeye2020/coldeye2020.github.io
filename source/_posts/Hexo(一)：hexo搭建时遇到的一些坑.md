---
title: Hexo踩坑(一)
urlname: Hexo(1)
date: 2021-4-3 13:20:00
categories: [Hexo]
tags: [Hexo, Yaml, Configuration]
---

## yaml配置文件

一定要注意：yaml配置文件也是有其固定格式的，特别是要注意空格。

### 经典报错：

```
can not read a block mapping entry; a multiline key may not be an implicit key
```

<!--more-->

### 我犯的错误：

在配置SEO，修改 `theme/next/_config.yml`

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

## 令人感到绝望的评论系统建立

### 流程：

1. 首先打算使用`gitalk`，根据官方文档给出的配置一步一步进行，但最后总是提示`bad credentials`，不解，于是查看原仓库`issue`，发现也有类似的案例，但是他们都是通过“重新更新了`clientSecret`之后再输入一次来解决的，我尝试多次未果后，选择在google上找解决方案，但是根据他们的博客内容，大体也同样是刷新一次就解决了，还有一个是通过加单引号解决的（可能也是通过更新，只是博主并未意识到），所以在经历了长达2h的鏖战未果后，我无奈选择了放弃使用`gitalk`作为comment system。

2. 然后我开始查找好用的评论系统，发现很多人都推荐了`valine`，所以我开始了漫长的配置之旅

3. 我首先查看官方文档，发现文档中并未预装`valine`插件，也没有相关教程，于是我查看了valine官网，但是配置过程过于复杂，所以我决定google一份教程，但大部分的教程都指向next主题是预装了`valine`插件的，只需要修改主题配置文件，打开这一功能就可以了，这些教程最晚的时间是今年2月份的，所以我以为valine是已经预装了，但是官方文档没写而已，于是参照教程上的步骤一步一步更改了配置文件，然后就。。。

4. 更早之前的教程指向需要自己`npm`安装一下，但是我觉得不可信，所以在next官方仓库中查了一下更新内容，发现还真的有，打开发现是在最近的版本（next8.1貌似）中删除了这个`valine`，具体原因没有明确指出，但是我在`issue`中看到了网友讨论的原因。于是查看了他们第三方comment system的使用方案，根据`hexo-next-valine`的教程完成了配置，但要命的事情发生了，我`hexo s`后查看博客时发现报错`valine Code 401: 未经授权的操作，请检查你的AppId和AppKey`，我google了大量的相关教程，发现他们要么是说`AppId`和`AppKey`配置错误，要么就是说自己代码有问题，也有说是打开了`next`中的`leancloud-counter`功能导致的，但都不符合我的情况，在疯狂的一顿尝试之后我决定再次更换。

5. 但是我仍感觉不死心，所以我重新的在`issue`中查找了一番，然后找到了`valine`中被`next`下架的原因，以及网友们推荐的新的替代品`waline`，但是`waline`是最近才出来的，没有与`hexo`适配的插件，需要自己更改`html`文件，考虑到之后next hexo更新的时候可能会出现的诸多merge，我有点不想尝试了，但是在查看`waline`官网教程的时候我无意发现了这样一句：

   ![waline](../images/hexo_1.png)

   然后，我貌似发现之前报错`valine Code 401: 未经授权的操作，请检查你的AppId和AppKey`的原因了（对，没错我就是那个注册了Leancode国内版的倒霉蛋），因为这两个项目都是使用的leancloud作为自己的应用服务器，所以我考虑到可能是因为Leancloud不同区域的服务不同造成的，于是我从新注册了一个国际版帐号，结果顺利通过，不再报错，至此博客的评论系统正式建立完成。

### 我犯的错误：

在搭建`gitalk`时的错误至今仍是个谜，在搭建`valine`时的错误在于我没有考虑到同一家网站国际版和国内版的服务居然会不同，浪费了大量时间，事实上网上很多教程都是使用的国内版进行注册的，他们没有遇到这个问题应该是当时还不需要备案。

### 后续：

当然，由于潜在的安全隐患，这个博客肯定不会长期使用`valine`作为comment system，等`waline`与`hexo`适配的插件出来后，我应该会考虑使用`waline`。






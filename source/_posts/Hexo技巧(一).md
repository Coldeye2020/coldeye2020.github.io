---
title: Hexo技巧(一)
date: 2021-04-04 20:43:52
categories: [Hexo]
tags: [Hexo]
mathjax: false
urlname: hexo_trick_1
keywords: [hexo writting, tricks]
description:
---

{% note info %}

**Attention**

本文撰写时的环境为`Hexo Version:5.4.0 `,`Next Version:8.2.2`

{% endnote %}



`Next`主题或者说`HEXO`官方其实是提供了很多可以增加博文美观的[plugins](https://theme-next.js.org/docs/tag-plugins)，这篇文章将介绍部分实用的plugins以帮助使用者们更好的使用`Hexo`进行写作：

1. Button
2. Group Pictures
3. Label
4. Link Grid
5. Note
6. PDF
7. Tabs



<!--more-->

## Button

### 作用：

将链接封装在一个button中以提高互动性和美观程度。

### 用法：

```markdown
{% button url, text, icon [class], [title] %}
<!-- Tag Alias -->
{% btn url, text, icon [class], [title] %}
```

+ url : 绝对路径或者相对路径，当然也可以是网络地址
+ text : Button中的文字内容. （和icon两者任选其一即可，也可以同时使用两者）
+ icon : Button中的Awesome Icon （和text两者任选其一）
+ [class] : 可选项，icon的size(es): fa-fw | fa-lg | fa-2x | fa-3x | fa-4x | fa-5x（从小到大）
+ [title] :可选项， 鼠标悬停时的提示文字.

### 示例：

#### Button with text

```html
{% btn #, Text %}
{% btn #, Text & Title,, Title %}
```

{% btn #, Text %}  {% btn #, Text & Title,, Title %}

#### Button with icon

```html
# 使用<div> </div> 进行换行控制
<div>{% btn #,, home fa-5x %}{% btn #,, home fa-5x %}{% btn #,, home fa-5x %}</div>
<div>{% btn #,, home fa-4x %}{% btn #,, home fa-4x %}{% btn #,, home fa-4x %}</div>
<div>{% btn #,, home fa-3x %}{% btn #,, home fa-3x %}{% btn #,, home fa-3x %}</div>
<div>{% btn #,, home fa-2x %}{% btn #,, home fa-2x %}{% btn #,, home fa-2x %}</div>
<div>{% btn #,, home fa-lg %}{% btn #,, home fa-lg %}{% btn #,, home fa-lg %}</div>
<div>{% btn #,, home %}{% btn #,, home %}{% btn #,, home %}</div>
```

<div>{% btn #,, home fa-5x %}{% btn #,, home fa-5x %}{% btn #,, home fa-5x %}<div>
<div>{% btn #,, home fa-4x %}{% btn #,, home fa-4x %}{% btn #,, home fa-4x %}<div>
<div>{% btn #,, home fa-3x %}{% btn #,, home fa-3x %}{% btn #,, home fa-3x %}<div>
<div>{% btn #,, home fa-2x %}{% btn #,, home fa-2x %}{% btn #,, home fa-2x %}<div>
<div>{% btn #,, home fa-lg %}{% btn #,, home fa-lg %}{% btn #,, home fa-lg %}<div>
<div>{% btn #,, home %}{% btn #,, home %}{% btn #,, home %}<div>

#### Button with text & icon

```html
<p>{% btn #, Text & Icon (buggy), home %}
{% btn #, Text & Icon (fixed width), home fa-fw %}</p>
```

<p>{% btn #, Text & Icon (buggy), home %} {% btn #, Text & Icon (fixed width), home fa-fw %}</p>

#### Button inside text

```html
Lorem {% btn #, Lorem, home fa-fw fa-lg %} ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident {% btn #, Ipsum, home fa-fw fa-lg %}, sunt in culpa qui officia deserunt mollit anim id est laborum.

```

Lorem {% btn #, Lorem, home fa-fw fa-lg %} ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident {% btn #, Ipsum, home fa-fw fa-lg %}, sunt in culpa qui officia deserunt mollit anim id est laborum.

#### Button inside other tag

```html
{% note info %}
{% btn #, Text & Icon, home fa-fw %}

{% btn #,, home, Title %}{% btn #, Text %}

[Link](#)
{% endnote %}
```

{% note info %}
{% btn #, Text & Icon, home fa-fw %}

{% btn #,, home, Title %}{% btn #, Text %}

[Link](#)
{% endnote %}

#### Button margin

```html
<div class="text-center"><div>{% btn #,, heading %}{% btn #,, fab fa-edge %}{% btn #,, times %}{% btn #,, circle-notch %}</div>
<div>{% btn #,, italic %}{% btn #,, fab fa-scribd %}</div>
<div>{% btn #,, fab fa-google %}{% btn #,, fab fa-chrome %}{% btn #,, fab fa-opera %}{% btn #,, gem fa-rotate-270 %}</div></div>
```

<div class="text-center"><div>{% btn #,, heading %}{% btn #,, fab fa-edge %}{% btn #,, times %}{% btn #,, circle-notch %}</div>
<div>{% btn #,, italic %}{% btn #,, fab fa-scribd %}</div>
<div>{% btn #,, fab fa-google %}{% btn #,, fab fa-chrome %}{% btn #,, fab fa-opera %}{% btn #,, gem fa-rotate-270 %}</div></div>

#### Button with relative URL

```html
<div class="text-center">{% btn #, Previous Chapter, arrow-left fa-fw fa-lg, Previous Chapter (Full Image) %} {% btn #, Next Chapter, arrow-right fa-fw fa-lg, Next Chapter (Label) %}</div>
```

#### <div class="text-center">{% btn #, Previous Chapter, arrow-left fa-fw fa-lg, Previous Chapter (Full Image) %} {% btn #, Next Chapter, arrow-right fa-fw fa-lg, Next Chapter (Label) %}</div>

#### Button with absolute URL

```html
<div class="text-center">{% btn https://github.com, GitHub, fab fa-github fa-fw fa-lg, GitHub %}</div>
```

<div class="text-center">{% btn https://github.com, GitHub, fab fa-github fa-fw fa-lg, GitHub %}</div>


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

+ `url`: 绝对路径或者相对路径，当然也可以是网络地址
+ `text`: Button中的文字内容. （和icon两者任选其一即可，也可以同时使用两者）
+ `icon`: Button中的Awesome Icon （和text两者任选其一）
+ `[class]`: 可选项，icon的size(es): fa-fw | fa-lg | fa-2x | fa-3x | fa-4x | fa-5x（从小到大）
+ `[title]`:可选项， 鼠标悬停时的提示文字.

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

<div class="text-center">{% btn #, Previous Chapter, arrow-left fa-fw fa-lg, Previous Chapter (Full Image) %} {% btn #, Next Chapter, arrow-right fa-fw fa-lg, Next Chapter (Label) %}</div>

#### Button with absolute URL

```html
<div class="text-center">{% btn https://github.com, GitHub, fab fa-github fa-fw fa-lg, GitHub %}</div>
```

<div class="text-center">{% btn https://github.com, GitHub, fab fa-github fa-fw fa-lg, GitHub %}</div>





## Group Pictures

### 作用：

按照一定的结构排列一组图片，以增加美感。

### 用法：

```markdown
{% grouppicture [number]-[layout] %}{% endgrouppicture %}
<!-- Tag Alias -->
{% gp [number]-[layout] %}{% endgp %}
```

+ `[number]` : 可选项，图片的总数量
+ `[layout]` : 可选项，图片的布局结构

`[layout]`如下：

![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/group-picture-1.png)

![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/group-picture-2.png)

### 示例：

```css
{% grouppicture 6-3 %}
![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/next.svg)
![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/next.svg)
![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/next.svg)
![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/next.svg)
![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/next.svg)
![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/next.svg)
{% endgrouppicture %}
```





## Label

### 作用：

对文字加上标签，突出重点，增加文章可读性。

### 用法：

```markdown
{% label [class]@text %}
```

+ `[class]` : 可选项，支持的值有: `default` | `primary` | `success` | `info` | `warning` | `danger`.默认为`default`
+ `text` : `@text` can be specified with or without space
  E.g. `success @text` is the same as `success@text`.

### 示例：

```html
Lorem {% label @ipsum %} {% label primary@dolor sit %} amet, consectetur {% label success@adipiscing elit, %} sed {% label info@do eiusmod %} tempor incididunt ut labore et dolore magna aliqua.

Ut enim *{% label warning @ad %}* minim veniam, quis **{% label danger@nostrud %}** exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

Duis aute irure dolor in reprehenderit in voluptate ~~{% label default @velit %}~~ <mark>esse</mark> cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

```

Lorem {% label @ipsum %} {% label primary@dolor sit %} amet, consectetur {% label success@adipiscing elit, %} sed {% label info@do eiusmod %} tempor incididunt ut labore et dolore magna aliqua.

Ut enim *{% label warning @ad %}* minim veniam, quis **{% label danger@nostrud %}** exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

Duis aute irure dolor in reprehenderit in voluptate ~~{% label default @velit %}~~ <mark>esse</mark> cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.



## Link Grid

### 作用：

动态的`link grid`，增加互动性

### 用法：

```css
{% linkgrid [image] [delimiter] [comment] %}{% endlinkgrid %}
<!-- Tag Alias -->
{% lg [image] [delimiter] [comment] %}{% endlg %}
```

+ `[image]` : 可选项， 图片的URL地址.
+ `[delimiter]` : 可选项，如果不给出分隔符的话默认分隔符为`|`，可以在此项指定分隔符.
+ `[comment]` : 可选项，如果不给出的注释参数的话默认分隔符为`%`，可以在此项指定注释参数.

### 示例：

#### 使用方式1

```
{% linkgrid %}
Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
% Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
{% endlinkgrid %}
```

{% linkgrid %}
Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
% Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
{% endlinkgrid %}

#### 使用方式2

```
{% lg /images/apple-touch-icon-next.png , %}
Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
% Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
{% endlg %}
```

{% lg /images/apple-touch-icon-next.png , %}
Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
% Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. ,https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/apple-touch-icon-next.png
{% endlg %}







## Note

### 作用：

动态的`link grid`，增加互动性

### 设置：

打开主题配置文件`next/_config.yml`

```yaml
note:
  # Note tag style values:
  #  - simple    bs-callout old alert style. Default.
  #  - modern    bs-callout new (v2-v3) alert style.
  #  - flat      flat callout style with background, like on Mozilla or StackOverflow.
  #  - disabled  disable all CSS styles import of note tag.
  style: simple
  icons: false
  # Offset lighter of background in % for modern and flat styles (modern: -12 | 12; flat: -18 | 6).
  # Offset also applied to label tag variables. This option can work with disabled note tag.
  light_bg_offset: 0
```



### 用法：

```css
{% note [class] [no-icon] [summary] %}
Any content (support inline tags too).
{% endnote %}
```

+ `[class]` : 可选项，支持的值有: default | primary | success | info | warning | danger.
+ `[no-icon]` : 可选项，取消icon.
+ `[summary]` : 可选项，总结note.

### 示例：

#### 简单示例

```css
{% note %}
#### Header
(without define class style)
{% endnote %}
```

{% note %}
#### Header
(without define class style)
{% endnote %}

```markdown
{% note default %}
#### Default Header
Welcome to [Hexo!](https://hexo.io)
{% endnote %}
```

{% note default %}
#### Default Header
Welcome to [Hexo!](https://hexo.io)
{% endnote %}

```markdown
{% note primary %}
#### Primary Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}
```

{% note primary %}
#### Primary Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}

```markdown
{% note info %}
#### Info Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}
```

{% note info %}
#### Info Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}

```markdown
{% note success %}
#### Success Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}
```

{% note success %}
#### Success Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}

```markdown
{% note warning %}
#### Warning Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}
```

{% note warning %}
#### Warning Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}

```markdown
{% note danger %}
#### Danger Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}
```

{% note danger %}
#### Danger Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}



#### 高级用法

##### No icon note

```markdown
{% note info no-icon %}
#### No icon note
Note **without** icon: `note info no-icon`
{% endnote %}
```

{% note info no-icon %}
#### No icon note
Note **without** icon: `note info no-icon`
{% endnote %}

##### Note with summary

```markdown
{% note primary This is a summary %}
#### Details and summary
Note with summary: `note primary This is a summary`
{% endnote %}
```

{% note primary This is a summary %}
#### Details and summary
Note with summary: `note primary This is a summary`
{% endnote %}

##### No icon with Summary

```markdown
{% note info no-icon This is a summary %}
#### Details and summary (No icon)
Note with summary: `note info no-icon This is a summary`
{% endnote %}
```

{% note info no-icon This is a summary %}
#### Details and summary (No icon)
Note with summary: `note info no-icon This is a summary`
{% endnote %}

##### Codeblock in note

```markdown
{% note success %}
#### Codeblock in note
{% code %}
code block in note tag
code block in note tag
code block in note tag
{% endcode %}
{% endnote %}
```

{% note success %}
#### Codeblock in note
{% code %}
code block in note tag
code block in note tag
code block in note tag
{% endcode %}
{% endnote %}

##### List in note

```markdown
{% note default %}
#### Lists in note
* ul
* ul
    * ul
    * ul
* ul

1. ol
2. ol
    1. ol
    2. ol
3. ol
{% endnote %}
```

{% note default %}
#### Lists in note
* ul
* ul
    * ul
    * ul
* ul

1. ol
2. ol
    1. ol
    2. ol
3. ol
{% endnote %}

##### Table in note

```markdown
#### Table in Note
{% note default %}
| 1 | 2 |
| - | - |
| 3 | 4 |
| 5 | 6 |
| 7 | 8 |
{% endnote %}
```

#### Table in Note
{% note default %}
| 1    | 2    |
| ---- | ---- |
| 3    | 4    |
| 5    | 6    |
| 7    | 8    |
{% endnote %}





## PDF

### 设置：

在主题配置文件`next/_config.yml`

```yaml
pdf:
  enable: true
  # Default height
  height: 500px
```

### 作用：

可以在文章中导入pdf。

### 用法：

```markdown
{% pdf url [height] %}
```

+ `url` : The URL (Absolute path) of the PDF file.
+ `[height]` : *Optional parameter.* Height of the PDF display element, e.g. 800px.

### 示例：

```markdown
{% pdf https://example.com/sample.pdf %}
```

```markdown
{% pdf /path/to/your/file.pdf 600px %}
```





## Tabs

### 设置：

在主题配置文件`next/_config.yml`

```yaml
tabs:
  transition:
    tabs: false
    labels: true
```

### 作用：

可以在文章中加入带有互动选项的表格，一般用于提供某一个问题的多种不同解决方案。

### 用法：

```markdown
{% tabs Unique name, [index] %}
<!-- tab [Tab caption] [@icon] -->
Any content (support inline tags too).
<!-- endtab -->
{% endtabs %}
```

+ `Unique name` : 表的名字
  + 必选参数
  + 首先一定要有，作为该tabs的唯一标识符，且一篇文章中不能出现同名的unique name
  + 并且当`[Tab caption]`项没有指定的话，将与`自动生成的index`一起作为每一个选项的名字
+ `[index]` : 默认出现的选项
  + 可选参数
  + 可以选择某一个选项作为默认选项，即如果用户未指定就是这个选项，若不指定`[index]`默认为1
  + 当然也可以设置一个选项都不指定，将`[index]`的值设置为`-1`
+ `[Tab caption]` : 各选项的表头名
  + 可选参数
  + 如果不指定
    + 同时也没有设置选项的`[@icon]`：则默认设置为`Unique name`+选项对应的`index`
    + 如果设置了`[@icon]`：则留空
+ `[@icon]` :  字体图标名
  + 可选参数
  + 可以与`[Tab caption]`配合起来一起使用，也可以单独使用

### 示例：

#### 简单用法：

##### Tabs with default tab selected

```markdown
{% tabs First unique name %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

{% tabs First unique name %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}



##### Tabs with 3rd tab selected

```markdown
{% tabs Second unique name, 3 %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

{% tabs Second unique name, 3 %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}



##### Tabs with no tab selected

```markdown
{% tabs Third unique name, -1 %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

{% tabs Third unique name, -1 %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}

##### Tabs with custom labels

```markdown
{% tabs Fourth unique name %}
<!-- tab Solution 1 -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab Solution 2 -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab Solution 3 -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

{% tabs Fourth unique name %}
<!-- tab Solution 1 -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab Solution 2 -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab Solution 3 -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}



##### Tabs with icons only

```markdown
{% tabs Fifth unique name %}
<!-- tab @text-width -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab @font -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab @bold -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

{% tabs Fifth unique name %}
<!-- tab @text-width -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab @font -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab @bold -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}



##### Tabs with icons and labels

```markdown
{% tabs Sixth unique name %}
<!-- tab Solution 1@text-width -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab Solution 2@font -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab Solution 3@bold -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

{% tabs Sixth unique name %}
<!-- tab Solution 1@text-width -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab Solution 2@font -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab Solution 3@bold -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}



#### 高级用法

##### Tabs permalinks test（tabs在页面中的链接）

```markdown
Permalink for > [Tab one](#tab-one).
Permalink for > [Tab one 1](#tab-one-1).
Permalink for > [Tab one 2](#tab-one-2).
Permalink for > [Tab one 3](#tab-one-3).

Permalink for > [Tab two](#tab-two).
Permalink for > [Tab two 1](#tab-two-1).
Permalink for > [Tab two 2](#tab-two-2).
Permalink for > [Tab two 3](#tab-two-3).

{% tabs Tab one %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}

{% tabs Tab two %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

Permalink for > [Tab one](#tab-one).
Permalink for > [Tab one 1](#tab-one-1).
Permalink for > [Tab one 2](#tab-one-2).
Permalink for > [Tab one 3](#tab-one-3).

Permalink for > [Tab two](#tab-two).
Permalink for > [Tab two 1](#tab-two-1).
Permalink for > [Tab two 2](#tab-two-2).
Permalink for > [Tab two 3](#tab-two-3).

{% tabs Tab one %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}

{% tabs Tab two %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}

##### Tabs with other tags

```markdown
{% tabs Tags %}
<!-- tab -->
**This is Tab 1.**

1. One
2. Two
3. Three

Indented code block:

    nano /etc

Tagged code block:

{% code %}
code tag
code tag
code tag
{% endcode %}

{% note default %}
Note default tag.
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**

* Five
* Six
* Seven

{% note primary %}
{% youtube Kt7u5kr_P5o %}
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**

{% subtabs Sub Tabs %}
<!-- tab -->
**This is Sub Tab 1.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

{% note warning %}
Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.
{% endnote %}

Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub Tab 2.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

{% note danger %}
Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub Tab 3.**

{% subtabs Sub-Sub Tabs %}
<!-- tab -->
**This is Sub-Sub Tab 1 of Sub Tab 3.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub-Sub Tab 2 of Sub Tab 3.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

{% note warning %}
Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}

{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub-Sub Tab 3 of Sub Tab 3.**

{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

{% note warning %}
Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

{% note danger %}
Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}

{% endnote %}

{% endnote %}
<!-- endtab -->
{% endsubtabs %}

<!-- endtab -->
{% endsubtabs %}

<!-- endtab -->
{% endtabs %}
```

{% tabs Tags %}
<!-- tab -->
**This is Tab 1.**

1. One
2. Two
3. Three

Indented code block:

    nano /etc

Tagged code block:

{% code %}
code tag
code tag
code tag
{% endcode %}

{% note default %}
Note default tag.
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**

* Five
* Six
* Seven

{% note primary %}
{% youtube Kt7u5kr_P5o %}
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**

{% subtabs Sub Tabs %}
<!-- tab -->
**This is Sub Tab 1.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

{% note warning %}
Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.
{% endnote %}

Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub Tab 2.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

{% note danger %}
Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub Tab 3.**

{% subtabs Sub-Sub Tabs %}
<!-- tab -->
**This is Sub-Sub Tab 1 of Sub Tab 3.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub-Sub Tab 2 of Sub Tab 3.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

{% note warning %}
Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}

{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub-Sub Tab 3 of Sub Tab 3.**

{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

{% note warning %}
Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

{% note danger %}
Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}

{% endnote %}

{% endnote %}
<!-- endtab -->
{% endsubtabs %}

<!-- endtab -->
{% endsubtabs %}

<!-- endtab -->
{% endtabs %}


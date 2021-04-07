---
title: Latex基础(一)Latex特殊字符表
date: 2020-03-01 20:43:52
categories:
- Tech 
- Latex
tags: [Latex]
mathjax: true
urlname: latex_characters
keywords: [Latex, Writting, characters]
description:
---

{% note info %}

**说明**

本文主要记录了`Latex`中常用的特殊字符
{% endnote %}

{% note warning %}

**注意**

如果可能的话尽量避免在公式中出现`大括号#`以及类似的字符(这是保留字符)，这会导致渲染错误，处理起来比较麻烦
{% endnote %}

## 字体表

```latex
\begin{array}{ll|l}
 \texttt{"normal"}      &\texttt{}         & ABCDEFGHIJKLMNOPQRSTUVWXYZ\\
 \texttt{"blackboard"}  &\texttt{\mathbb}  &\mathbb{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
 \texttt{"boldface"}    &\texttt{\mathbf}  &\mathbf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
 \texttt{"typewriter"}  &\texttt{\mathtt}  &\mathtt{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
 \texttt{"roman"}       &\texttt{\mathrm}  &\mathrm{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
 \texttt{"sans-serif"}  &\texttt{\mathsf}  &\mathsf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
\end{array}
```


$$
\begin{array}{ll|l}
 \texttt{"normal"}      &\texttt{}         & ABCDEFGHIJKLMNOPQRSTUVWXYZ\\
 \texttt{"blackboard"}  &\texttt{\mathbb}  &\mathbb{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
 \texttt{"boldface"}    &\texttt{\mathbf}  &\mathbf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
 \texttt{"typewriter"}  &\texttt{\mathtt}  &\mathtt{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
 \texttt{"roman"}       &\texttt{\mathrm}  &\mathrm{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
 \texttt{"sans-serif"}  &\texttt{\mathsf}  &\mathsf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
\end{array}
$$

<!--more-->

{% note primary %}

**说明**

因为本文需要渲染公式较多，如果出现了公式未渲染的情况，请等待一会后刷新网页。

{% endnote %}



## 色彩表

```latex
\begin{array}{|lc|}
\hline
\color{black}{黑色}   \\
\color{darkgray}{深灰}\\
\color{gray}{灰色}    \\
\color{silver}{银色}  \\
\color{lightgray}{浅灰}\\
\color{white}{白色}   \\
\hline
\color{brown}{棕色}   \\
\color{maroon}{栗色}  \\
\color{red}{红色}     \\
\color{fuchsia}{桃红} \\
\color{magenta}{品红} \\
\color{pink}{粉红}    \\
\color{orange}{橙色}  \\
\color{yellow}{黄色}  \\
\color{lime}{青柠}    \\
\color{olive}{橄榄}   \\
\color{green}{绿色}   \\
\color{aqua}{水绿}    \\
\color{cyan}{青色}    \\
\color{teal}{靛青}    \\
\color{blue}{蓝色}    \\
\color{navy}{海蓝}    \\
\color{purple}{罗兰}  \\ 
\color{purple}{紫色}  \\ 
\hline
\end{array}
```

$$
\begin{array}{|lc|}
\hline
\color{black}{黑色}   \\
\color{darkgray}{深灰}\\
\color{gray}{灰色}    \\
\color{silver}{银色}  \\
\color{lightgray}{浅灰}\\
\color{white}{白色}   \\
\hline
\color{brown}{棕色}   \\
\color{maroon}{栗色}  \\
\color{red}{红色}     \\
\color{fuchsia}{桃红} \\
\color{magenta}{品红} \\
\color{pink}{粉红}    \\
\color{orange}{橙色}  \\
\color{yellow}{黄色}  \\
\color{lime}{青柠}    \\
\color{olive}{橄榄}   \\
\color{green}{绿色}   \\
\color{aqua}{水绿}    \\
\color{cyan}{青色}    \\
\color{teal}{靛青}    \\
\color{blue}{蓝色}    \\
\color{navy}{海蓝}    \\
\color{purple}{罗兰}  \\ 
\color{purple}{紫色}  \\ 
\hline
\end{array}
$$

## 连分数

```latex
x = a_0 + \cfrac{1^2}{a_1
        + \cfrac{2^2}{a_2
        + \cfrac{3^2}{a_3 
        + \cfrac{4^4}{a_4 + \cdots}}}}
```

$$
x = a_0 + \cfrac{1^2}{a_1
        + \cfrac{2^2}{a_2
        + \cfrac{3^2}{a_3 
        + \cfrac{4^4}{a_4 + \cdots}}}}
$$



```latex
\underset{j=1}{\overset{\infty}{\LARGE\mathrm K}}\frac{a_j}{b_j}
=\cfrac{a_1}{b_1
+\cfrac{a_2}{b_2
+\cfrac{a_3}{b_3
+\ddots}}}
```

$$
\underset{j=1}{\overset{\infty}{\LARGE\mathrm K}}\frac{a_j}{b_j}
=\cfrac{a_1}{b_1
+\cfrac{a_2}{b_2
+\cfrac{a_3}{b_3
+\ddots}}}
$$

```latex
x = a_0 + \frac{1^2}{a_1}+
          \frac{2^2}{a_2}+
          \frac{3^2}{a_3}+
          \frac{4^4}{a_4}+ \cdots
```

$$
x = a_0 + \frac{1^2}{a_1}+
          \frac{2^2}{a_2}+
          \frac{3^2}{a_3}+
          \frac{4^4}{a_4}+ \cdots
$$


## 线性代数

```latex
\begin{array}{ll}
 \texttt{\overline}&\overline{AAA}\\
 \texttt{\underline}&\underline{BBB}\\
 \texttt{\widetilde}&\widetilde{CCC}\\
 \texttt{\widehat}&\widehat{DDD}\\
 \texttt{\fbox}&\fbox{EEE}\\
\hline
 \texttt{\vec}&\vec{x}\ \mathrm{or}\ \vec{AB}\\
 \texttt{\check}&\check{x}\\
 \texttt{\acute}&\acute{x}\\
 \texttt{\grave}&\grave{x}\\
 \texttt{\bar}&\bar{x}\\
 \texttt{\hat}&\hat{x}\\
 \texttt{\tilde}&\tilde{x}\\
 \texttt{\mathring}&\mathring{x}\\
 \texttt{\dot}&\dot{x}\\
 \texttt{\ddot}&\ddot{x}\\
 \texttt{\dddot}&\dddot{x}\\
\end{array}
```

$$
\begin{array}{ll}
 \texttt{\overline}&\overline{AAA}\\
 \texttt{\underline}&\underline{BBB}\\
 \texttt{\widetilde}&\widetilde{CCC}\\
 \texttt{\widehat}&\widehat{DDD}\\
 \texttt{\fbox}&\fbox{EEE}\\
\hline
 \texttt{\vec}&\vec{x}\ \mathrm{or}\ \vec{AB}\\
 \texttt{\check}&\check{x}\\
 \texttt{\acute}&\acute{x}\\
 \texttt{\grave}&\grave{x}\\
 \texttt{\bar}&\bar{x}\\
 \texttt{\hat}&\hat{x}\\
 \texttt{\tilde}&\tilde{x}\\
 \texttt{\mathring}&\mathring{x}\\
 \texttt{\dot}&\dot{x}\\
 \texttt{\ddot}&\ddot{x}\\
 \texttt{\dddot}&\dddot{x}\\
\end{array}
$$



```latex
\begin{pmatrix}
 1 & a_1 & a_1^2 & \cdots & a_1^n \\
 1 & a_2 & a_2^2 & \cdots & a_2^n \\
 \vdots  & \vdots& \vdots & \ddots & \vdots \\
 1 & a_m & a_m^2 & \cdots & a_m^n \\
\end{pmatrix}
```

$$
\begin{pmatrix}
 1 & a_1 & a_1^2 & \cdots & a_1^n \\
 1 & a_2 & a_2^2 & \cdots & a_2^n \\
 \vdots  & \vdots& \vdots & \ddots & \vdots \\
 1 & a_m & a_m^2 & \cdots & a_m^n \\
\end{pmatrix}
$$



```latex
\begin{array}{ll}
 \texttt{\overline}&\overline{AAA}\\
 \texttt{\underline}&\underline{BBB}\\
 \texttt{\widetilde}&\widetilde{CCC}\\
 \texttt{\widehat}&\widehat{DDD}\\
 \texttt{\fbox}&\fbox{EEE}\\
\hline
 \texttt{\vec}&\vec{x}\ \mathrm{or}\ \vec{AB}\\
 \texttt{\check}&\check{x}\\
 \texttt{\acute}&\acute{x}\\
 \texttt{\grave}&\grave{x}\\
 \texttt{\bar}&\bar{x}\\
 \texttt{\hat}&\hat{x}\\
 \texttt{\tilde}&\tilde{x}\\
 \texttt{\mathring}&\mathring{x}\\
 \texttt{\dot}&\dot{x}\\
 \texttt{\ddot}&\ddot{x}\\
 \texttt{\dddot}&\dddot{x}\\
\end{array}
```

$$
\begin{array}{ll}
 \texttt{\overline}&\overline{AAA}\\
 \texttt{\underline}&\underline{BBB}\\
 \texttt{\widetilde}&\widetilde{CCC}\\
 \texttt{\widehat}&\widehat{DDD}\\
 \texttt{\fbox}&\fbox{EEE}\\
\hline
 \texttt{\vec}&\vec{x}\ \mathrm{or}\ \vec{AB}\\
 \texttt{\check}&\check{x}\\
 \texttt{\acute}&\acute{x}\\
 \texttt{\grave}&\grave{x}\\
 \texttt{\bar}&\bar{x}\\
 \texttt{\hat}&\hat{x}\\
 \texttt{\tilde}&\tilde{x}\\
 \texttt{\mathring}&\mathring{x}\\
 \texttt{\dot}&\dot{x}\\
 \texttt{\ddot}&\ddot{x}\\
 \texttt{\dddot}&\dddot{x}\\
\end{array}
$$



```latex
\begin{pmatrix}
 1 & a_1 & a_1^2 & \cdots & a_1^n \\
 1 & a_2 & a_2^2 & \cdots & a_2^n \\
 \vdots  & \vdots& \vdots & \ddots & \vdots \\
 1 & a_m & a_m^2 & \cdots & a_m^n \\
\end{pmatrix}
```


$$
\begin{pmatrix}
 1 & a_1 & a_1^2 & \cdots & a_1^n \\
 1 & a_2 & a_2^2 & \cdots & a_2^n \\
 \vdots  & \vdots& \vdots & \ddots & \vdots \\
 1 & a_m & a_m^2 & \cdots & a_m^n \\
\end{pmatrix}
$$


```latex
\left[
\begin{array}{cc|c}
  1&2&3\\
  4&5&6\\
\end{array}
\right]
```

$$
\left[
\begin{array}{cc|c}
  1&2&3\\
  4&5&6\\
\end{array}
\right]
$$

```latex
\begin{cases}
%线性方程组加\\[2ex],不然会挤在一起.
 a_1x+b_1y+c_1z=\frac{p_1}{q_1} \\[2ex] 
 a_2x+b_2y+c_2z=\frac{p_2}{q_2} \\[2ex] 
 a_3x+b_3y+c_3z=\frac{p_3}{q_3}
\end{cases}
```

$$
\begin{cases}
 a_1x+b_1y+c_1z=\frac{p_1}{q_1} \\[2ex] 
 a_2x+b_2y+c_2z=\frac{p_2}{q_2} \\[2ex] 
 a_3x+b_3y+c_3z=\frac{p_3}{q_3}
\end{cases}
$$



```latex
%约去符,删除线
\require{cancel}
\require{enclose}
\begin{array}{ll}
 \verb|y+\cancel{x}| & y+\cancel{x}\\
 \verb|y+\bcancel{x}| & y+\bcancel{x}\\
 \verb|y+\xcancel{x}| & y+\xcancel{x}\\
 \verb|y+\cancelto{0}{x}| & y+\cancelto{0}{x}\\
 \verb+\frac{1\cancel9}{\cancel95} = \frac15+& \frac{1\cancel9}{\cancel95} = \frac15 \\
 \verb|\enclose{horizontalstrike}{x+y}| & \enclose{horizontalstrike}{x+y}\\
 \verb|\enclose{verticalstrike}{\frac xy}| & \enclose{verticalstrike}{\frac xy}\\
 \verb|\enclose{updiagonalstrike}{x+y}| & \enclose{updiagonalstrike}{x+y}\\
 \verb|\enclose{downdiagonalstrike}{x+y}| & \enclose{downdiagonalstrike}{x+y}\\
\end{array}
```

$$
\require{cancel}
\require{enclose}
\begin{array}{ll}
 \verb|y+\cancel{x}| & y+\cancel{x}\\
 \verb|y+\bcancel{x}| & y+\bcancel{x}\\
 \verb|y+\xcancel{x}| & y+\xcancel{x}\\
 \verb|y+\cancelto{0}{x}| & y+\cancelto{0}{x}\\
 \verb+\frac{1\cancel9}{\cancel95} = \frac15+& \frac{1\cancel9}{\cancel95} = \frac15 \\
 \verb|\enclose{horizontalstrike}{x+y}| & \enclose{horizontalstrike}{x+y}\\
 \verb|\enclose{verticalstrike}{\frac xy}| & \enclose{verticalstrike}{\frac xy}\\
 \verb|\enclose{updiagonalstrike}{x+y}| & \enclose{updiagonalstrike}{x+y}\\
 \verb|\enclose{downdiagonalstrike}{x+y}| & \enclose{downdiagonalstrike}{x+y}\\
\end{array}
$$

## 数学符号表

### 数学模式重音符

```latex
\hat{a} \check{a} \tilde{a} \acute{a}
\grave{a} \dot{a} \ddot{a} \breve{a}
\bar{a} \vec{a} \widehat{A} \widetilde{A}
```

$$
\hat{a} \check{a} \tilde{a} \acute{a}
\grave{a} \dot{a} \ddot{a} \breve{a}
\bar{a} \vec{a} \widehat{A} \widetilde{A}
$$

### 小写希腊字母

![image-20200320151609176](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20200320151609176.png)

### 大写希腊字母

![image-20200320151628633](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20200320151628633.png)

### 二元关系符

![image-20200320151701880](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20200320151701880.png)

### 二元运算符

![image-20200320151727539](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20200320151727539.png)

### 大尺寸运算符

![image-20200320151743230](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20200320151743230.png)

### 箭头

![image-20200320151755631](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20200320151755631.png)

### 定界符

![image-20200320151807633](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20200320151807633.png)

### 大尺寸定界符

![image-20200320151824258](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20200320151824258.png)

### 其他符号

![image-20200320151849212](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20200320151849212.png)

#### 非数学符号

![3-11](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/20180110120814709)

#### AMS 定界符

![3-12](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/20180110120845203)

#### AMS 希腊和希伯来字母

![3-13](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/20180110120857003)

#### AMS 二元关系符

![3-14](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/20180110120908923)

#### AMS 箭头

![3-15](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/20180110120921290)

#### AMS 二元否定关系符和箭头

![3-16](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/20180110120934677)

#### AMS 二元运算符

![3-17](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/20180110120948160)

#### AMS 其它符号

![3-18](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/20180110121000205)

#### 数学字母

![3-19](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/20180110121011781)
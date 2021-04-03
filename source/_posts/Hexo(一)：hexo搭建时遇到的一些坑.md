---
title: Hexo踩坑(一)
urlname: Hexo(1)
date: 2021-4-3 13:20:00
categories: [Hexo]
tags: [Hexo, Yaml, Configuration]
---

## 1. yaml配置文件

一定要注意：yaml配置文件也是有其固定格式的，特别是要注意空格。

#### 经典报错：

```
can not read a block mapping entry; a multiline key may not be an implicit key
```

<!------more------>

#### 我犯的错误：

在配置SEO，修改 `theme/next/_config.yml`

```yaml
# 错误案例
# Google Webmaster tools verification.
# See: https://developers.google.com/search
google_site_verification:vBZBS_Ucyk1uWpkEaY8rOwJx0vIi2CVILoSATSjHr-k

# Bing Webmaster tools verification.
# See: https://www.bing.com/webmasters
bing_site_verification:0A53450D60EE95103C2117D5737EA0C7 

# Yandex Webmaster tools verification.
# See: https://webmaster.yandex.ru
yandex_site_verification: 

# 正确案例
# Baidu Webmaster tools verification.
# See: https://ziyuan.baidu.com/site
baidu_site_verification: code-snl66xrgB7
```


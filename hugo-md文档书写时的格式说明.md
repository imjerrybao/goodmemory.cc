---
title: "hugo-md文档书写时的格式说明"
description: "文章详细介绍在hugo下书写markdown时的格式和字段问题，如果你想使用hugo，这个将是必看的文章之一"
tags: [ "hugo" ]
date: "2015-12-17"
url: /hugo-md文档书写时的格式说明/
categories:
  - "go"
slug: ""

---

# 前言

在决定使用自动化流程后，第一个面临的问题就是，这个文档头的格式到底是什么样的，因为现在你要手写，就需要彻底搞清楚，
以便达到正确和高效。

阅读查找了gohugo.io的所有相关页面，找到以下两个相关的内容基本上说的很清楚了：
[https://gohugo.io/content/front-matter/](https://gohugo.io/content/front-matter/)
[https://gohugo.io/content/archetypes/](https://gohugo.io/content/archetypes/)

# 头格式

md只是文档的类型，但是里面的内容遵循怎样的格式呢？
hugo目前支持3中toml，yaml，json，三种格式的文件头。识别符号分别如下
* toml: +++
* yaml: ---
* json: {}

toml示例：

<pre>
+++
title = "spf13-vim 3.0 release and new website"
description = "spf13-vim is a cross platform distribution of vim plugins and resources for Vim."
tags = [ ".vimrc", "plugins", "spf13-vim", "vim" ]
date = "2012-04-06"
categories = [
  "Development",
  "VIM"
]
slug = "spf13-vim-3-0-release-and-new-website"
+++

Content of the file goes Here
</pre>

yaml示例：

<pre>
---
title: "spf13-vim 3.0 release and new website"
description: "spf13-vim is a cross platform distribution of vim plugins and resources for Vim."
tags: [ ".vimrc", "plugins", "spf13-vim", "vim" ]
date: "2012-04-06"
categories:
  - "Development"
  - "VIM"
slug: "spf13-vim-3-0-release-and-new-website"
---

Content of the file goes Here
</pre>

json示例：

<pre>
{
    "title": "spf13-vim 3.0 release and new website",
    "description": "spf13-vim is a cross platform distribution of vim plugins and resources for Vim.",
    "tags": [ ".vimrc", "plugins", "spf13-vim", "vim" ],
    "date": "2012-04-06",
    "categories": [
        "Development",
        "VIM"
    ],
    "slug": "spf13-vim-3-0-release-and-new-website",
}

Content of the file goes Here
</pre>

# 字段变量
文档可以包含很多变量。

## 必要字段
* tile: 内容的标题
* description: 内容的描述
* date:日期
* taxonomies:分类字段，包括tag和categories

## 可选字段
* aliases: [别名](https://gohugo.io/extras/aliases/)
* daft: 是否是草稿
* publishdate: 定时未来发布的时间
* type: 内容的格式，可以从内容自动识别
* isCJKLanguage：是否时CJK
* weight: 排序的权重
* markup: 时markdown格式还是reStructuredText
* slug: url尾部的token
* url: 完整的url

# 附

[hugo markdown引擎的配置](http://gohugo.io/overview/configuration/#configure-blackfriday-rendering:a66b35d20295cb764719ac8bd35837ec)

finish

---
layout: page
title: 首页
tagline: 一个神奇的网站
group: navigation
---
{% include JB/setup %}

阅读 [Jekyll 快速上手](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)

完全使用手册: [Jekyll Bootstrap](http://jekyllbootstrap.com)

## 更新作者属性

记得在 `_config.yml` 定义你自己的属性:

    title : My Blog =)

    author :
      name : Name Lastname
      email : blah@email.test
      github : username
      twitter : username

主题模板可以在任何需要的时候，引用这些参数。

## 文章示例

这个博客包含文章示例，来帮助展示页面和博客数据。

如果你不再需要这些示例，直接删除文件夹`_posts/core-samples`

    $ rm -rf _posts/core-samples

这里是一个"文章列表"示例：

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## 下一步行动

这个主题还未完成，如果你想成为贡献者，[请fork](http://github.com/plusjade/jekyll-bootstrap)！

我们需要清理主题，用主题特定的标记示例制作主题使用指南。

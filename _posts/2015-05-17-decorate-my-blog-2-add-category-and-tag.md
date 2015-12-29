---
layout: post
title: 博客装修记(2)——为博客添加分类和标签
category: 博客装修记
tags: [github-pages, jekyll]
summary: 简单的博客搭建完成，可以开始写文章啦~可是纵观整个博客主题，文章页面居然没有分类和标签(◞‸◟)
---

####插件or手动添加
说到给博客添加分类和标签功能，最简单的方法当然是……使用一个带分类和标签功能的Jekyll主题~然而好折腾的我们显然不满意——“教练，有没有更麻烦的方法？”这样的话也可以选择引入一个分类标签插件，然而我们还不满意——
> “教练，我们想要diy！”

---
####认识Liquid
[Liquid](http://docs.shopify.com/themes/liquid-basics)是Jekyll使用的模板语言，它是一种基于Ruby的、非常简单的语言。Liquid的语法详见前面的链接，这里不赘述。

不过，关于Liquid，有一点需要注意：

* 语句用\{ \}包裹，而对象用\{\{ \}\}包裹（改了好久bug发现是括号问题让人忧郁）。

---
####在文章中添加分类和标签
这部分主要参照这位德国小哥[Stephan Groß](http://www.minddust.com)的博文[How To Use Tags And Categories On Github Pages Without Plugins](http://www.minddust.com/post/tags-and-categories-on-github-pages)。

#####分类Category
*Step 1:* 在\_layouts目录下的post.html中,

```html
{% raw %}
{% if page.update_date %}
  <span class="post-meta post-updated">Updated: {{ page.update_date | date: "%b %-d, %Y" }}</span><br>
{% endif %}
{% endraw %}
```
这段代码后添加如下代码

```html
{% raw %}
{% if post.category %}
      {% for site_category in site.data.categories %}
          {% if site_category.slug == post.category %}
              {% assign category = site_category %}
          {% endif %}
      {% endfor %}
      {% if category %}
          {% capture category_content %}<i class="fa fa-book">: <span class="category_label" style="background: {{ category.color }}"><a href="/blog/category/{{ category.slug }}/">{{ category.name }}</a></span></i>{% endcapture %}
      {% endif %}
  {% else %}
      {% assign category_content = '' %}
  {% endif %}
{% endraw %}
```

*Step 2:* 在\_layouts目录下新建一个名为blog_by_category.html的模版文件，内容如下：

```html
{% raw %}
---
layout: default
---

<span style="width: 100px; height: 100px; background: #000000;"></span>
<header id="post-header">
    <h1 id="post-title">{{ page.title }}</h1>
</header>

<div id="post-content">
    {% if site.categories[page.category] %}
        {% for post in site.categories[page.category] %}
            {% capture post_year %}{{ post.date | date: '%Y' }}{% endcapture %}
            {% if forloop.first %}
                <h3>{{ post_year }}</h3><div class="list-group">
            {% endif %}
			
            {% if forloop.first == false %}
                {% assign previous_index = forloop.index0 | minus: 1 %}
                {% capture previous_post_year %}{{ site.categories[page.category][previous_index].date | date: '%Y' }}{% endcapture %}
                {% if post_year != previous_post_year %}
                    </div><h3>{{ post_year }}</h3><div class="list-group">
                {% endif %}
            {% endif %}
			
            <a href="{{ post.url }}/" class="list-group-item">
                <h4 class="list-group-item-heading">{{ post.title }}</h4>
            </a>

            {% if forloop.last %}
                </div>
            {% endif %}
        {% endfor %}
    {% else %}
        <p>该分类下暂无文章.</p>
    {% endif %}
</div>
{% endraw %}
```

*Step3:* 回到\_layouts目录下的post.html中，在Step 1中新添代码之后再添加如下代码：

```html
{% raw %}
<span class="post-meta post-category-and-tag">{{ category_content }}</span>
{% endraw %}
```

这样，博文中就有了显示分类的功能。可喜可贺～
可是机智如你发现问题又来了：分类可以显示，但没法设定啊(´･_･`)，所以我们需要继续设置分类名称。

*Step4:* 新建名为blog的目录，在其中新建Category目录。该目录中存放所有分类。对每一个分类都要新建一个md文件，文件名称即为你想要的分类名称（比如我们要建一个名为“绅♂士♂”的分类），文件内容如下：

```html
---
layout: blog_by_category
title: 绅♂士♂
category: 绅♂士♂
permalink: /blog/category/绅♂士♂/
---
```

*Step5:* 对于每一篇博文，文章头部增加category字段，例如：

```html
---
layout: post
title: 论比利王对哲学的改革
category: 绅♂士♂
---
```

至此，终于完成了为文章设定分类的任务。










---
layout: post
title: 博客装修记(2)——为博客添加分类和标签
category: 博客装修记
tags: [github-pages, jekyll]
summary: 简单的博客搭建完成，可以开始写文章啦~可是纵观整个博客主题，文章页面居然没有分类和标签(◞‸◟)

---

#### 插件or手动添加

说到给博客添加分类和标签功能，最简单的方法当然是……使用一个带分类和标签功能的Jekyll主题~然而好折腾的我们显然不满意——“教练，有没有更麻烦的方法？”这样的话也可以选择引入一个分类标签插件，然而我们还不满意——
> “教练，我们想要diy！”

---

#### 认识Liquid

[Liquid](http://docs.shopify.com/themes/liquid-basics)是Jekyll使用的模板语言，它是一种基于Ruby的、非常简单的语言。Liquid的语法详见前面的链接，这里不赘述。

不过，关于Liquid，有一点需要注意：

* 语句用\{ \}包裹，而对象用\{\{ \}\}包裹（改了好久bug发现是括号问题让人忧郁）。

---

#### 在文章中添加分类和标签

这部分主要参照这位德国小哥[Stephan Groß](http://www.minddust.com)的博文[How To Use Tags And Categories On Github Pages Without Plugins](http://www.minddust.com/post/tags-and-categories-on-github-pages)。

##### 分类Category

*Step 1:* 在\_layouts目录下的post.html中,

~~~html
{% raw %}
{% if page.update_date %}
  <span class="post-meta post-updated">Updated: {{ page.update_date | date: "%b %-d, %Y" }}</span><br>
{% endif %}
{% endraw %}
~~~
这段代码后添加如下代码

~~~html
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
~~~

*Step 2:* 在\_layouts目录下新建一个名为blog\_by\_category.html的模版文件，内容如下：

~~~html
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
~~~

*Step3:* 回到\_layouts目录下的post.html中，在Step1中新添代码之后再添加如下代码：

~~~html
{% raw %}
<span class="post-meta post-category-and-tag">{{ category_content }}</span>
{% endraw %}
~~~

这样，博文中就有了显示分类的功能。可喜可贺～
可是机智如你发现问题又来了：分类可以显示，但没法设定啊(´･_･`)，所以我们需要继续设置分类名称。

*Step4:* 新建名为blog的目录，在其中新建category目录。该目录中存放所有分类。对每一个分类都要新建一个md文件，文件名称即为你想要的分类名称（比如我们要建一个名为“绅♂士♂”的分类），文件内容如下：

~~~html
---
layout: blog_by_category
title: 绅♂士♂
category: 绅♂士♂
permalink: /blog/category/绅♂士♂/
---
~~~

*Step5:* 对于每一篇博文，文章头部增加category字段，例如：

~~~html
---
layout: post
title: 论比利王对哲学的改革
category: 绅♂士♂
---
~~~

*Step6:* 要将文章对分类的设定与其真正的分类联系起来，还需要在项目目录中新建\_data目录，并在其中新建名为categories的yml文件，每新增一种分类，就需要在该文件中添加如下代码：

~~~html
- slug: 绅♂士♂
  name: 绅♂士♂
  color: '#94BFDA'
~~~
其中的color字段对应Step1中对category背景颜色的设定，可以不设置。

##### 标签Tag

标签的设定与分类极为相似。

*Step1:* 在添加分类的Step1中添加的代码之后新增如下代码：

~~~html
{% raw %}
{% if post.tags.size > 0 %}
      {% capture tags_content %} &nbsp;&nbsp;&nbsp;{% if post.tags.size == 1 %}<i class="fa fa-tag"></i>: {% else %}<i class="fa fa-tags"></i>{% endif %}: {% endcapture %}
      {% for post_tag in post.tags %}
          {% for data_tag in site.data.tags %}
              {% if data_tag.slug == post_tag %}
                  {% assign tag = data_tag %}
              {% endif %}
          {% endfor %}
          {% if tag %}
              {% capture tags_content_temp %}{{ tags_content }}<span class="tag_label"><a href="/blog/tag/{{ tag.slug }}/">{{ tag.name }}</a></span>{% if forloop.last == false %}, {% endif %}{% endcapture %}
              {% assign tags_content = tags_content_temp %}
          {% endif %}
      {% endfor %}
  {% else %}
      {% assign tags_content = '' %}
  {% endif %}
{% endraw %}
~~~

*Step2:* 同样在\_layouts目录下新建一个名为blog\_by\_tag.html的模版文件，内容如下：

~~~html
{% raw %}
---
layout: default
---

<header id="post-header">
    <h1 id="post-title">{{ page.title }}</h1>
</header>

<div id="post-content">
    {% if site.tags[page.tag] %}
        {% for post in site.tags[page.tag] %}
            {% capture post_year %}{{ post.date | date: '%Y' }}{% endcapture %}
            {% if forloop.first %}
                <h3>{{ post_year }}</h3><div class="list-group">
            {% endif %}
			
            {% if forloop.first == false %}
                {% assign previous_index = forloop.index0 | minus: 1 %}
                {% capture previous_post_year %}{{ site.tags[page.tag][previous_index].date | date: '%Y' }}{% endcapture %}
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
        <p>该标签下暂无文章.</p>
    {% endif %}
</div>
{% endraw %}
~~~

*Step3:* 将添加分类的Step3中新增的代码改为

~~~html
{% raw %}
  <span class="post-meta post-category-and-tag">{{ category_content }}{{ tags_content }}</span>
{% endraw %}
~~~

*Step4:* 在blog目录中新建tag目录，该目录中存放所有标签。对每一个标签都要新建一个html文件，文件名称即为你想要的标签名称（比如我们要建一个名为“比利”的标签），文件内容如下：

~~~html
---
layout: blog_by_tag
title: 比利
category: 比利
permalink: /blog/tag/比利/
---
~~~

*Step5:* 对于每一篇博文，文章头部增加tags字段，例如：

~~~html
---
layout: post
title: 论比利王对哲学的改革
category: 绅♂士♂
tags: [比利, 哲学]
---
~~~

*Step6:* 同样在\_data目录中新建名为tags的yml文件。每添加一种标签，就在该文件中对应添加：

~~~html
- slug: 比利
  name: 比利 
~~~

注意每篇文章的分类category只有一个，而标签tags则有多个哟～

---
呼～为文章添加分类和标签到此基本完成，如果还有疑惑，欢迎查看本教练的[代码实现](https://github.com/ErythroME/ErythroME.github.io)或给我留言～









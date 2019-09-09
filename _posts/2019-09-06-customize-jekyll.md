---
layout: post
title: 细节之调教Jekyll
permalink: "/blog-with-github-pages/customize-jekyll/"
keywords:
- Jekyll
- Liquid
- Html
- CSS
date: 2019-09-06 14:56 +0800
---
> 天下难事，必做于易；天下大事，必做于细。——老子

### 你看，填空题
Jekyll站点的常见结构：
{% highlight bash %}
.
├── _config.yml
├── _data
|   └── members.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.md
|   └── on-simplicity-in-technology.md
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
|   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
|   ├── _base.scss
|   └── _layout.scss
├── _site
├── .jekyll-metadata
└── index.html # can also be an 'index.md' with valid front matter
{% endhighlight %}

Jekyll的配置性还不错，site scope的配置都在_config.yml里面，看着改就是了。因为技术原因这个文件不能热加载，修改完成后重启一下serve进程就能看到变更。

### 更多定制
#### 给文章页加上关键字
创建页面 `_includes/keywords.html` 如下：
{% highlight html %}
{% raw %}
<!-- file path: _includes/keywords.html -->
{%- if page.keywords -%}
<keywords>
    {% for kw in page.keywords %}
    <code class="highlighter-rouge">{{ kw }}</code>
    {% endfor %}
</keywords>
<span>&nbsp;</span>
{%- endif -%}
{% endraw %}
{% endhighlight %}
编辑 `_layout/post.html` ，添加一行：

{% highlight html %}
{% raw %}
<!-- file path: _layout/post.html -->
<header class="post-header">
    <h1 class="post-title p-name" itemprop="name headline">{{ page.title | escape }}</h1>
    <p class="post-meta">
        {%- include keywords.html -%} <!-- 修改了这里 -->
        
        <time class="dt-published" datetime="{{ page.date | date_to_xmlschema }}" itemprop="datePublished">
            {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
            {{ page.date | date: date_format }}
        </time>
        {%- if page.author -%}
        • <span itemprop="author" itemscope itemtype="http://schema.org/Person"><span class="p-author h-card" itemprop="name">{{ page.author | escape }}</span></span>
        {%- endif -%}</p>
</header>
{% endraw %}
{% endhighlight %}
效果如下：
{% include keywords.html keywords=page.keywords %}

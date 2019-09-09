---
layout: post
title: 搭建Jekyll环境
permalink: "/blog-with-github-pages/setup-jekyll/"
keywords:
- Macos
- Homebrew
- Ruby
- Jekyll
date: 2019-09-06 11:20 +0800
---
![老师走一个](/assets/20190905/mr.jpg)

来吧!

{% highlight bash %}
# install rbenv
brew update
brew inistall rbenv

# install plugins for rbenv
git clone https://github.com/ianheggie/rbenv-binstubs.git "$(rbenv root)/plugins/rbenv-binstubs"
# speedup downloading with ruby-china mirror
git clone https://github.com/andorchen/rbenv-china-mirror.git "$(rbenv root)"/plugins/rbenv-china-mirror

rbenv rehash

# list avaiable versions
rbenv install -l
## Output:
# ...
# 2.6.2
# 2.6.3
# 2.6.4
# ...

# choose a version and install
rbenv install 2.6.4

# enable rbenv auto loading
echo 'eval "$(rbenv init -)"'  >> .~/bash_profile

# install jekyll
gem install bundler jekyll
jekyll new my-awesome-site
cd my-awesome-site
{% endhighlight %}

至此，基本的环境准备完毕。走一个：

`bundle exec jekyll serve`

猛击： [http://localhost:4000](http://localhost:4000)， 诸君武运昌隆！
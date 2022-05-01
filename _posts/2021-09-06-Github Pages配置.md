# 准备工作

## git准备

    git init <REPOSITORY-NAME>
    #<REPOSITORY-NAME>=<USER>.github.io
    cd <REPOSITORY-NAME>

## jekyll准备

    jekyll new .                                #初始化当前文件夹

## 安装MM(Gems Base)

进入Jekyll创建好的website目录。编辑`Gemfile`

```
gem "minimal-mistakes-jekyll"
gem "jekyll-include-cache"                      #依赖的插件
```

更新Gems

    bundle update

查看安装的gem所在路径

    bundle show minimal-mistakes-jekyll

把相关的文件、文件夹复制到当前文件夹

    cp cp -rf /home/yodh/gems/gems/minimal-mistakes-jekyll-4.24.0/* .

删除`CHANGELOG.md`和`README.md`

从[MM的repo](https://github.com/mmistakes/minimal-mistakes)复制`.gitignore`和`_config.yml`

    wget -N https://raw.githubusercontent.com/mmistakes/minimal-mistakes/master/.gitignore
    wget -N https://raw.githubusercontent.com/mmistakes/minimal-mistakes/master/_config.yml

创建`CNAME`

    ladeo.net

※还需要在github的pages设定里开启`Enforce HTTPS`

在`_config.yml`配置

```yml
theme: minimal-mistakes-jekyll                  #选择Theme
plugins:
  - jekyll-include-cache                        #追加插件
```

※`Remote theme`安装方式不做说明。

## git提交

    git add .
    git commit -m 'Initial GitHub pages site with Jekyll'
    git remote add origin git@github.com:<USER>/<USER>.github.io.git
    git push -u origin BRANCH                   #<BRANCH>=master

因为之前配置过github pages，远程已经存在了名为`main`的branch。需要把default branch切换为master。
再把main这个分支删除。最后把master重命名为main。
再把本地的目录删除，重新从远程拉取。

※git push之后github有时候并不会立刻进行rebuild！页面无法立即变化。

## 测试

    bundle exec jekyll serve -w --host=0.0.0.0

测试页面`http://ip:4000`

# Jekyll Theme

[minimal-mistakes](https://github.com/mmistakes/minimal-mistakes)目前github上stars数量最多的Theme。

## 推送本地代码到github

    git add .
    git commit -m "Initial Jekyll"

# 配置MM

[官方配置说明](https://mmistakes.github.io/minimal-mistakes/docs/configuration/)

※使用浏览器的inspection功能查找页面元素对应的css，对css进行修改。

编辑`_config.yml`

## css

[Style Sheet](https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/)

`assets/css/main.scss`的配置会覆盖`_sass`里的配置

## 字体配置

- webfonts
  - [Adobe TypeKit](https://fonts.adobe.com/typekit)
  - [Google Fonts](https://fonts.google.com)
  
更新font stacks，把script添加到`_includes/head/custom.html`

```
/* system typefaces */
$serif      : "宋体", "Source Han Serif", Georgia, Times, serif;
$sans-serif : "微软雅黑", "Source Han Sans", -apple-system, BlinkMacSystemFont, "Roboto", "Segoe UI", "Helvetica Neue", "Lucida Grande", Arial, sans-serif;
$monospace  : "Noto Sans CJK", Monaco, Consolas, "Lucida Console", monospace;
```

※需要填写在`@import`之前

## 修改字体大小

配置文件`_sass/minimal-mistakes/_variables.scss`

    sed -i "s/1em/0.75em/g" `grep 1em -rl _sass/minimal-mistakes`

## 发布文章

markdown文件要放在`_posts`目录里， 文章的格式 YYYY-MM-DD-TITLES.markdown

```yml
---
layout: post
title:  "Welcome to Jekyll!"
date:   2021-09-06 11:58:16 +0000
categories: jekyll update
---
```

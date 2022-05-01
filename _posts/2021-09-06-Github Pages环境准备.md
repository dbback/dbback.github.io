- Key Words:
  - Github Pages(gh-pages)
  - Cloudflare(CF)
  - Jekyll
  - Jekyll Theme(minimal-mistakes)

# Github Pages

## 创建专用Repo

1. 点击Github页面右上角用户头像。
2. 在下拉菜单选择`Your Repositories`。
3. 点击界面右侧`New`按钮。
4. `Repository Name`填写新Repo的名称。Repo可见性选择Public(Private需要是收费用户)。

## 两种Pages模式

1. User/Organization Pages
Repo的名字必须是：`<yourname>.github.io`(比如: ladeo.github.io)。
适合作为个人网站，本文采用这种模式。

2. Project Pages
这是针对开发项目的Pages，本文不采用这种模式。

完成Repo创建

## 配置Pages

进入刚创建的Repo(ladeo.github.io)。点击`Settings`，在左侧选择`Pages`。
`Theme Chooser`选择一个Jekyll主题。

确认自己Pages(https://ladeo.github.io)可以访问。

# Cloudflare

## 添加DNS Record

进入域名(ladeo.net)的管理界面。需要修改2种记录。

`CNAME`记录对应`www子域名`(www.ladeo.net)

    www -> ladeo.github.io

`A`记录对应`apex域名`(ladeo.net)

    ladeo.net -> 185.199.108.153
    ladeo.net -> 185.199.109.153
    ladeo.net -> 185.199.110.153
    ladeo.net -> 185.199.111.153

※添加DNS Record时，`Proxy status`先选择为`DNS only`(不使用CF的CDN)。

## Github配置

回到Github的Repo(ladeo/ladeo.github.io)的`Settings`，进入`Pages`进行配置。
`Custom domain`填写自己域名(ladeo.net)后保存`save`。Repo里会新增一个名为CNAME的文件，内容是自己域名(ladeo.net)。
`Enforce HTTPS`勾选生效。

## 开启CF的CDN

※如果直接访问github速度不错，就不用开启CF的CDN。
在CF的DNS管理界面，把`Proxy status`选择为`Proxied`。

[速度测试网站](https://tool.chinaz.com/sitespeed)对比CDN开启前后的速度。

## 浏览器访问失败

报错信息如下：

> The page isn’t redirecting properly
> ERR_TOO_MANY_REDIRECTS

在CF控制面板里选中自己域名，在`SSL\TLS`APP中把`SSL/TLS encryption mode`修改为`FULL`。

[Troubleshooting redirect loop errors](https://support.cloudflare.com/hc/en-us/articles/115000219871-Troubleshooting-redirect-loop-errors-)

# Jekyll

Jekyll是基于Ruby的静态网页生成器。
在本地PC(ubuntu 20.04)上安装。

## 准备所需环境

    sudo apt-get install ruby-full build-essential zlib1g-dev

编辑`~/.bashrc`

```bash
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## 替换gems源

ruby-china、清华二选一

```shell
gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
gem sources --add https://mirrors.tuna.tsinghua.edu.cn/rubygems/ --remove https://rubygems.org/
gem sources -l                                              #确认更换结果
```

或者编辑`~/.gemrc`的`sources`字段。

## 安装bundler

    gem install jekyll bundler

`bundler`可以为Ruby项目提供一贯的运行环境(感觉类似python的pyenv)。配置文件是`Gemfile`。

## 替换bundler源

```
bundle config mirror.https://rubygems.org https://mirrors.tuna.tsinghua.edu.cn/rubygems
bundle config mirror.https://rubygems.org https://gems.ruby-china.com
```

或者编辑`Gemfile`的`sources`字段。

## 创建新网站

实际上gh-pages后台就运行着Jekyll。但是[版本](https://pages.github.com/versions)不是最新的。

```shell
jekyll new website                                #初始化jekyll
cd website
bundle exec jekyll serve                          #访问地址http://127.0.0.1:4000
bundle exec jekyll serve -w --host=0.0.0.0        #可以从局域网其他PC测试
```

## 用bundler安装gems

编辑`Gemfile`，添加需要的gem

    gem "jekyll"

安装/更新

    bundle install                                #安装所有依赖的gems
    bundle update                                 #更新
    
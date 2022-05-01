github pages 在：技术来自于 [Jekyll](https://jekyllrb.com/) & [Minimal Mistakes](https://mademistakes.com/work/minimal-mistakes-jekyll-theme/).

https://github.com/mypppv/mypppv.github.io

以下针对这个进行设置，使谷歌可以搜索

1、设置 ：google_site_verification，需要修改 config.yml



`google_site_verification : TqJIq5GkHS9ItlV3nrV7XKVK2112121219oNhrzFMctI`



2、检查是否被收录

----------

首先查看你的博客地址是否已经被 Google 收录，在 Google 的搜索栏中搜索：

> site:https://xxxx.github.io

其中`https://xxxx.github.io`为你的博客地址，如果结果是`尝试使用Google Search Console`，则意味着没有被收录。

如果搜索出你想要的结果，那么不用继续往下看了。

3. 搜索资源提交

---------

进入 Google Web Master，点击：[Google Search Console](https://www.google.com/webmasters/tools/home?hl=zh-CN)（若未登录谷歌账号，需要先登录谷歌账号）

点击添加，提交你的博客网址，然后跳转到如下界面进行验证。

这里需要验证网站所有权，有多种方法进行验证，网站给我们提示了一个推荐验证方法是：通过在你的网站上添加一个它提供的 html 文件来验证。

![](https://evanli.github.io/img/20181025/verify-method.jpg)

下载该文件，上传到你的 Github Pages 的根目录，然后点击验证，即可通过验证。

![](https://evanli.github.io/img/20181025/verify-completed.jpg)

或者也可通过其他方法进行验证，比如不想在根目录添加 html 文件的话，可以选择在网站首页添加元标记，即在_includes 目录下的 head.html 中的 head 标签之间添加如下元标记即可。

![](https://evanli.github.io/img/20181025/other-verify-method.jpg)

4.添加站点地图

---------

站点地图 (Site Map) 是用来注明网站结构的文件，我们希望搜索引擎的爬虫了解我们的网站结构, 以便于高效爬取内容，快速建立索引。

*   点击进入 [XML-Sitemaps.com](https://www.xml-sitemaps.com/) 页面，输入博客地址，点击 start。

![](https://evanli.github.io/img/20181025/xml-sitemaps-com.jpg)

*   等待搜索完成，点击 VIEW SITEMAP DETAILS。

![](https://evanli.github.io/img/20181025/sitemap-completed.jpg)

*   下载 SITEMAP 文件 sitemap.xml 并将其上传到网站的根目录。

![](https://evanli.github.io/img/20181025/download-sitemap.jpg)

*   在 Google Search console 中添加你的 sitemap URL。

还是刚刚的 [Google Search Console](https://www.google.com/webmasters/tools/home?hl=zh-CN) 网站，点击刚刚验证成功的你的网站进入控制台，在左边侧边栏 “抓取” 下找到“站点地图”：

![](https://evanli.github.io/img/20181025/google-search-console-sitemap.jpg)

点击 “添加 / 测试站点地图”，将 https://xxxx.github.io/sitemap.xml 提交并刷新，就可以看到博客的网站结构了。

![](https://evanli.github.io/img/20181025/google-search-console-add-sitemap.jpg)

如果没有什么问题的话，到这里就结束了，但是现在用 Google 还不能立即查到博客的内容，要等到搜索引擎下一次更新检索时才会有显示。

5.手动提交 Google 抓取（可选）

---------------------

等待 Google 抓取所需时间比较长，可以利用 Google 抓取工具手动提交网址。（不是必须，等待 Gooogle 自行抓取也是可以的）

还是刚刚的 Google Webmaster，在左侧的 “抓取” 栏下可以找到“Google 抓取工具”，输入你想要被抓取的网址链接，点击“抓取”，然后在下面选择“请求编入索引”，然后提交即可。

![](https://evanli.github.io/img/20181025/googlebot.jpg)

![](https://evanli.github.io/img/20181025/googlebot-index.jpg)

此时再在 Google 的搜索栏中搜索：

> site:https://xxxx.github.io

应该就会有你刚刚提交上去的链接的结果了！也就大功告成了！

* * *
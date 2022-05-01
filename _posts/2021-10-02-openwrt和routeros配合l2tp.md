心血来潮，研究了下routeros和openwrt进行配对代理的问题，归结如下，主要涉及openwrt设置：

1、openwrt设置静态地址：

![](https://raw.githubusercontent.com/mypppv/images/master/2021-10-02/1.PNG)

2、l2tp如下：

![](https://raw.githubusercontent.com/mypppv/images/master/2021-10-02/2.PNG)

![](https://raw.githubusercontent.com/mypppv/images/master/2021-10-02/3.PNG)

3、l2tp拨号成功后，就可以上网了

4、为本地开启socks代理服务

![](https://raw.githubusercontent.com/mypppv/images/master/2021-10-02/4.PNG)

![](https://raw.githubusercontent.com/mypppv/images/master/2021-10-02/5.PNG)

5、为本地开启加速

![](https://raw.githubusercontent.com/mypppv/images/master/2021-10-02/6.png)

6、手机端代理上网即可
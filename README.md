# calibre的亚马逊中国元数据插件

**2017.12.15重大更新**

很久不关注amazon了，取了最新的一期(2017.12.15发布)calibre 3.14.0中的源文件重新更新了此插件，又可以抓取价格了，tag读不出。源文件写的是适用最低版本2.82 各位看着办吧。

注意！[日本亚马逊](https://www.amazon.co.jp/)最近作妖了，居然限制【每天每IP】读取网站书籍数据的次数，超过次数不给你数据！错误如下：

> CaptchaError: Amazon returned a CAPTCHA page. Recently Amazon has begun using statistical profiling to block access to its website. As such this metadata plugin is unlikely to ever work reliably. 

所以此插件和calibre自带的元数据插件都多了一个选项：数据来源。不过我试过以后发现除了amazon之外的几个数据源（好像都是网页缓存）并不好用.所以,悠着点用吧，别把人家网站服务器累死了:)

![](/img/v2-c85f229b95d9fc2dc8ccecf3bf88bf9c_hd.jpg)

**2016.12.09更新**   
Calibre已经发布最新的2.74版,已内置对[amazon.cn](https://amazon.cn)的支持!!!本插件正式退休,想抓价格的可以继续使用,仅仅想抓取中国亚马逊商店信息的可以直接使用官方版本。

以下是原文:  
---------------------------------------------------------------------------------------------  
我作了一个可以抓取亚马逊书籍**价格**的插件,可以从包括亚马逊中国在内的几个主要市场抓取书籍元数据.  
我作了一个日本亚马逊在售轻小说简介的网站 **acgnd.com**,可以参考利用这个插件抓取亚马逊图书信息的最终效果: [萌新小说-最新日本轻小说--日本亚马逊Kindle商店样书试读](http://www.acgnd.com/) 目前已经抓取了超过2万本书的信息了~

因为主程序__init__.py是直接拷贝了最新的calibre(2.74.0)源代码中的 calibre calibre-master\src\calibre\ebooks\metadata\sources\amazon.py 又加了几个函数而成,所以它原来有什么功能现在照样还有什么功能,原来不能下载亚马逊中国的元数据现在可以了。

1. 为什么要作这么一个插件?  
因为我想用calibre管理我的电子书,抓取亚马逊中国的元数据,同时**抓取价格**.而一本书一般有两种以上的价格, 便宜的那个当然是kindle电子书价格,贵点的是平装书价格,可能还有精装书价格等.

![](/img/b525183b2689572c42c5e89e401d8257_hd.jpg)

对于日本亚马逊卖的书,往往除了电子书价格,文库本价格外,还有新书,中古书(也就是二手书)的价格,相当多的书可是1 日元哦~

![](/img/14273f1d9dfa2cbda337364aed2f1189_hd.jpg)

2. 如何作这么一个插件?  
完全不懂python啊！！！拼了！从github上下载calibre的源代码,最新的是calibre(2.64.0),拷贝源代码中的 calibre calibre-master\src\calibre\ebooks\metadata\sources\amazon.py 重命名为__init__.py 抓取下列xpath:
```python
root.xpath('//div[@id="priceBlock"]/table/tbody/tr//b[@class="priceLarge"]')  
root.xpath('//span[@class="a-color-secondary"]/span')

root.xpath('//tbody[@id="paperback_meta_binding_winner"]/tr//td[@class=" price "]')  
root.xpath('//span[@class="a-color-base"]/span[@class="a-color-price"]') 
```
居然成功了!!!!  
问题又来了,calibre自带的栏目中并没有price,我不知道如何把抓取的信息存在用户自定义的栏目里,于是曲线救国,统一存到到了书号(identifiers)里  
于是又加上一个空的txt文件,命名为plugin-import-name-AMAZON_PRICE.txt 和上述的  
__init__.py一起打包成为一个zip文件

3. 如何安装?

下载地址 [度盘](https://pan.baidu.com/s/11-BuuaNAAxp9vrgbEOVFUw)

打开calibre,点击 首选项->插件->从文件安装插件,选择刚才那个zip文件,点两次确定.

![](/img/83f25febe5092ecc591eb261cce9bfa5_hd.jpg)

![](/img/d7e4b4d168deebca7695b089763b88d5_hd.jpg)

![](/img/9e3492ebae9f4cae754d606af95cd60d_hd.jpg)

![](/img/869d429e25820ab9fe04742b1bf19f74_hd.jpg)

![](/img/b43fca0a66794b823238e76de3dd6322_hd.jpg)

安装好了就这样, 继续点击"自定义插件"

![自定义插件](/img/54d2845f3b265c2d8365dfffafbf8a9c_hd.jpg)

选择要下载的元数据字段,选择要使用的Amazon网站为"china",确定.

我个人建议尽量**不要下载评分和出版日期**,因为评分要么没有,要么总是5星,而中国区和日本区的出版日期抓取出来总是比正确的日期晚一天.

![](/img/432070c4c82afdbecdaa63081dddc82f_hd.jpg)

当然也可以从 首选项->元数据下载 进入同样的配置界面

![](/img/7561a84cca869fa0e0dc5e4037e0fe36_hd.jpg)

![](/img/a5a982e520c2f95e2a1d146580a3da7a_hd.jpg)

4. 工作

安装好了就开始下载了!

在calibre选择几本书,点 编辑元数据->下载元数据和封面, 或者直接用快捷键ctrl+D

![](/img/f7249e82758cc6b7acd1ff76378a08eb_hd.jpg)

![](/img/e91f4cdcbba4be38fbfaf2fd255b26cd_hd.jpg)

过一会儿软件又下角会浮出一个对话框,可以选择"是"或者"检查刚下载的元数据"

![下载元数据](/img/5abcccc783ac6679cf68976cd4ab3aec_hd.jpg)

看看,价格,作者,标签,等等都有啦~

![](/img/4d8c4e6515eb4438524e36d25a9ac758_hd.jpg)

添加两个自定义的栏目: 首选项->添加栏目->添加自定义栏目,栏目模版是{identifiers:select(price)} 类型是文本.当然你愿意使用浮点数也可以的

![](/img/6b99ec373d723a2f3b23f790b36a3504_hd.jpg)

![](/img/0f86dc82237dc139a295c94ad34e6b6c_hd.jpg)

![](/img/104b83c058d151d1530c2018f70d3d86_hd.jpg)

好了,大功告成!最后就是这个样子:

![成功](/img/d0a5d63e964426b737648e1188515f54_hd.jpg)

另外这个插件还可以下载丛书(series)和序号(series_index),因为这两项信息只有日本亚马逊的书才有,所以不多说了.

还有源代码中抓取评分(rating)的代码是错误的,我尝试修改了一下,抓取能抓出来,保存的时候又错了,解决不能,放弃了

知乎原文 [www.zhihu.com/question/22378030](https://www.zhihu.com/question/22378030)

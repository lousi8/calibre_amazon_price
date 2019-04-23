This is a calibre metadata download plugin, it can download all the available metadata plus price information from amazon.cn and amazon.co.jp and saved it into identifiers.price and identifiers.price2

Please visit these to find how to use it:
http://www.zhihu.com/question/22378030
http://kindleren.com/thread-188573-1-1.html 
price means ebook price and price2 means paper book price, usually price2 is higher than price. As you know paper book is always expensive than ebook:)
I didn't have so many books to test all the other amazon market such as amazon.com and amazon.de but I guess it also works fine since the xpath of price  
in amazon worldwide webpage is almost the same.

I don't know how to save information to user columns, so saved it into system built-in column identifiers.price and identifiers.price2

It also can download series and series index from amazon.co.jp. For all the other amazon market, no series information displayed.

Any questions please contact me at lulusoft@yeah.net. Very Thanks for Niu Kai who told me it is possible to create a plugin to download information from  
amazon's website and give me an example for amazon.cn

If you know Japanese or Chinese, please visit http://www.acgnd.com to check all my test cases:) There are more than 1600 downloaded kindle example  
ebooks form www.amazon.co.jp and managed by calibre very well.

This zip file include such files:
__init__.py
plugin-import-name-AMAZON_PRICE.txt

__init__.py is copied from the latest(2.30.0) source code of calibre calibre-master\src\calibre\ebooks\metadata\sources\amazon.py and modified by me.

2015.06.11


非常感谢知乎@亚里士缺德的帮助,我作了一个可以抓取亚马逊书籍价格的插件,可以从包括亚马逊中国在内的几个主要市场抓取书籍元数据.
下载地址 https://pan.baidu.com/s/1i5cc9UH
因为主程序__init__.py是直接拷贝了最新的calibre(2.30.0)源代码中的 calibre calibre-master\src\calibre\ebooks\metadata\sources\amazon.py 又加了几个函数而成,所以它原来有什么功能现在照样还有什么功能,原来不能下载亚马逊中国的元数据现在可以了~~就这样.

1>为什么要作这么一个插件?
因为我想用calibre管理我的电子书,抓取亚马逊中国的元数据,同时抓取价格.而一本书一般有两种以上的价格, 便宜的那个当然是kindle电子书价格,贵点的是平装书价格,可能还有精装书价格等.
对于日本亚马逊卖的书,往往除了电子书价格,文库本价格外,还有新书,中古书(也就是二手书)的价格,相当多的书可是1 日元哦~

2>如何作这么一个插件?
完全不懂python啊！！！xpath又是什么鬼?拼了！从github上下载calibre的源代码,最新的是calibre(2.30.0),拷贝源代码中的 calibre calibre-master\src\calibre\ebooks\metadata\sources\amazon.py 重命名为__init__.py 抓取下列xpath:

root.xpath('//div[@id="priceBlock"]/table/tbody/tr//b[@class="priceLarge"]')
root.xpath('//span[@class="a-color-secondary"]/span')

root.xpath('//tbody[@id="paperback_meta_binding_winner"]/tr//td[@class=" price "]')
root.xpath('//span[@class="a-color-base"]/span[@class="a-color-price"]')
居然成功了!!!!
问题又来了,calibre自带的栏目中并没有price,我不知道如何把抓取的信息存在用户自定义的栏目里,于是曲线救国,统一存到到了书号(identifiers)里
于是又加上一个空的txt文件,命名为plugin-import-name-AMAZON_PRICE.txt 和上述的
__init__.py一起打包成为一个zip文件

3>如何安装?
打开calibre,点击 首选项->插件->从文件安装插件,选择刚才那个zip文件,点两次确定.
安装好了就这样, 继续点击"自定义插件"
选择要下载的元数据字段,选择要使用的Amazon网站为"china",确定.
我个人建议尽量不要下载评分和出版日期,因为评分要么没有,要么总是5星,而中国区和日本区的出版日期抓取出来总是比正确的日期晚一天~~

当然也可以从 首选项->元数据下载 进入同样的配置界面
4>工作
安装好了就开始下载了!
在calibre选择几本书,点 编辑元数据->下载元数据和封面, 或者直接用快捷键ctrl+D

过一会儿软件又下角会浮出一个对话框,可以选择"是"或者"检查刚下载的元数据"
看看,价格,作者,标签,等等都有啦~

添加两个自定义的栏目: 首选项->添加栏目->添加自定义栏目,栏目模版是{identifiers:select(price)} 类型是文本.当然你愿意使用浮点数也可以的
好了,大功告成!最后就是这个样子:

另外这个插件还可以下载丛书(series)和序号(series_index),因为这两项信息只有日本亚马逊的书才有,所以不多说了.

还有源代码中抓取评分(rating)的代码是错误的,我尝试修改了一下,抓取能抓出来,保存的时候又错了,解决不能,放弃了~~

请访问我的日本轻小说试读网站www.acgnd.com查看效果~

2015.07.05 更新1.0.1
日本亚马逊网站改版, series和series_index从网站上消失,导致我的这个插件抓取出的series毫无意义.修改了另外一个算法,仅对小部分书籍有效.
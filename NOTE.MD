# 随笔



  ## 2022



### 10.15

最近在研究netflav（一个我觉得挺好的av网站）的爬虫，装了React的调试插件可以看到它是用react写的，所有直接逆向不是很方便

![image-20221019105027613](https://imgbed-1254007525.cos.ap-nanjing.myqcloud.com//img/image-20221019105027613.png)

每个视频会提供一个或多个播放器（是嵌在视频页面里面的另一个页面），有的视频会提供bt链接

看看网络请求

![image-20221019110311516](https://imgbed-1254007525.cos.ap-nanjing.myqcloud.com//img/image-20221019110311516.png)

可以直接找到视频链接

但是咱们不知道请求的链接中的字符串是怎么生成的

![image-20221019110400363](https://imgbed-1254007525.cos.ap-nanjing.myqcloud.com//img/image-20221019110400363.png)



js代码也经过了混淆

所以只能想其他的方法

我暂时想到的方法是puppeteer，可以模拟浏览器运行，然后在监听请求即可，这样可以拿到视频的m3u8地址





## 10.19

今天早上放假回来

再研究了下

发现每个页面json  字符串 保存了当前页面的相关信息

![image-20221019123830955](https://imgbed-1254007525.cos.ap-nanjing.myqcloud.com//img/image-20221019123830955.png)

感觉很奇怪

还可以看到Next字样

之前没有接触过服务端渲染

也许就是这么玩的



再看了下每个视频页面的播放器

![image-20221019124044927](https://imgbed-1254007525.cos.ap-nanjing.myqcloud.com//img/image-20221019124044927.png)

去Google搜了下

他们都是提供视频存储服务的平台

在视频里插入广告，视频的上传者可以根据播放量拿到钱，收益好像还不少

![image-20221019124912939](https://imgbed-1254007525.cos.ap-nanjing.myqcloud.com//img/image-20221019124912939.png)

收益根据用户地区（指视频观看者）决定

发达国家的收益要比一般国家的收益高得多，最高1w次观看可以拿到30刀



大多数视频都有**DO**这个播放器

![image-20221019125310542](https://imgbed-1254007525.cos.ap-nanjing.myqcloud.com//img/image-20221019125310542.png)

视频链接通过这样一个地址获取

再看看调用堆栈

![image-20221019125352586](https://imgbed-1254007525.cos.ap-nanjing.myqcloud.com//img/image-20221019125352586.png)

可以看到最底层是html

说明链接就直接写在html里

再搜索一下这个链接

![image-20221019125518369](https://imgbed-1254007525.cos.ap-nanjing.myqcloud.com//img/image-20221019125518369.png)

![image-20221019125535499](https://imgbed-1254007525.cos.ap-nanjing.myqcloud.com//img/image-20221019125535499.png)

果然



这样，只要发送两次请求，就可以拿到mp4格式的视频，然后丢到cloudreve上面，自动下载到OneDrive
---
layout:     post
title:      "想办法躺着看片"
subtitle:   " \"打造我的Netflix\""
date:       2022-02-08 13:32:00
author:     "Bing"
catalog:    true
tags:
    - 生活
    - 看片
    - 娱乐
---

最近看片追剧有点麻烦。想要看的片在国内要么有删减，要么就干脆没有。只能自己去找资源下载到本地了。然而，在电脑上看没办法躺着，传到设备上又嫌麻烦。**那么能不能像在Bilibili看片一样，在手机上直接观看个人电脑中存储的影片资源呢？**

经过Google以及在Github上的翻找，我发现了 [**Streama**](https://github.com/streamaserver/streama) 这个有趣的项目。简单来说，它能让你打造一个类似 *Netflix* 的个人线上影院。

Streama是运行在Java环境下的，我们得先安装[JRE 8](https://www.oracle.com/java/technologies/downloads/)。

然后去[Streama Release](https://github.com/streamaserver/streama/releases)下载Streama的jar包。

执行jar包，我们的Streama Server就运行起来了。Server默认服务在http://localhost:8080上。
```
java -jar streama-1.10.4.jar
```

访问并登录。
![](/img/post/streama-logging-page.PNG)

接下来设置**Base Url**，修改成终端可访问的Url地址。
![](/img/post/streama-base-url.PNG)

然后设置**Local Video Files**目录，即本地储存影片资源的目录。
![](/img/post/streama-local-video-files.PNG)

接下来可以开始创建我们剧集了。

然后创建单集视频。

配置本地片源。

手机上看看试试效果。

***大功告成，可以躺着看剧了！***
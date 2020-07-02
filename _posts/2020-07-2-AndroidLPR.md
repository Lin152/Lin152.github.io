---
title: AndroidLPR
tags: Lin
---

先配置NDK，NDK版本为14
下载NDK-14，再把解压的文件夹里的所有文件替换掉之前NDK文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154005216.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwNDkyNzcx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154012126.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwNDkyNzcx,size_16,color_FFFFFF,t_70)
下载链接
https://developer.android.google.cn/ndk/downloads/older_releases.html
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154020503.png)
导入opencv342（一定要342，其他可能会出错）
Opencv342下载地址
https://github.com/opencv/opencv/releases/tag/3.4.2
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154032829.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwNDkyNzcx,size_16,color_FFFFFF,t_70)
Android程序点File，然后New，再Import module from source
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154039287.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwNDkyNzcx,size_16,color_FFFFFF,t_70)
再选择opencv342的路径
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154043591.png)
因为我已经导入了opencv，所有会报错
最后在Project Structure 添加opencv依赖
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154049393.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwNDkyNzcx,size_16,color_FFFFFF,t_70)
App的gradle和opencv的gradle版本要统一
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154053252.png)

然后在模板文件中复制一些你Android程序中没有的文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154056255.png)
在AndroidManif.xml文件中开启权限
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154101295.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwNDkyNzcx,size_16,color_FFFFFF,t_70)
配置build.gradle，把模板里有的都复制过来
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154109811.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwNDkyNzcx,size_16,color_FFFFFF,t_70)
修改.cpp文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154115394.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154121649.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154124263.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154137465.png)与
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154144681.png)的路径
要一样
.so文件如果没有要加
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200605154213409.png)

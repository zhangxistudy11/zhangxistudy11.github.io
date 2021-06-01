# sourcetree



一、--no-ff 使用和不使用的区别

1、能够fast-foward情况下，即切出分支后，主分支没有任何改动:

使用 --no-ff ，会多出一根线，显示切出分支的改动；不使用的话，直接合并过来，看不出切出分支的改动；

这个时候 --no-ff 使用会有效果

使用：

![截屏2021-01-31 20.28.20.png](https://upload-images.jianshu.io/upload_images/1076103-4681f11a7d90e9c3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

不使用：
![截屏2021-01-31 20.28.30.png](https://upload-images.jianshu.io/upload_images/1076103-ae1356633fdf3416.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


2、不能fast-foward情况下，即切出分支后，主分支也有改动：

使用不适用--no-ff ，效果都是一样的，都展示如图

![截屏2021-01-31 20.28.39.png](https://upload-images.jianshu.io/upload_images/1076103-ca03dee31c1d0556.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

二、切出使用了reabse后，合并的时候，都是可以fast-forward的，这个时候，最好是配合--no-ff使用

展示如图：

![截屏2021-01-31 20.28.54.png](https://upload-images.jianshu.io/upload_images/1076103-f9e082562e274b11.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


三、[参考链接](https://backlog.com/git-tutorial/cn/stepup/stepup1_4.html)

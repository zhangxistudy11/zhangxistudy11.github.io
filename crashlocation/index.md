# iOS如何将闪退日志符号化


![Minion](https://app.yinxiang.com/files/common-services/binary-datas/c2VydmljZVR5cGU9MiZzZXJ2aWNlRGF0YT17Im5vdGVHdWlkIjoiZjg5ZWU2Y2MtMzhmMy00OTJkLTk0MmQtYTdmNzRkOWZjZDU2IiwicmVzb3VyY0d1aWQiOiI3MmUyMDhhNC0yZjJjLTQ2YWQtYWUwNS03MTI1YTMzZTI1NmEifQ==)

这篇文章会介绍定位闪退的几种方法，由易到难进行介绍。当你手里关于闪退的信息越多，解决就越简单，反之，就会更难。

首先解释下符号化的概念：符号化就是解决把栈回溯地址转化为为源码方法名或函数名的过程。符号化完成后，崩溃日志中所有的十六进制地址都转化为了方法名函数名，方便开发人员定位bug.



### 1、在第三方平台或者自研apm平台获取符号化后的日志

>前提：
>
>1. 项目集成的三方收集日志的平台，或者有自研的apm平台；
>
>2. 打包同学在该平台上传了dysm文件。

这种方法是最简单的，也不用过多介绍。很多项目都集成了bugly、友盟等等，大公司都会有自己的一套APM平台。

### 2、利用Xcode查看崩溃信息

>前提：
>
>1. 开发者手里有发生崩溃的手机；
>
>2. 手机上的应用是这台电脑安装打包。

选择window－> devices －> 选择自己的手机 -> view device logs 就可以查看手机上所有的崩溃信息了。如果是使用其他电脑进行的打包，可以在这里面将Crash文件导出，自己通过命令行的方式进行解析（见方法3）。

![WeChat7b227a7badf8de1ee1f36dd0fd1f9040.png](https://app.yinxiang.com/files/common-services/binary-datas/c2VydmljZVR5cGU9MiZzZXJ2aWNlRGF0YT17Im5vdGVHdWlkIjoiNmEwOWE1ZGQtYTQ3ZS00ZjE3LTg2MzQtYzA4NTg1ZDI1ZGI0IiwicmVzb3VyY0d1aWQiOiI0NDgxYzVmNS1kMWZlLTQ3NDAtYTQ3NC03ZGZkZGVhN2RmYjIifQ==)

### 3、Mac自带的命令行工具symbolicatecrash


>前提：
>
>1. symbolicatecrash工具;
>
>2. .ips文件;
>
>3. dSYM文件;

##### 1、如何获取symbolicatecrash工具？
右键Xcode,显示包内容，通过以下路径找到：/Xcode.app/Contents/SharedFrameworks/DVTFoundation.framework/Versions/A/Resources/symbolicatecrash.

##### 2、如何获取.ips文件
1. 可以通过真机连Xcode 导出：Xcode>Window>Devices and Simulators>选择已连接的真机>View Device Logs>xxxApp>右键导出.crash文件；


2. 手机->设置->隐私->分析与改进->分析数据，找到对应时间点的日志；

##### 3、如何获取dysm文件?

1. 找到打包的那台机器，打开Xcode.Window -> Organizer -> Archives -> 选中需要导出dSYM的Archive右击 -> Show in Finder -> 右键.xcarchive文件显示包内容 -> dSYMs文件夹

2. 大公司的打包平台下载app的地方，就有对应的dysm文件。

拿到以上，三个文件后，放到一个统一文件夹里。命令行cd 到该文件下，执行以下命令：

>./symbolicatecrash xxxxx.ips xxxxx.app.dSYM > crash.log

此时该目录下，就会多出一个crash.log的文件，里面放的就是符号化后的解析日志。

如果报错 Error: "DEVELOPER_DIR" is not defined at ./symbolicatecrash line 69. 需要 执行命令
>export DEVELOPER_DIR="/Applications/XCode.app/Contents/Developer"
然后重新 输入命令
>./symbolicatecrash xxxxx.ips xxxxx.app.dSYM > crash.log

### 4、通过atos逐行解析堆栈

![aa.png](https://app.yinxiang.com/files/common-services/binary-datas/c2VydmljZVR5cGU9MiZzZXJ2aWNlRGF0YT17Im5vdGVHdWlkIjoiNmEwOWE1ZGQtYTQ3ZS00ZjE3LTg2MzQtYzA4NTg1ZDI1ZGI0IiwicmVzb3VyY0d1aWQiOiJjMzVkODlmYS05MWU1LTQyODgtODc3Ny1iZTRlNTI4ODVjNzgifQ==)
##### 根据对应的Binary Images 是项目自己的二进制还是系统动态库来区分

###### 1、是项目里的二进制

直接执行命令：

>atos -arch arm64 -o 二进制名（图中的2） -l 首地址(后面对应的短的那个)  偏移地址(后面对应长的那个)

###### 2、是系统的动态库

这个时候要根据日志中的iOS版本信息(图中的1) 去[符号表目录](https://github.com/Zuikyo/iOS-System-Symbols/blob/master/collected-symbol-files.md)下载对应版本的符号信息。

下载好对应版本的符号信息，把日志里对应的动态库(图片中的3)拷到一个单独文件内，命令行cd到对应文件夹，执行命令：

>atos -arch arm64 Foundation.framework/Foundation -l 0x1830bc000 0x0000000183109f94





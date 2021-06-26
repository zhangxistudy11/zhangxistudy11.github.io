# 使用SourceTree回滚






  >代码回滚，适用于的场景：
   >#### 1.提交错代码，想放弃刚刚提交的部分；
   >#### 2.代码发生冲突，处理比较麻烦，为了代码安全，直接回滚到之前干净的代码。
  
  ### 我个人理解，可以分为本地回滚和远程回滚：
  ### 一.本地回滚，回滚自己已经提交的代码，但还未推送到远程仓库。
  ![WeChat7b227a7badf8de1ee1f36dd0fd1f9040.png](https://app.yinxiang.com/files/common-services/binary-datas/c2VydmljZVR5cGU9MiZzZXJ2aWNlRGF0YT17Im5vdGVHdWlkIjoiZDQzZGU0MTctYzE4ZC00ZGVmLTk0YmMtNTE5OTdiNDA5YjUxIiwicmVzb3VyY0d1aWQiOiJlMDU1MWI3Mi1hMjhlLTRlMjAtOTlmNi05MjVjMTQwZGNkNGQifQ==)

   目前我在本地提交了两次，但第二次有大量错误代码，我选择放弃，想直接回到第一次提交的位置，采取以下步骤：
   选中你想回滚到的提交记录，右击->将（所在分支）重置到这次提交->强行合并->确定
   
   
   ![屏幕快照 2019-03-02 下午6.59.15.png](https://app.yinxiang.com/files/common-services/binary-datas/c2VydmljZVR5cGU9MiZzZXJ2aWNlRGF0YT17Im5vdGVHdWlkIjoiZDQzZGU0MTctYzE4ZC00ZGVmLTk0YmMtNTE5OTdiNDA5YjUxIiwicmVzb3VyY0d1aWQiOiI1MmFhODM2Ny1mM2FlLTRjOGYtYThiNC1iNjhhYmYwYjhiOTEifQ==)
![屏幕快照 2019-03-02 下午6.59.29.png](https://app.yinxiang.com/files/common-services/binary-datas/c2VydmljZVR5cGU9MiZzZXJ2aWNlRGF0YT17Im5vdGVHdWlkIjoiZDQzZGU0MTctYzE4ZC00ZGVmLTk0YmMtNTE5OTdiNDA5YjUxIiwicmVzb3VyY0d1aWQiOiJmNjA3YzY5NC1jMGRjLTQ2NGItODc3Ni00MWM3ZGFmNjZhOGQifQ==)




### 二.远程回滚，即回滚远程代码仓库的代码。
SourceTree默认是不提供这种操作的，因为存在风险。所以，回滚远程代码，一定要注意：
>1.想要放弃的代码，是所有开发成员都一致同意的；
>
>2.想要放弃的代码只是自己的，中间没有别人的提交记录，这可以直接回滚。
>
>3.这个操作过程中，提醒其他成员不要推送代码。
>
  操作步骤如下：
  1.SourceTree开启允许强制推送权限
  ![WeChat49ce02c556383746dfcc3eab7c6e4b47.png](https://app.yinxiang.com/files/common-services/binary-datas/c2VydmljZVR5cGU9MiZzZXJ2aWNlRGF0YT17Im5vdGVHdWlkIjoiZDQzZGU0MTctYzE4ZC00ZGVmLTk0YmMtNTE5OTdiNDA5YjUxIiwicmVzb3VyY0d1aWQiOiI5MThkN2ZiMy02Njc0LTQwYzMtYmZlMy1lOGM2MTkzNWRlMmQifQ==)
  2.和本地回滚一样，先回滚到想要的位置
![屏幕快照 2019-03-02 下午6.59.15.png](https://app.yinxiang.com/files/common-services/binary-datas/c2VydmljZVR5cGU9MiZzZXJ2aWNlRGF0YT17Im5vdGVHdWlkIjoiZDQzZGU0MTctYzE4ZC00ZGVmLTk0YmMtNTE5OTdiNDA5YjUxIiwicmVzb3VyY0d1aWQiOiI1MmFhODM2Ny1mM2FlLTRjOGYtYThiNC1iNjhhYmYwYjhiOTEifQ==)

3.强制推送代码，切记这个时候不要拉取代码
![屏幕快照 2019-03-02 下午7.51.34.png](https://app.yinxiang.com/files/common-services/binary-datas/c2VydmljZVR5cGU9MiZzZXJ2aWNlRGF0YT17Im5vdGVHdWlkIjoiZDQzZGU0MTctYzE4ZC00ZGVmLTk0YmMtNTE5OTdiNDA5YjUxIiwicmVzb3VyY0d1aWQiOiI4NmVhYzZkNS03Y2U0LTQ4YmMtYmQ0Mi1mYzA2MWZlNjc0NjgifQ==)
5.完成操作，本地和远程的代码都是你想要回滚的地方。




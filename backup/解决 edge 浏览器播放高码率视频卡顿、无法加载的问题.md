
笔者在使用 edge 播放高码率视频的过程中遇到了播放卡死等问题

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1735759894354-122e256d-aa68-4fab-9b40-e3c37ef8a3a8.png)

于是找来朋友测试，确认视频是没问题的

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1735759868557-6729ff4d-ca6b-450b-ae1c-3f2b25ed2f9f.png)



在确认网络没问题的前提下，将 edge 的设置都翻了一遍，可这并没有解决

于是尝试换了 edge 的 dev 版本，还是寄

当关闭硬件加速时可以正常播放，但是这样独显就成了摆设，对这个结果我肯定时不满意的

于是咱尝试更新了 N 卡驱动，还是不行

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1735759749861-9b308828-ec52-4e83-9c96-9eab93c61da7.png)



然后...我注意到了一个分页文件报错的信息

嗯...然后我找上了 swap![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1735759972141-577abb42-adaa-4b9e-9a5b-f278d48c663d.png)![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1735759977177-14a12e85-e327-4cc3-a0d9-206a43500385.png)



尝试关掉它后，重启

视频能正常播放了



![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1735760104679-bbf157d7-f30c-430c-ae22-744923146c91.png)

引发故障的原因似乎是系统无法正常分配虚拟内存，因为笔者 D 盘也装了系统，笔者将虚拟内存丢到 D 盘去了

浏览器大概是硬件加速的时候调用了 swap 然后寄了...挺奇妙的，不知道为什么这种时候不直接写进内存

因为笔者内存足够所以直接关了，读者可以自行选择，反正不报错就大概能用，大概吧

笔者在这里有一点要说，生产机器还是不建议关虚拟内存的，毕竟开了有虚拟内存兜底，程序不会直接爆了（笑


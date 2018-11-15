---
title: ffmpeg转封装【ffmpeg 从入门到精通】
date: 2018-10-07 17:36:10
tags: ffmpeg
categories: ffmpeg
---
音视频文件转mp4格式

ffmpeg 对媒体格式进行转封装；
媒体格式转封装是什么？？？


1）mp4 格式
2）格式解析方式、 
3）如何获取mp4格式文件解析时需要的数据
4）mp4的可视化分析工具，
5）使用ffmpeg封装mp4文件

<h3> 一、了解mp4的视频优势 </h3> 
	跨平台好， 可以使用flash、ios、android 的H5播放。
<h3> 二、MP4基本格式 </h3>
MP4标准： ISO-14496 part 12 ， ISO-14496 part 14
这个链接如何进行查看？？？？ 【这个可以直接搜索，然后看维基百科的内容】
https://en.wikipedia.org/wiki/MPEG-4

<h4>1、几个概念：</h4>
	（1）MP4 = (n)Box + (n)fullBox【 MP4是由许多个Box 与fullBox组成】
	（2）Box = Header + Data 
	（3）FullBox 是Box的扩展，基于Box结构， 在Header中增加了8位version标志 和24位flag标志。
	（4）Header 包含了整个Box的长度大小(size)和类型(type)
		当size等于0时，代表这个Box是文件的最后一个Box；
		当size等于1时，代表Box长度需啊哟更多的位来描述, 在后面定义一个64位的largesize来描述Box长度。
		当Type为uuid时，说明这个Box中的数据是用户自定义扩展类型。
	(5)Data 是Box的实际数据，可以是纯数据，也可以是更多的子Box。
	(6)当一个Box中Data是一系列的子Box时，这个Box又可以成为Container（容器）Box。

<h4>2、Mp4 常用参考标准排列方式</h4>
<h5>1）看书p61<h5>
note：
MP4标准中描述的moov与mdat 的存放位置前后并没有进行强制要求，所以这些时候moov这个Box在mdat的后面和前面都有可能；
在互联网视频点播中，如果希望MP4文件被迅速打开，则需要将moov存放在mdat的前面；
如果放在后面，则需要将mp4文件下载完成了之后才可以进行播放。

下面是表的主要信息：
<h6> <1>moov容器 </h6>
moov定了一个mp4文件中的数据信息【meta信息】，类型是moov， 是一个容器atom，其至少必须包含以下三种atom中的一种：
【atom是啥？ 隐式是存放音视频数据信息的一种数据结构】
	1）mvhd(movie header atom) 存放未压缩过的影片信息的头容器
	2）cmov（compressed movied atom）压缩过的电影信息容器，不常用
	3）rmra（reference movie atom） 参考电影信息容器，不常用
	4）包含其他容器信息，eg：影片剪辑信息(clipping atom(clip))、一个或几个trakAtom(trak)、一个Color table atom(atab) 和一个user data atom(udta)

详解：
	1）mvhd 定义多媒体的time scale ，duration以及display characteristic；
		track中定义了多媒体文件中的一个track信息，track是多媒体文件中可以独立操作的媒体单位，例如： 一个音频流就是一个track，一个视频流就是一个track。
	使用二进制查看工具打开吗，哎一个mp4 文件。？？？ 使用什么工具？Hex fiend 、atom inspector工具打开
	![使用二进制查看工具打开mp4文件(Hex fiend )](../../../../asset/Snip20181007_2.png)
	![使用二进制查看工具打开mp4文件(Hex fiend )](../../../../asset/Snip20181009_29.png)
	上面两张图中，上一张是视频被截断的，下一张是完整的视频， 我们开始应该尽可能的使用完整的视频
	![atom inspector](../../../../asset/Snip20181007_4.png)

下面是moov参数：
![moov 参数](../../../../asset/Snip20181008_23.png)


<h3>三、mp4 分析工具</h3>
mp4封装格式的分析工具：
ffmpeg、elecard streamEye/ mp4box, mp4info

<h5>1)Elecard StreamEye </h5>
	<1>可以查看帧的排列信息，将I帧，p帧、B帧显示不同颜色；而且柱的长短根据帧的大小展示；
	<2>mp4内容信息，包括流的信息、宏块的信息、文件头的信息、图像的信息以及文件的信息等。
set volume bootability and startup disk options,
设置启动能力和启动磁盘选项
https://www.elecard.com/videos
注册了一个，说5S发邮件给我，但是没有收到，下次使用google的邮箱看看

<h5>2) 查看一个媒体文件，使用vi来也是可以看到基本的内容的</h5>
![moov 参数](../../../../asset/Snip20181008_24.png)

<h5>3) mp4box</h5>
mp4box 是GPAC 项目中的一个组件， 可以通过mp4box针对媒体文件进行合成、拆解等操作。
![mp4box 里面的参数](../../../../asset/Snip20181008_27.png)

mp4box 有很多子帮助项， 
eg： DASH 切片、编码、metadata、BIFS流、ISMA、SWF相关帮助信息等。
分析mp4文件,命令如下:
> mp4box -info 1519916400.mp4
[输出信息](../../../../asset/mp4box.txt)
可以看到有timescale 、duration、framegremented等内容

<h5>4) mp4info </h5>
可以将mp4文件中的Box 解析出来，并将其中数据展现出来
官网链接： 
https://www.bento4.com/
https://www.bento4.com/documentation/mp4info/
在mac上只有命令行的，没有图形界面的内容，这个到时候在进行写个mac应用吧；

直接执行： mp4info output.mp4
输出结果如下：
[输出结果](../../../../asset/mp4info.txt)

<h3> 四、mp4在ffmpeg中的Demuxer</h3>
1) ffmpeg -h demuxer=mp4
结果如下图：
![ffmpeg 中的Demuxer](../../../../asset/Snip20181009_28.png)
上面的图可以看出，mp4的demuxer与mov、3pg、m4a、3g2、mj2的Demuxer相同；可以详细查看图中的选项；

2) 在解析MP4文件，通过ffmpeg解析时，可以通过参数ignore_editlist 忽略Editlist Atom 对MP4的解析；
不过通常使用默认操作就可以了；

<h3> 五、mp4在ffmpeg中的Muxer</h3>
mp4在封装相对于解封装的时候复杂点；上面的几种格式在封装和解封装上基本上没有太大差别；·
输入命令：ffmpeg -h muxer=mp4
结果如下：
![ffmpeg 中的muxer](../../../../asset/Snip20181010_9.png)
![ffmpeg 中的muxer](../../../../asset/Snip20181010_10.png)
mp4的muxer支持的参数比较复杂，例如：支持在视频关键帧处切片，只支持设置moov容器大小的最大值，支持设置encrypt加密等。

下面是对应参数了解：
	1）faststart 








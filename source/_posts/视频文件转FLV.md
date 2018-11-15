---
title: 视频文件转FLV
date: 2018-10-12 00:20:25
tags: ffmpeg
categories: ffmpeg
---

从文件标题可以看出，flv并不是视频文件？ 
视频文件： mp4 等
它也是一种视频文件格式； 

flv格式 编辑
FLV流媒体格式是sorenson公司开发的一种视频格式，全称为Flash Video。它的出现有效地解决了视频文件导入Flash后，使导出的SWF文件体积庞大，不能在网络上很好的使用等缺点。


flv在网络的直播与点播场景中【flv也是一种常见的格式】，flv是adobe不发的一种以作为直播也可以作为点播的封装格式。
格式组成（简单）： 均以FLVTAG的形式存在，并且每个TAG都是独立存在的。

<h2>一、flv 文件的标准格式 </h2>
<h3>1、文件格式</h3>
两部分： （1）flv文件头，（2）flv文件内容

flv文件信息如下：
![flv 文件信息](../../../../asset/Snip20181012_29.png)
得出： 
1）文件签名占用了 3个字节， 组成： flv 
2）文件版本， 常见为1
3）接下来文件前5位位0【保留】，接着音频展示设置为1，下一位为0【保留】，再下一位为视频展示，设置为1；
eg：如果是一个音视频都展示为flv文件，那么这个字节会设置为0x05（00000101）
4）4字节的数据，为flv文件头数据的偏移位置。
然后可以对flv二进制的文件进行解析，可以使用工具，hex fieid工具；

<h3>2、flv文件内容格式解析 </h3>
如下面的图：
![flv 文件信息](../../../../asset/Snip20181012_30.png)
计算每个TAG的大小， 为11（tag的header） + tag的body的大小；
flv文件内容的格式为FLVTAG，
FLVTAG分为两部分：
1）TAGHeader部分
2）TAGBody部分

<h3>3、FLVTAG格式解析</h3>
看下面的图：
![flv 文件内容1](../../../../asset/Snip20181012_31.png)
![flv 文件内容2](../../../../asset/Snip20181012_32.png)
1）保留为占2位， 最大为：11b
2)滤镜位占用1位，最大为1b
3）TAG类型占用5位，最大声为11111b常见为：0x08, 0x09, 0x12,处理，和保留、滤镜公用一个字节，一般处理将保留位于滤镜设置为0；
4）数据大小：24b（3bytes）
5）时间戳大小：24b（3bytes）；最大：0xffffff（16777215ms）转化为16777s， 279m，4.66h，所以，flv格式可以存储达到4.66小时；
6）扩展时间8b（1byte），最大为255，扩展时间戳使得flv原有的时间戳得到扩展，所以不仅仅是4.66H，可以到达49.7D；
7)流ID大小24b（3bytes），最大为0xFFFFFF，不过flv中一直将其存储为0
8）接下来就是header之后的数据，为TAG的data，大小为flag的Header中DataSize中存储的大小，存储的数据分为视频数据，音频数据，以及脚本数据。

<h3>4、video tag解析</h3>
如果header的flvType为0x09，则TAG为视频数据TAG，falv支持多种视频格式，说明：
![flv videotag 0](../../../../asset/Snip20181012_33.png)
![flv videotag 1](../../../../asset/Snip20181012_34.png)
DTS： 主要用于视频的解码,在解码阶段使用；Decode Time Stamp。DTS主要是标识读入内存中的ｂｉｔ流在什么时候开始送入解码器中进行解码。
PTS： 主要用于视频的同步和输出.在display的时候使用； Presentation Time Stamp。PTS主要用于度量解码后的视频帧什么时候被显示出来。

<h3>5、audio tag数据格式解析</h3>
tagtype = 0x08， 为音频，
音频可以封装的压缩音频编码可以有很多种；
![flv audio tag 1](../../../../asset/Snip20181012_35.png)
![flv audio tag 1](../../../../asset/Snip20181012_36.png)

<h3>6、scriptData 格式解析</h3>
tagtype = 0x12 ,这个数据为scriptData类型，scriptData常见的展示方式为flv的metadata，里面存储的数据格式一般为AMF数据；
![flv script data](../../../../asset/Snip20181012_37.png)
更多解析可以查看官方文档；

<h2>二、ffmpeg转flv参数 </h2>
执行命令：ffmpeg -i 1519916400.mp4 -c copy -f flv output.flv
![flv ffmpeg 转flv参数](../../../../asset/Snip20181012_37.png)





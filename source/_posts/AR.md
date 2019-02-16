---
title: AR
date: 2019-02-15 10:50:16
tags: AR
categories: AR
---

AR （augmented reality）增强现实 《ARKit开发实践》
详： 把现实世界和虚拟内容融合到一起，形成了各种效果。

有关的几个R： VR（虚拟现实） MR（混合现实） AR（增强现实）


				   			混合现实
	<—————————————————— mixed reality ———————————————————>
	现实环境        增强现实        增强虚拟 		虚拟环境
    real 		   augmented      augmented		virtual
    environment    reality   	virtuality 		environment


<h3>结构组成：</h3>
![AR有关实现的结构](../../../../asset/Snip20190215_6.png)
key: 
1) 如何获取用户的位姿势（位置和角度）
2）如何获取用户的交互指令
3）如何显示叠加后的场景内容

<h4>SLAM</h4>
simultaneous localization and mapping 及时廷尉与地图构建
是值一个搭载传感器（IMU或者摄像头）
主要解决问题： 定位 + 地图构建
地位：  估算自身在环境中的位置
地图构建： 识别所处环境的模型【也就是在定位的基础上构建环境的增量式地图】

SLAM分为两类： （1）纯视觉 （2）视觉惯性传感器（IMU）


1）视觉SLAM （visual SLAM）
只搭载了相机，只能够获取图像信息，从图像中获取特征带你，然后进行特征匹配，以此来估算用户的位姿。【相机： 值的单目相机，双目相机，深度摄像头】

流程：
（1）信息的采集和读取  【通过摄像头擦剂到图像序列或者视频流】
（2）视觉里程计（前端） 【相当于整个流程的前端，分析相邻帧图像之间的变换关系，利用图像序列或者视频流来估算相机的运动，并构造场景的控件结构，， 主要讨论相邻之间的运动关系】
（3）后台优化 【传感器等因素影响，会出现误差（噪声），这一步可以得到全局一直的轨迹和地图】
（4）闭环检测 【主要解决位置随时间漂移的问题】
（5）建图  【根据后端优化的轨迹，实时简历与任务要求对应的地图】


2） 视觉 + IMU SLAM
IMU可以和摄像头行程互补
（1）IMU测量设备的加速度和角速度，测量值会会出现漂移，短时间的快速移动，IMU估算的效果会很有效
（2）IMU在相机画面方面漂移情况会少很多； 设备放在桌子上，IMU估算会出现漂移，相机画面也不会变，纯粹视觉估算的设备位姿也不会变，这个时候摄像头估算的数据可以对IMU估算的数据进行校正。
（3）设备固定不动，场景发生变化；这个时候摄像机会发生变化，摄像头会认为设备在移动。

视觉 + IMU SLAM 形式称作： VIO（visual inertial odometry）视觉惯性里程计

AR历史（略过）
AR发展现状：
当前AR开发基本采用Unity 3D游戏引擎引入AR SDK ，同时大部分SDK可以直接接入Android 、iOS 移动端进行开发。

（1）google class 谷歌眼睛
（2）Hololens 微软的产品
（3）Magic Leap 
（4）Impression Pi 
（5）HoloSEER
（6）HIAR Glasses
（7）Leap Motion

AR软件：
（1）ARToolKit 奈良先端科学技术学院的加藤宏开发
（2）Metaio  初创公司开发
（3）vuforia 高通推出
（4）Wikitude 移动增强技术提供商Wikitude开发
（5）亮风台HiAR 国内AR sdk提供商
（6）视辰 EasyAR 视辰科技开发


AR内容
Google Tango引擎（2014） ARCore(2017） HoloLens (MR 2016)
Facebook AR开发平台爱camera effects platform 
apple 收购AR引擎开发商Metaio ， 引入ATeamAR 程序开发包

（1）原深感摄像头（trueDepth camera）
（2）设计跟踪、场景理解、集合渲染、人脸跟踪




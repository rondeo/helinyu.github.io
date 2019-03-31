---
title: ios 上架被拒可能遇到的问题
date: 2019-03-31 10:31:24
tags: iOS
categories: iOS
---

<h1>这里对iOS上架被拒可能遇到的问题的列表</h1>
<hr/>

<font color="green" size="4">1、Q1</font>
Guideline 2.5.1 - Performance - Software Requirements
We noticed that your app uses HealthKit, but your app does not appear to include any primary features that require health or fitness data. 
The intended use of HealthKit is to share health or fitness data with other apps or devices, and it should be used only in apps that require this data as a part of the app's core functionality. 
Next Steps
To resolve this issue, please remove any HealthKit functionality from your app, as well as any references to this app’s interactivity with HealthKit from the app or its metadata.
PS :
healthkit 出现的问题内容；
描述中申请了资源，但是没有使用；
info.plist 文件里面设置了healthkit上面的内容；
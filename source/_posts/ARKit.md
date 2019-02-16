---
title: ARKit
date: 2019-02-15 16:30:18
tags: AR
categories: AR
---

ARKt 苹果系统框架，类似foundation ，core animation ，uikit等，不需要考虑打包的大小
涉及到的领域： 相机视觉、传感器融合、相机调校、惯性视觉导航、光照估算、SLAM
第三方引擎： Unity、 Unreal Engine（虚幻引擎）

ARKit分为4个模块进行处理：
1）世界跟踪 （VIO（visual inertial Odometry）视觉惯性里程计） 技术实现跟踪设备的位置和姿态变化；
详解： 以设备初始位置为原点，然后将相机画面、惯性传感器（IMU）数据进行融合，这样就可以不需要对外部环境进行设置、不需要预先知道外部环境、不需要被手机增加额外传感器的情况下，精确跟踪设备在所处环境中的运动变化。 也就是对显示世界的运动进行跟踪，所以定义为： 世界跟踪

2）场景理解
  【获取手机运动轨迹和姿态变化之后，在相机画面中添加虚拟的集合模型】
（1）结婚模型要添加到画面的什么地方
（2）集合模型自身的管早亮度如何根据手机所处环境的光照来设定？
目的： 几何模型和真实环境相匹配 ————————>ARKit提供场景理解的能力
定义：指的是手机通过一系列的软件算法分析相机图像而得到手机所处在环境的信息。
通过在图像中提取到特征点来估算场景中的水平面（比如：地板、桌子），然后在使用hit-test 功能，在水平面上或者其他地方找到合适的地方放置几何模型。 + 光照条件

3）几何渲染
将几何模型从三维模型转换为二维图像，需要考虑到手机位资信息，场景信息，光照亮度等
前面两个步骤已经得到了这些信息，但是并没有ARKit并没有渲染能力， 这个部分需要其他的渲染引擎进行工作。

可选： sceneKit(3D) /spriteKit(2D) 、Metal框架， 第三方游戏引擎Unity、Unreal Engine
ARKit 最低支持到Apple A9 处理器。

4）人脸跟踪
和前面三个模块不同， 只适应到iphone X 以及之后的设备中。 
iphone X配有原深感摄像头（TrueDepth Camera），可以高度精确且实时地检测用户脸部位置、脸部拓步和用户表情。
![ARKit的结构](../../../../asset/Snip20190215_7.png)


<h2>AR 上面的项目初体验</h2>

项目的创 create a new xcode project ————> augmented reality app  出现对应的界面，选择编程的语言oc/swift 还有一个是content Technology [渲染引擎]
![创建AR项目的时候选择项](../../../../asset/Snip20190215_9.png "创建AR项目的时候选择项")

<div  align="center">    
![选择了Scenekit的目录](../../../../asset/Snip20190215_10.png  "选择了Scenekit的目录")
上面的结构多了一个art.scnassets 资源文件夹，文件夹里面又分为了3个文件：
ship.cn： 是sceneKit的场景文件
setting.json : 对应的设置
texture.png 着色的图片
</div>

项目必须运行到真机上， 若是出现： unable to run the session , configuration is not supported on this device ， 白鸥是当前的设备不支持AR；

<font color=red size=4 >SceneKit的内容：</font>
![选择了Scenekit的目录](../../../../asset/WechatIMG621.jpeg
  "初始化运行到手机上面的结果")

![AR](../../../../asset/Snip20190215_11.png  "创建完成了之后，默认的占位代码")
<br/>

<h4>下面详细了解一下对应的ARSCNView 的内容：</h4>
```
/**
这个视图（view）整合了ARSession到Scenekit中渲染
view 绘制是在相机的后台绘画，提供和更新一个相机，管理秒点（anchors） 节点和更新光线（lighting）。
 */
API_AVAILABLE(ios(11.0))  // 注意到是11 版本之后才会有的
@interface ARSCNView : SCNView

// 渲染的代理
@property (nonatomic, weak, nullable) id<ARSCNViewDelegate> delegate;

这个session是用来提供给view去根性场景的（scene）
@property (nonatomic, strong) ARSession *session;

指定view 的场景
@property (nonatomic, strong) SCNScene *scene;

// 确定是否view将会更新scene的光线，讨论当设置，view将会自动创建和更新光线对于光的评估对于会话的提供，默认是YES。
@property (nonatomic, assign) BOOL automaticallyUpdatesLighting;// 自动更新光线

 查找到scene的anchor通过提供的node
- (nullable ARAnchor *)anchorForNode:(SCNNode *)node;

 获取和指定的anchor映射的node（节点）。
- (nullable SCNNode *)nodeForAnchor:(ARAnchor *)anchor;

/**
搜索当前的帧和view上的点对应的对象。
讨论：
point: coordinate system , 
types: 查找的类型
return: 返回一个hit-test 的所有结果，从近到远排序

一个2D点在view的坐标空间中能够关联到一条直线上
在3D坐标控件中，hit-test 查找对象在时间的本地关于这个直线上。
*/
- (NSArray<ARHitTestResult *> *)hitTest:(CGPoint)point types:(ARHitTestResultType)types;


/**
 Unproject a 2D point from the view onto a plane in 3D world coordinates.
 
 @discussion A 2D point in the view’s coordinate space can refer to any point along a line segment
 in the 3D coordinate space. Unprojecting gets the 3D position of the point along this line segment that intersects the provided plane.
 @param point A point in the view’s coordinate system.
 @param planeTransform The transform used to define the coordinate system of the plane.
 The coordinate system’s positive Y axis is assumed to be the normal of the plane.
 @return 3D position in world coordinates or a NAN values if unprojection is not possible.
 */
- (simd_float3)unprojectPoint:(CGPoint)point ontoPlaneWithTransform:(simd_float4x4)planeTransform API_AVAILABLE(ios(12.0)) NS_REFINED_FOR_SWIFT;

@end


#pragma mark - ARSCNViewDelegate


API_AVAILABLE(ios(11.0))
@protocol ARSCNViewDelegate <SCNSceneRendererDelegate, ARSessionObserver>
@optional

- (nullable SCNNode *)renderer:(id <SCNSceneRenderer>)renderer nodeForAnchor:(ARAnchor *)anchor;
- (void)renderer:(id <SCNSceneRenderer>)renderer didAddNode:(SCNNode *)node forAnchor:(ARAnchor *)anchor;
- (void)renderer:(id <SCNSceneRenderer>)renderer willUpdateNode:(SCNNode *)node forAnchor:(ARAnchor *)anchor;
- (void)renderer:(id <SCNSceneRenderer>)renderer didUpdateNode:(SCNNode *)node forAnchor:(ARAnchor *)anchor;
- (void)renderer:(id <SCNSceneRenderer>)renderer didRemoveNode:(SCNNode *)node forAnchor:(ARAnchor *)anchor;

@end

下面是一下常量

typedef SCNDebugOptions ARSCNDebugOptions API_AVAILABLE(ios(11.0));

展示场景的原始世界
API_AVAILABLE(ios(11.0))
FOUNDATION_EXTERN const SCNDebugOptions ARSCNDebugOptionShowWorldOrigin NS_SWIFT_NAME(ARSCNDebugOptions.showWorldOrigin);

展示在时间上阿敏的3D特色点
API_AVAILABLE(ios(11.0))
FOUNDATION_EXTERN const SCNDebugOptions ARSCNDebugOptionShowFeaturePoints NS_SWIFT_NAME(ARSCNDebugOptions.showFeaturePoints);

```

<font color=red size=4 >SpriteKit的内容：</font>
<div  align="center">    
![Sprite](../../../../asset/Snip20190215_13.png
  "SpriteKit 创建默认的项目结构")
多了一个scene.sks 文件 ， 这个是一个场景文件
和scene.m 和scene.h文件
<div>

![sprite 初始化项目的截图](../../../../asset/WechatIMG622.jpeg
  "sprite 初始化项目的截图【注意点击一下图片屏幕才会展示虚拟模型图片】")
显示的是2D效果，为什么不是正常的2D效果？ ：
spritekit 会把2D图像以漂浮的方式放置在3D控件中，就类似于将一个广告牌放置在某个地方
，当你移动设备的时候，这几个广告牌始终是向着你的，同sceneKit适配效果是一样的。

看到viewcontroller里面的代码， 加载场景的过程：
![Sprite](../../../../asset/Snip20190215_14.png
  "viewcontroller里面的代码")
![Sprite](../../../../asset/Snip20190215_15.png
  "sprite delegate 的代理方法")
  ![Sprite](../../../../asset/Snip20190215_16.png
  "自定义的scene的内容")


```
ARSKView 的内容

代理方法
#pragma mark ARSKViewDelegate
API_AVAILABLE(ios(11.0))
@protocol ARSKViewDelegate <SKViewDelegate, ARSessionObserver>
@optional
- (nullable SKNode *)view:(ARSKView *)view nodeForAnchor:(ARAnchor *)anchor;
- (void)view:(ARSKView *)view didAddNode:(SKNode *)node forAnchor:(ARAnchor *)anchor;
- (void)view:(ARSKView *)view willUpdateNode:(SKNode *)node forAnchor:(ARAnchor *)anchor;
- (void)view:(ARSKView *)view didUpdateNode:(SKNode *)node forAnchor:(ARAnchor *)anchor;
- (void)view:(ARSKView *)view didRemoveNode:(SKNode *)node forAnchor:(ARAnchor *)anchor;

@end

#pragma mark ARSKView

/**
一个view继承了ARSession在SpriteKit上渲染
讨论：这个view在相机后台绘画，和项目和匹配锚点到节点中。

API_AVAILABLE(ios(11.0))
@interface ARSKView : SKView

@property (nonatomic, weak, nullable) NSObject <ARSKViewDelegate> *delegate; 代理

@property (nonatomic, strong) ARSession *session; // 绘画

- (nullable ARAnchor *)anchorForNode:(SKNode *)node;
- (nullable SKNode *)nodeForAnchor:(ARAnchor *)anchor;
- (NSArray<ARHitTestResult *> *)hitTest:(CGPoint)point types:(ARHitTestResultType)types;
和sceneKit的接口一样
@end
```
<font color=red size=4 > Metal</font>
<div>
![metal](../../../../asset/Snip20190215_17.png
  "metal 创建项目的默认结构")
  Metal 项目中没有资源文件， 但是有一个metal文件，是用于编写shaders（着色器）的。
</div>
可以详细阅读里面的代码， shader.metal 这个文件类似于openGL的shader.sh文件。
metal的学习应该多点查看对应的openGL里面的内容。







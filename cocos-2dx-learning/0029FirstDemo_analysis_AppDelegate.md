### AppDelegate 分析

#### AppDelegate 类
```
The cocos2d Application.
Private inheritance here hides part of interface from Director.

cocos2d 的应用类
封装部分来自Director的接口
```

#### 重点公共方法
- virtual bool applicationDidFinishLaunching()
```
Implement Director and Scene init code here.
@return true    Initialize success, app continue.
@return false   Initialize failed, app terminate.

应用启动完成时调用，在这实现导演（Director）和场景（Scene）的初始化
```
<br>

- virtual void applicationDidEnterBackground()
```
Called when the application moves to the background
@param  the pointer of the application

应用切到后台时调用
```
<br>

- virtual void applicationWillEnterForeground()
```
Called when the application reenters the foreground
@param  the pointer of the application

应用重新切到前台时调用
```
<br>

- 综上
1. AppDelegate 用于宏观是管理应用状态
### Optimizations for OPPO devices  OPPO设备优化
[原文 Optimizations for OPPO devices](https://docs.cocos2d-x.org/cocos2d-x/v4/en/advanced_topics/oppo.html) 
<br>
<br>


#### OPPO设备的优化
注意：此文档仅适用于Cocos2d-x 3.17.2及更高版本。Cocos2d-x对OPPO设备进行了一些优化。这些优化仅在OPPO设备（特别是Reno设备）上生效。

#### 优化的内容
有两个地方进行了优化：

1. 加载场景
2. 引擎内部的着色器编译

加载场景的优化从场景创建开始，结束于Scene::onEnter()，因此你应该在它们之间创建资源。<br>

#### 手动调用优化代码
应用程序知道何时需要更多的功率，比引擎更了解情况。你可以调用此API在需要时获得更多的功率。你可以在C++或Java中调用此API。

C++示例用法：
```cpp
// 通知设备发生事件，比如开始加载一个场景。
// 在v3.17.2后可用。
#if CC_TARGET_PLATFORM == CC_PLATFORM_ANDROID
    DataManager::setOptimise(const string&, const string&);
#end if

// 场景加载开始，需要更多的功率。
#if CC_TARGET_PLATFORM == CC_PLATFORM_ANDROID
    DataManager::onSceneLoaderBegin();
#end if

// 场景加载结束。
#if CC_TARGET_PLATFORM == CC_PLATFORM_ANDROID
    DataManager::onSceneLoaderEnd();
#end if

// 着色器编译开始，需要更多的功率。
#if CC_TARGET_PLATFORM == CC_PLATFORM_ANDROID
    DataManager::onShaderLoaderBegin();
#end if

// 着色器编译结束。
#if CC_TARGET_PLATFORM == CC_PLATFORM_ANDROID
    DataManager::onShaderLoaderEnd();
#end if
```

Java示例用法：
```java
Cocos2dxDataManager::setOptimise(String thing, float value);
```

数值表
```
任务		1		0
load_scene	开始		结束
shader_compile	开始		结束
```
在v3.17.2之后，数值的类型从float更改为string，以使其更易用。<br>
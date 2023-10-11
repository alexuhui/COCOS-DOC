### Advanced audio functionality  高级音频功能
[原文 Advanced audio functionality](https://docs.cocos2d-x.org/cocos2d-x/v4/en/audio/advanced.html) 
<br>
<br>

#### 设置
使用 SimpleAudioEngine API 很容易入门。在使用音频时，特别是在移动设备上（如手机和平板电脑）操作时，需要考虑一些因素。当您在手机上执行多任务并在应用程序之间切换时会发生什么？或者当有电话呼入时会发生什么？您需要在游戏中处理这些异常情况。幸运的是，我们在这里帮助您。<br>

在 AppDelegate.cpp 中，注意以下方法：<br>

```cpp
// This function will be called when the app is inactive. When comes a phone call,
// it's be invoked too
void AppDelegate::applicationDidEnterBackground() {
    Director::getInstance()->stopAnimation();

    // if you use SimpleAudioEngine, it must be pause
    // SimpleAudioEngine::getInstance()->pauseBackgroundMusic();
}

// this function will be called when the app is active again
void AppDelegate::applicationWillEnterForeground() {
    Director::getInstance()->startAnimation();

    // if you use SimpleAudioEngine, it must resume here
    // SimpleAudioEngine::getInstance()->resumeBackgroundMusic();
}
```

注意 SimpleAudioEngine 的注释行吗？如果您正在使用音频进行背景音乐和音效，请确保取消对这些行的注释。<br>

#### 预加载声音
当游戏启动时，您可能希望预加载音乐和效果，以便在需要时立即使用。<br>

```cpp
#include "SimpleAudioEngine.h"
using namespace CocosDenshion;

auto audio = SimpleAudioEngine::getInstance();

// 预加载背景音乐和音效。您可以预加载音效，例如在应用程序启动时，以便在您想使用它们时已经加载。
audio->preloadBackgroundMusic("myMusic1.mp3");
audio->preloadBackgroundMusic("myMusic2.mp3");

audio->preloadEffect("myEffect1.mp3");
audio->preloadEffect("myEffect2.mp3");

// 从缓存中卸载声音。如果您完成了一个声音并且在游戏中不再使用它，请将其卸载以释放资源。
audio->unloadEffect("myEffect1.mp3");
```

#### 音量
您可以通过编程方式增加和减少声音和音乐的音量。

```cpp
#include "SimpleAudioEngine.h"
using namespace CocosDenshion;

auto audio = SimpleAudioEngine::getInstance();

// 将音量设置为指定的浮点值
audio->setEffectsVolume(0.5);
audio->setBackgroundMusicVolume(0.5);
```
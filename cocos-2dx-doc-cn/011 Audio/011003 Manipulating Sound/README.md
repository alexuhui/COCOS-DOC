### Manipulating Sound  操纵声音
[原文 Manipulating Sound](https://docs.cocos2d-x.org/cocos2d-x/v4/en/audio/operations.html) 
<br>
<br>


#### 暂停、停止和恢复音乐和音效
在开始播放音乐和音效后，您可能需要在某些操作之后暂停、停止或恢复。这可以很容易地完成。

1. 暂停
```cpp
#include "SimpleAudioEngine.h"
using namespace CocosDenshion;

auto audio = SimpleAudioEngine::getInstance();

// 暂停背景音乐。
audio->pauseBackgroundMusic();

// 暂停音效。
audio->pauseEffect();

// 暂停所有音效。
audio->pauseAllEffects();
```

2. 停止
```cpp
#include "SimpleAudioEngine.h"
using namespace CocosDenshion;

auto audio = SimpleAudioEngine::getInstance();

// 停止背景音乐。
audio->stopBackgroundMusic();

// 停止音效。
audio->stopEffect();

// 停止所有运行中的音效。
audio->stopAllEffects();
```

3. 恢复
```cpp
#include "SimpleAudioEngine.h"
using namespace CocosDenshion;

auto audio = SimpleAudioEngine::getInstance();

// 恢复背景音乐。
audio->resumeBackgroundMusic();

// 恢复音效。
audio->resumeEffect();

// 恢复所有音效。
audio->resumeAllEffects();
```
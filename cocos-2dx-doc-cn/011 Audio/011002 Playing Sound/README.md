### Playing Sound  播放声音
[原文 Playing Sound](https://docs.cocos2d-x.org/cocos2d-x/v4/en/audio/getting_started.html) 
<br>
<br>


#### 播放背景音乐
播放用作背景音乐的音频文件。这可以连续重复播放。

```cpp
#include "SimpleAudioEngine.h"
using namespace CocosDenshion;

auto audio = SimpleAudioEngine::getInstance();

// 设置背景音乐并持续播放。
audio->playBackgroundMusic("mymusic.mp3", true);

// 设置背景音乐并仅播放一次。
audio->playBackgroundMusic("mymusic.mp3", false);
```

#### 播放音效
播放音效。

```cpp
#include "SimpleAudioEngine.h"
using namespace CocosDenshion;

auto audio = SimpleAudioEngine::getInstance();

// 播放音效，仅一次。
audio->playEffect("myEffect.mp3", false, 1.0f, 1.0f, 1.0f);
```
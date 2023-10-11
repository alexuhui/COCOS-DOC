### Transitioning  场景过渡
[原文 Transitioning](https://docs.cocos2d-x.org/cocos2d-x/v4/en/scenes/transitioning.html) 
<br>
<br>

在游戏中，你可能需要在场景之间切换。也许开始一个新游戏，切换关卡，甚至结束游戏。Cocos2d-x提供了许多方法来执行场景过渡。<br>

切换场景的方式<br>
有许多通过场景的方式，每种都具有特定的功能。让我们逐个了解。给定：<br>

```cpp
auto myScene = Scene::create();
```

- runWithScene() - 仅在第一个场景中使用。这是启动游戏的第一个场景的方法。<br>

```cpp
Director::getInstance()->runWithScene(myScene);
```

- replaceScene() - 直接替换场景。<br>

```cpp
Director::getInstance()->replaceScene(myScene);
```

- pushScene() - 暂停运行场景的执行，将其推送到暂停场景的堆栈上。只有在有正在运行的场景时才调用此方法。<br>

```cpp
Director::getInstance()->pushScene(myScene);
```

- popScene() - 这个场景将替换当前正在运行的场景。当前运行的场景将被删除。只有在有正在运行的场景时才调用此方法。<br>

```cpp
Director::getInstance()->popScene();
```

带有效果的过渡场景<br>
你可以为场景过渡添加视觉效果。<br>

```cpp
auto myScene = Scene::create();

// 渐变淡出
Director::getInstance()->replaceScene(TransitionFade::create(0.5, myScene, Color3B(0,255,255)));

// FlipX
Director::getInstance()->replaceScene(TransitionFlipX::create(2, myScene));

// 从上方滑入的过渡
Director::getInstance()->replaceScene(TransitionSlideInT::create(1, myScene));
```

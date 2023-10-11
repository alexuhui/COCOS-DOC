### Director  导演
[原文 Director](https://docs.cocos2d-x.org/cocos2d-x/v4/en/basic_concepts/director.html) 
<br>
<br>

Cocos2d-x采用了导演（Director）的概念，就像在电影中一样！导演对象控制操作的流程并告诉必要的接收者该做什么。想象一下自己是执行制片人，你告诉导演要做什么！一个常见的导演任务是控制场景替换和转场。导演是一个共享的单例（有效地，一次只有一个类的实例），你可以在代码的任何地方调用它。<br>

这是一个典型游戏流程的示例。导演通过这个流程，根据你的游戏标准进行决策：<br>

![游戏流程图](scenes.png)

你是你游戏的导演。你决定发生什么，什么时候发生，以及如何发生。掌握主动权！<br>

**如何引起导演的注意？**
要与导演互动，你需要呼叫它。有几种方法可以做到这一点：

```cpp
// 获取导演，然后使用它
auto director = cocos2d::Director::getInstance();
director->runWithScene(scene);

// 为每个操作获取导演（不建议重复请求）
auto s = cocos2d::Director::getInstance()->getWinSize();
```

**导演能做哪些事情？**
导演有许多责任，甚至有更多的可能性。如上所述，导演控制整个展示。以下是导演可以轻松完成的一些有用的事情：

- **场景（Scenes）**：更改场景，使用过渡效果更改场景等...

```cpp
director->runWithScene(scene); // 在启动游戏时使用

director->replaceScene(scene2); // 在从当前场景更改到另一个场景时使用
```

- **暂停/恢复**：暂停你的游戏（如果使用物理引擎，则需要更多步骤）

```cpp
// 停止动画
cocos2d::Director::getInstance()->stopAnimation();

// 恢复动画
cocos2d::Director::getInstance()->startAnimation();
```

- **获取内部信息**：获取/设置你游戏的属性。查阅API参考以获取更多功能。

```cpp
// 打开显示FPS
cocos2d::Director::GetInstance()->setDisplayStats(true);

// 设置FPS。如果你不调用这个，默认值是1.0/60
cocos2d::Director::GetInstance()->setAnimationInterval(1.0f / 60);

// 设置内容比例因子
cocos2d::Director::GetInstance()->setContentScaleFactor(....);
```

**让我们构建一个游戏 - 第3步**
在上一步中，我们探讨了AppDelegate类及其功能。在下一章中，我们将探索场景。在进入那之前，我们应该进行一些基本的设置。

**资源**
每个游戏至少都会有一些资源。这些资源可能是字体、音效、音乐或精灵。在这个示例游戏中，我们首先将使用简单的形状，直到我们的游戏可玩。在后面的阶段，我们可以使用真正的艺术品。<br>

继续... <br>
### Creating a Scene  创建场景
[原文 Creating a Scene](https://docs.cocos2d-x.org/cocos2d-x/v4/en/scenes/creating.html) 
<br>
<br>

很容易创建一个场景<br>

```cpp
auto myScene = Scene::create();
```

还记得场景图吗？<br>

在本指南的第2章，我们学到了场景图以及它如何影响游戏的绘制。重要的是要记住，这定义了GUI元素的绘制顺序。还记得Z轴顺序！<br>

一个简单的场景<br>

让我们建立一个简单的场景。记住，Cocos2d-x使用右手坐标系统。这意味着我们的(0,0)坐标位于屏幕/显示的左下角。当你开始定位游戏元素时，这是你应该从中开始计算的地方。让我们创建一个简单的场景并向其中添加一些元素：<br>

```cpp
auto dirs = Director::getInstance();
Size visibleSize = dirs->getVisibleSize();

auto myScene = Scene::create();

auto label1 = Label::createWithTTF("My Game", "Marker Felt.ttf", 36);
label1->setPosition(Vec2(visibleSize.width / 2, visibleSize.height / 2));

myScene->addChild(label1);

auto sprite1 = Sprite::create("mysprite.png");
sprite1->setPosition(Vec2(100, 100));

myScene->addChild(sprite1);
```

当我们运行这段代码时，我们将看到一个包含标签和精灵的简单场景。它并没有做太多事情，但这是一个开始。<br>

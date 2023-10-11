### Physics is scary, do I really need it? Please tell me no!  物理太可怕了，我真的需要她吗？请对我说不！
[原文 Physics is scary, do I really need it? Please tell me no!](https://docs.cocos2d-x.org/cocos2d-x/v4/en/physics/getting_started.html) 
<br>
<br>

#### 物理学可能看起来吓人，但我真的需要吗？请告诉我不需要！
请不要逃跑，床底下没有物理学怪物！你的需求可能足够简单，不需要使用物理引擎。也许使用 Node 对象的 update() 函数、Rect 对象以及 containsPoint() 或 intersectsRect() 函数的组合就足够了？例如：

```cpp
void update(float dt)
{
  auto p = touch->getLocation();
  auto rect = this->getBoundingBox();

  if(rect.containsPoint(p))
  {
      // 做一些事情，发生交叉
  }
}
```

这种机制适用于非常简单的需求，但不具备可扩展性。如果你有 100 个 Sprite 对象，都在不断地更新以检查与其他对象的交叉，可能是可行的，但 CPU 使用率和帧率会严重受到影响。你的游戏将无法玩。物理引擎以一种可扩展且对 CPU 友好的方式解决了这些问题。尽管这可能看起来陌生，让我们看一个简单的例子，然后将这个例子、术语和最佳实践结合起来。

```cpp
// 创建一个静态的 PhysicsBody
auto physicsBody = PhysicsBody::createBox(Size(65.0f , 81.0f ), PhysicsMaterial(0.1f, 1.0f, 0.0f));
physicsBody->setDynamic(false);

// 创建一个精灵
auto sprite = Sprite::create("whiteSprite.png");
sprite->setPosition(Vec2(400, 400));

// 精灵将使用 physicsBody
sprite->addComponent(physicsBody);

// 添加接触事件侦听器
auto contactListener = EventListenerPhysicsContact::create();
contactListener->onContactBegin = CC_CALLBACK_1(onContactBegin, this);
_eventDispatcher->addEventListenerWithSceneGraphPriority(contactListener, this);
```

尽管这个例子很简单，看起来复杂且吓人。但如果我们仔细看，其实并不复杂。这里发生的步骤有：

1. 创建一个 PhysicsBody 对象。
2. 创建一个 Sprite 对象。
3. Sprite 对象应用 PhysicsBody 对象的属性。
4. 创建一个侦听器以响应 onContactBegin() 事件。

一步一步来看，这个概念就开始变得清晰了。

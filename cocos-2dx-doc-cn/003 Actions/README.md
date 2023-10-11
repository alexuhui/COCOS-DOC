### Actions  动作
[原文 Actions](https://docs.cocos2d-x.org/cocos2d-x/v4/en/actions/) 
<br>
<br>

动作对象就像它们的名字一样。它们使一个 Node 执行对其属性的更改。动作对象允许在时间上对 Node 属性进行转换。任何具有 Node 基类的对象都可以执行动作对象。例如，您可以将 Sprite 从一个位置移动到另一个位置，并在一段时间内执行此操作。<br>

MoveTo 和 MoveBy 动作的示例：<br>

```cpp
// 将精灵移动到 50,10 的位置，耗时 2 秒。
auto moveTo = MoveTo::create(2, Vec2(50, 10));
mySprite1->runAction(moveTo);

// 将精灵向右移动 20 个点，耗时 2 秒。
auto moveBy = MoveBy::create(2, Vec2(20,0));
mySprite2->runAction(moveBy);
```

让我们开始使用动作吧！

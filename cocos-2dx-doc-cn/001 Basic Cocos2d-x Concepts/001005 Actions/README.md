### Actions 动作
[原文 Actions](https://docs.cocos2d-x.org/cocos2d-x/v4/en/basic_concepts/actions.html) 
<br>
<br>

创建一个场景并在屏幕上添加精灵对象只是我们需要做的一部分。要使游戏成为游戏，我们需要让东西在屏幕上移动！动作对象是每个游戏的重要组成部分。动作允许在时间空间内对节点对象进行变换。想要将一个精灵从一个点移动到另一个点，并在完成时使用回调？没问题！你甚至可以创建一个在节点上执行的动作项序列。你可以更改节点的属性，如位置、旋转和缩放。示例动作：MoveBy（移动）、Rotate（旋转）、Scale（缩放）。所有的游戏都使用动作。<br>

看一下本章示例代码，这里是动作的工作方式：<br>

![（动作的例子）](../001004%20Sprites/2n_level1_action_start.png)<br>

5秒后，精灵将移动到一个新的位置：<br>

![（移动动作后的例子）](../001004%20Sprites/2n_level1_action_end.png)<br>

创建动作对象非常简单：<br>

```cpp
auto mySprite = Sprite::create("Blue_Front1.png");

// 将精灵向右移动50个像素，并向上移动10个像素，持续2秒。
auto moveBy = MoveBy::create(2, Vec2(50,10));
mySprite->runAction(moveBy);

// 将精灵移动到指定位置，持续2秒。
auto moveTo = MoveTo::create(2, Vec2(50,10));
mySprite->runAction(moveTo);
```
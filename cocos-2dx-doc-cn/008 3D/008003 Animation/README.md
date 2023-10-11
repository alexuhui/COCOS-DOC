### Animation  动作
[原文 Animation](https://docs.cocos2d-x.org/cocos2d-x/v4/en/3d/animation.html) 
<br>
<br>

#### 动作
Sprite3D对象是游戏中不可或缺的一部分！我们已经学会了如何操作它们。然而，我们可能想要更丰富的体验。进入动画！要运行3D动画，可以使用Animation3D和Animate3D对象。然后使用Animation3D对象创建一个Animate3D动作。示例：

```cpp
// 动画包含在.c3b文件中
auto animation = Animation3D::create("orc.c3b");

// 使用Animation对象创建Action
auto animate = Animate3D::create(animation);

// 运行动画
sprite->runAction(RepeatForever::create(animate));
```

运行示例中的程序员指南示例代码，以看到它实际运行的效果！请记住，3D动画与2D完全相同的概念。请参考本指南中的第4章。

#### 多个动画
当您想同时运行多个动画时，该怎么办？使用动画开始时间和动画长度参数，您可以创建多个动画。这两个参数的单位都是秒。示例：

```cpp
auto animation = Animation3D::create(fileName);

auto runAnimate = Animate3D::create(animation, 0, 2);
sprite->runAction(runAnimate);

auto attackAnimate = Animate3D::create(animation, 3, 5);
sprite->runAction(attackAnimate);
```

在上面的示例中，有两个动画要运行。第一个立即开始，持续2秒。第二个在3秒后开始，持续5秒。

#### 动画速度
动画的速度是正整数表示正向，而负速度表示反向。在这种情况下，速度设置为10。这意味着这个动画可以被视为10秒的长度。

#### 动画混合
在使用多个动画时，自动在每个动画之间应用混合。混合的目的是在效果之间创建平滑的过渡。给定两个动画A和B，动画A的最后几帧和动画B的第一帧重叠，以使动画的变化看起来自然。<br>

默认的过渡时间为0.1秒。您可以使用Animate3D::setTransitionTime设置过渡时间。<br>

Cocos2d-x仅支持关键帧之间的线性插值。这填补了曲线中的间隙，以确保平滑的路径。如果在模型制作中使用了其他插值方法，我们的内置工具fbx-conv将生成额外的关键帧进行补偿。这种补偿是根据目标帧完成的。有关fbx-conv的更多信息，请参考本章末尾关于它的讨论。<br>
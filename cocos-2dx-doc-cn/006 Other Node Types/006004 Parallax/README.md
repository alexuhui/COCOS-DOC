### Parallax  视差
[原文 Parallax](https://docs.cocos2d-x.org/cocos2d-x/v4/en/other_node_types/getting_started.html) 
<br>
<br>

视差节点（Parallax Node）是一种模拟视差滚动的特殊节点类型。你说什么？视差.. 什么？是的，视差。简单来说，你可以将视差节点视为一种特殊效果，使物体的位置或方向在不同位置观看时似乎有所不同。简单的日常例子包括通过相机的取景器和镜头观看。你可以想象许多以这种方式运行的游戏，超级马里奥兄弟就是一个经典的例子。视差节点对象可以通过序列（Sequence）以及鼠标、触摸、加速度计或键盘事件手动移动。<br>


视差节点比常规节点稍微复杂。为什么呢？因为它们需要使用多个节点才能正常工作。视差节点不能独自运行。你至少需要另外两个节点对象才能完成一个视差节点。和往常一样，在真正的Cocos2d-x风格中，创建视差节点非常简单：<br>


```cpp
// 创建视差节点
auto paraNode = ParallaxNode::create();
```

由于你需要多个节点对象，它们也很容易添加：<br>


```cpp
// 创建视差节点
auto paraNode = ParallaxNode::create();

// 将背景图像移动到0.4x、0.5y的比例
paraNode->addChild(background, -1, Vec2(0.4f, 0.5f), Vec2::ZERO);

// 瓦片以2.2x、1.0y的比例移动
paraNode->addChild(middle_layer, 1, Vec2(2.2f, 1.0f), Vec2(0, -200));

// 顶部图像以3.0x、2.5y的比例移动
paraNode->addChild(top_layer, 2, Vec2(3.0f, 2.5f), Vec2(200, 800));
```

好了，看起来和感觉都很熟悉，对吧？请注意一些事项！每个添加的节点对象都被赋予唯一的z-order，以便它们可以堆叠在彼此之上。还请注意在addChild()调用中额外添加了两个Vec2类型的参数。这些参数可以被视为相对于父节点的速度比率。<br>


在文本中很难展示视差节点，所以请运行示例程序员指南中的示例代码，看看它是如何运作的！<br>

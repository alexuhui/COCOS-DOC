### Scene 分析

#### 概念
```
Scene is a subclass of Node that is used only as an abstract concept.

Scene and Node are almost identical with the difference that Scene has its
anchor point (by default) at the center of the screen.

For the moment Scene has no other logic than that, but in future releases it might have
additional logic.

It is a good practice to use a Scene as the parent of all your nodes.
 
Scene will create a default camera for you.

Scene（场景）是 Node（节点）的一个子类，仅用作一个抽象概念。

Scene 和 Node 在几乎相同，区别在于 Scene 默认情况下在屏幕中心具有其锚点。

目前，Scene 除此之外没有其他逻辑，但在将来的版本中可能会添加额外的逻辑。

将 Scene 作为所有节点的父节点是一个良好的实践。

Scene 将为你创建一个默认的摄像机。
```

#### scene 是一个特殊的节点
Scene继承自Node, 是其它当前场景上的节点的根节点
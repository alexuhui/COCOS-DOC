### FixedPriority vs SceneGraphPriority  固定优先级 vs 场景图优先级
[原文 FixedPriority vs SceneGraphPriority](https://docs.cocos2d-x.org/cocos2d-x/v4/en/event_dispatcher/types.html) 
<br>
<br>

#### Fixed Priority 和 Scene Graph Priority 用于确定哪些事件侦听器将首先接收到事件。

1. **Fixed Priority（固定优先级）** 是一个整数值。具有较低优先级值的事件侦听器在具有较高优先级值的事件侦听器之前处理事件。

2. **Scene Graph Priority（场景图优先级）** 是一个指向 Node 的指针。其节点具有较高 z-order 值（即绘制在顶部）的事件侦听器会在具有较低 z-order 值（即绘制在底部）的事件侦听器之前接收事件。这确保了触摸事件等按前后顺序传递，正如你所期望的那样。

记得基本概念的那一章吗？我们谈到了场景图，还谈到了这张图：

![Scene Graph](./in-order-walk.png)

当使用 Scene Graph Priority 时，实际上是在向上遍历此树... I、H、G、F、E、D、C、B、A。如果触发了事件，H 将检查它并且可能吞噬它（下面会详细解释），或者让它传递到 I。同样，I 可能吞噬它或者让它传递到 G，依此类推，直到事件被吞噬或者没有被处理。
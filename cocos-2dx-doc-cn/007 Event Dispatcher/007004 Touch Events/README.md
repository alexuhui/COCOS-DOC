### Touch Events  触摸事件
[原文 Touch Events](https://docs.cocos2d-x.org/cocos2d-x/v4/en/event_dispatcher/touch.html) 
<br>
<br>

Touch 事件是移动游戏中最重要的事件。它们易于创建，并提供多功能功能。让我们确保知道什么是触摸事件。当您触摸移动设备的屏幕时，它会接受触摸，查看您触摸的位置，并决定您触摸了什么。然后，将回答您的触摸。可能您触摸的对象可能不是响应的对象，而可能是其下方的某物。触摸事件通常分配一个优先级，具有最高优先级的事件是回答的事件。以下是如何创建基本触摸事件侦听器：

```cpp
// 创建“one by one”触摸事件侦听器（一次处理一个触摸）
auto listener1 = EventListenerTouchOneByOne::create();

// 当按下时触发
listener1->onTouchBegan = [](Touch* touch, Event* event){
    // 您的代码
    return true; // 如果您正在消耗它
};

// 移动触摸时触发
listener1->onTouchMoved = [](Touch* touch, Event* event){
    // 您的代码
};

// 当您松开触摸时触发
listener1->onTouchEnded = [=](Touch* touch, Event* event){
    // 您的代码
};

// 添加侦听器
_eventDispatcher->addEventListenerWithSceneGraphPriority(listener1, this);
```

正如您所看到的，使用触摸事件侦听器时，有三个不同的事件，您可以在这些事件上采取行动。它们在调用它们的时间上各自有一个明确定义的时机。

- `onTouchBegan` 在按下时触发。
- `onTouchMoved` 在按下并移动对象时触发。
- `onTouchEnded` 在松开触摸时触发。
### There are 5 types of event listeners.  有5种事件监听器
[原文 There are 5 types of event listeners.](https://docs.cocos2d-x.org/cocos2d-x/v4/en/event_dispatcher/types.html) 
<br>
<br>

#### 有5种类型的事件监听器。

1. `EventListenerTouch` - 响应触摸事件
2. `EventListenerKeyboard` - 响应键盘事件
3. `EventListenerAcceleration` - 响应加速度计事件
4. `EventListenerMouse` - 响应鼠标事件
5. `EventListenerCustom` - 响应自定义事件

#### 吞噬事件
当你有一个监听器并且你希望一个对象接受它获得的事件时，你必须吞噬它。换句话说，你消耗它，这样它就不会传递给优先级较低的其他对象。这很容易做到。

```cpp
// 当 "swallow touches" 为 true 时，从 onTouchBegan 方法返回 'true' 将 "吞噬" 触摸事件，阻止其他监听器使用它。
listener1->setSwallowTouches(true);

// 你也应该在 onTouchBegan() 中返回 true
listener1->onTouchBegan = [](Touch* touch, Event* event){
    // 你的代码

    return true;
};
```
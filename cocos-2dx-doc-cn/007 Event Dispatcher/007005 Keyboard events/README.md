### Keyboard events  键盘事件
[原文 Keyboard events](https://docs.cocos2d-x.org/cocos2d-x/v4/en/event_dispatcher/keyboard.html) 
<br>
<br>

#### 键盘事件
对于桌面游戏，您可能会发现使用键盘机制很有用。Cocos2d-x 支持键盘事件。就像上面的触摸事件一样，创建键盘事件也很容易。

```cpp
// 创建键盘事件侦听器
auto listener = EventListenerKeyboard::create();
listener->onKeyPressed = CC_CALLBACK_2(KeyboardTest::onKeyPressed, this);
listener->onKeyReleased = CC_CALLBACK_2(KeyboardTest::onKeyReleased, this);

_eventDispatcher->addEventListenerWithSceneGraphPriority(listener, this);

// 键盘事件回调函数原型的实现
void KeyboardTest::onKeyPressed(EventKeyboard::KeyCode keyCode, Event* event)
{
        log("按下键：%d", keyCode);
}

void KeyboardTest::onKeyReleased(EventKeyboard::KeyCode keyCode, Event* event)
{
        log("释放键：%d", keyCode);
}
```

这里，我们创建了一个键盘事件侦听器，然后指定了按键按下和释放时的回调函数。在回调函数中，我们使用 `log` 函数记录按下或释放的键码。
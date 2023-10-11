### Mouse events  鼠标事件
[原文 Mouse events](https://docs.cocos2d-x.org/cocos2d-x/v4/en/event_dispatcher/mouse.html) 
<br>
<br>

#### 鼠标事件
与以往一样，Cocos2d-x 支持鼠标事件。

```cpp
_mouseListener = EventListenerMouse::create();
_mouseListener->onMouseMove = CC_CALLBACK_1(MouseTest::onMouseMove, this);
_mouseListener->onMouseUp = CC_CALLBACK_1(MouseTest::onMouseUp, this);
_mouseListener->onMouseDown = CC_CALLBACK_1(MouseTest::onMouseDown, this);
_mouseListener->onMouseScroll = CC_CALLBACK_1(MouseTest::onMouseScroll, this);

_eventDispatcher->addEventListenerWithSceneGraphPriority(_mouseListener, this);

void MouseTest::onMouseDown(Event *event)
{
    // 以演示事件....
    EventMouse* e = (EventMouse*)event;
    string str = "Mouse Down detected, Key: ";
    str += tostr(e->getMouseButton());
}

void MouseTest::onMouseUp(Event *event)
{
    // 以演示事件....
    EventMouse* e = (EventMouse*)event;
    string str = "Mouse Up detected, Key: ";
    str += tostr(e->getMouseButton());
}

void MouseTest::onMouseMove(Event *event)
{
    // 以演示事件....
    EventMouse* e = (EventMouse*)event;
    string str = "MousePosition X:";
    str = str + tostr(e->getCursorX()) + " Y:" + tostr(e->getCursorY());
}

void MouseTest::onMouseScroll(Event *event)
{
    // 以演示事件....
    EventMouse* e = (EventMouse*)event;
    string str = "Mouse Scroll detected, X: ";
    str = str + tostr(e->getScrollX()) + " Y: " + tostr(e->getScrollY());
}
```

在这里，我们创建了一个鼠标事件侦听器，分别处理了鼠标的按下、抬起、移动和滚动事件。这些事件处理函数中，我们使用 `EventMouse` 类的方法获取了有关鼠标事件的信息。
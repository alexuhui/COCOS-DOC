### Custom Events  自定义事件
[原文 Custom Events](https://docs.cocos2d-x.org/cocos2d-x/v4/en/event_dispatcher/custom.html) 
<br>
<br>

#### 自定义事件
上述的事件类型是由系统定义的，这些事件（如触摸屏、键盘响应等）由系统自动触发。此外，您可以创建自己的自定义事件，这些事件不是由系统触发的，而是由您的代码触发，如下所示：

```cpp
_listener = EventListenerCustom::create("game_custom_event1", [=](EventCustom* event){
    std::string str("Custom event 1 received, ");
    char* buf = static_cast<char*>(event->getUserData());
    str += buf;
    str += " times";
    statusLabel->setString(str.c_str());
});

_eventDispatcher->addEventListenerWithSceneGraphPriority(_listener, this);
```

上面定义了一个自定义事件侦听器，具有一个响应方法，并将其添加到事件分发器中。那么事件处理程序是如何触发的呢？看看下面的例子：

```cpp
static int count = 0;
++count;

char* buf[10];
sprintf(buf, "%d", count);

EventCustom event("game_custom_event1");
event.setUserData(buf);

_eventDispatcher->dispatchEvent(&event);
```

上述示例创建了一个 EventCustom 对象，并设置了其 UserData。然后，它被手动调度，使用 `_eventDispatcher->dispatchEvent(&event)`。这会立即触发先前定义的事件处理程序。处理程序立即调用，因此可以使用本地堆栈变量作为 UserData。
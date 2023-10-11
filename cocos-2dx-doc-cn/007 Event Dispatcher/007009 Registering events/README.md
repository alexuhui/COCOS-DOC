### Registering events with the dispatcher  向分发器注册事件
[原文 Registering events with the dispatcher](https://docs.cocos2d-x.org/cocos2d-x/v4/en/event_dispatcher/registering.html) 
<br>
<br>

#### 向分发器注册事件
向事件分发器注册事件非常简单。以前面示例中的触摸事件侦听器为例：

```cpp
// 添加监听器
_eventDispatcher->addEventListenerWithSceneGraphPriority(listener1, sprite1);
```

需要注意的是，每个对象只能注册一个触摸事件。如果需要为多个对象使用相同的监听器，应使用 `clone()`。

```cpp
// 添加监听器
_eventDispatcher->addEventListenerWithSceneGraphPriority(listener1, sprite1);

// 将相同的监听器添加到多个对象。
_eventDispatcher->addEventListenerWithSceneGraphPriority(listener1->clone(), sprite2);

_eventDispatcher->addEventListenerWithSceneGraphPriority(listener1->clone(), sprite3);
```

从分发器中删除事件
可以使用以下方法删除已添加的监听器：

```cpp
_eventDispatcher->removeEventListener(listener);
```

尽管它们可能看起来很特殊，但内置的 Node 对象以与我们讨论的相同的方式使用事件分发器。有道理吧？以菜单为例。当您拥有一个带有菜单项的菜单时，单击它们时会触发一个事件。您还可以在内置的 Node 对象上使用 `removeEventListener()`。
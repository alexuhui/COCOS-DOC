### EventDispatcher 分析

#### 概念
1. EventListener
```
The base class of event listener.
If you need custom listener which with different callback, 
you need to inherit this class.
For instance, you could refer to EventListenerAcceleration,
EventListenerKeyboard, EventListenerTouchOneByOne, EventListenerCustom.

事件监听的基类
```

2. EventDispatcher
```
This class manages event listener subscriptions
and event dispatching.

The EventListener list is managed in such a way that
event listeners can be added and removed even
from within an EventListener, while events are being
dispatched.

这个类管理事件监听器的订阅和事件分发。

事件监听器管理着一个监听列表，可以添加/移除事件，并通过
这个列表派发事件
```
<br>

#### 重点方法
- void addEventListenerWithSceneGraphPriority(EventListener* listener, Node* node)
```
Adds a event listener for a specified event with the priority of scene graph.
@param listener The listener of a specified event.
@param node The priority of the listener is based on the draw order of this node.
@note  The priority of scene graph will be fixed value 0. So the order of listener item
        in the vector will be ' <0, scene graph (0 priority), >0'.

按场景图优先级添加事件监听
```
[关于场景图](../cocos-2dx-doc-cn/001%20Basic%20Cocos2d-x%20Concepts/001003%20Scenes%20and%20the%20Scene%20Graph/README.md)
<br>

- void addEventListenerWithFixedPriority(EventListener* listener, int fixedPriority)
```
Adds a event listener for a specified event with the fixed priority.
@param listener The listener of a specified event.
@param fixedPriority The fixed priority of the listener.
@note A lower priority will be called before the ones that have a higher value.
      0 priority is forbidden for fixed priority since it's used for scene graph based priority.

指定优先级添加事件监听
优先级的值越小，越早调用
```
<br>

- EventListenerCustom* addCustomEventListener(const std::string &eventName, const std::function<void(EventCustom*)>& callback)
```
Adds a Custom event listener.
It will use a fixed priority of 1.
@param eventName A given name of the event.
@param callback A given callback method that associated the event name.
@return the generated event. Needed in order to remove the event from the dispatcher

添加自定义的事件监听
```
<br>

- void removeEventListener(EventListener* listener)
- void removeEventListenersForType(EventListener::Type listenerType)
- void removeEventListenersForTarget(Node* target, bool recursive = false)
- void removeCustomEventListeners(const std::string& customEventName)
- void removeAllEventListeners()

<br>

- void pauseEventListenersForTarget(Node* target, bool recursive = false)     void resumeEventListenersForTarget(Node* target, bool recursive = false)
```
Pauses/Resumes all listeners which are associated the specified target.
@param target A given target node.
@param recursive True if pause recursively, the default value is false.

暂停/恢复 事件监听
```
<br>

- void dispatchEvent(Event* event)
```
Dispatches the event.
Also removes all EventListeners marked for deletion from the
event dispatcher list.

@param event The event needs to be dispatched.

派发事件
被标记未`deletion`的事件会被移除
```
<br>

-  void dispatchCustomEvent(const std::string &eventName, void *optionalUserData = nullptr)
<br>

#### 事件管理及派发机制
##### void addEventListener(EventListener* listener)
- DispatchGuard
```cpp
// 卫兵
// 构造时对引用加一，析构减一
class DispatchGuard
{
public:
    DispatchGuard(int& count):
            _count(count)
    {
        ++_count;
    }

    ~DispatchGuard()
    {
        --_count;
    }

private:
    int& _count;
};

// 在这里，通过_inDispatch的值标注正在派发事件
void EventDispatcher::dispatchEvent(Event* event)
{
    if (!_isEnabled)
        return;
    
    updateDirtyFlagForSceneGraph();
    DispatchGuard guard(_inDispatch);

    // ......
}
```
<br>

- EventListenerVector
```cpp
//封装了一个容器，主要包含以下两个子容器
// 1. 固定优先级的监听
std::vector<EventListener*>* _fixedListeners;
// 2. 按场景图划分优先级的监听
std::vector<EventListener*>* _sceneGraphListeners;
```
<br>

- Listeners map
```cpp
std::unordered_map<EventListener::ListenerID, EventListenerVector*> _listenerMap;
```
以ListenerID（`字符串类型`）为key的事件监听容器字典<br>
<br>

-  dirty flag map
```cpp
std::unordered_map<EventListener::ListenerID, DirtyFlag> _priorityDirtyFlagMap;
```
<br>

`addEventListener()`将`listener`添加到`_listenerMap` 、`_priorityDirtyFlagMap` <br>
<br>

##### void dispatchEvent(Event* event)
```cpp 
auto pfnDispatchEventToListeners = &EventDispatcher::dispatchEventToListeners;
if (event->getType() == Event::Type::MOUSE) {
    pfnDispatchEventToListeners = &EventDispatcher::dispatchTouchEventToListeners;
}
auto iter = _listenerMap.find(listenerID);
if (iter != _listenerMap.end())
{
    // 如果在_listenerMap中找到对应id的事件
    auto listeners = iter->second;
    auto onEvent = [&event](EventListener* listener) -> bool{
        event->setCurrentTarget(listener->getAssociatedNode());
        listener->_onEvent(event);
        return event->isStopped();
    };
    // 根据事件类型，调用 dispatchEventToListeners 或 dispatchTouchEventToListeners
    (this->*pfnDispatchEventToListeners)(listeners, onEvent);
}
```
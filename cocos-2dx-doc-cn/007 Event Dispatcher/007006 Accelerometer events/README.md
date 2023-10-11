### Accelerometer events  加速器事件
[原文 Accelerometer events](https://docs.cocos2d-x.org/cocos2d-x/v4/en/event_dispatcher/accelerometer.html) 
<br>
<br>

#### 加速度计事件
一些移动设备配备了加速度计。加速度计是一种测量重力加速度以及方向变化的传感器。一个使用案例可能是需要将您的手机来回移动，也许是为了模拟一个平衡动作。Cocos2d-x 也支持这些事件，而创建它们则很简单。在使用加速度计事件之前，您需要在设备上启用它们：

```cpp
Device::setAccelerometerEnabled(true);
// 创建一个加速度计事件
auto listener = EventListenerAcceleration::create(CC_CALLBACK_2(
AccelerometerTest::onAcceleration, this));

_eventDispatcher->addEventListenerWithSceneGraphPriority(listener, this);

// 加速度计回调函数原型的实现
void AccelerometerTest::onAcceleration(Acceleration* acc, Event* event)
{
    // 处理逻辑在这里
}
```

在这里，我们启用了设备的加速度计功能，然后创建了一个加速度计事件侦听器，并指定了加速度变化时的回调函数。在回调函数中，我们可以处理加速度计事件，并使用 `acc` 参数获取加速度的信息。
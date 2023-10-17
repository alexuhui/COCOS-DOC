### Scheduler 分析

#### 概念
```
Scheduler is responsible for triggering the scheduled callbacks.
You should not use system timer for your game logic. Instead, use this class.

There are 2 different types of callbacks (selectors):

- update selector: the 'update' selector will be called every frame. You can customize the priority.
- custom selector: A custom selector will be called every frame, or with a custom interval of time

The 'custom selectors' should be avoided when possible. It is faster, and consumes less memory to use the 'update selector'.

调度器负责触发已安排的回调。你不应该在游戏逻辑中使用系统定时器，而应该使用这个类。
有两种不同类型的回调（选择器）：
1. update selector: 每帧调用。你可以自定义优先级。
2. custom selector：每帧调用，或者以自定义的时间间隔调用。
尽可能避免使用 'custom selectors'。使用 'update selector' 更快，占用的内存更少。
```
<br>

#### 重点公共方法
- void update(float dt)
```
update函数是游戏里很重要的一个函数，几乎游戏的一切都靠update来推进。
You should NEVER call this method, unless you know what you are doing.
不要自己手动调用这个update函数

注册在Schedule里的回调根据优先级保存在_updatesNegList/_updates0List/_updatesPosList 三个双向链表
这个函数会每帧刷新这些回调

```
<br>

- void scheduleUpdate(T *target, int priority, bool paused)
```
Schedules the 'update' selector for a given target with a given priority.
The 'update' selector will be called every frame.
The lower the priority, the earlier it is called.

注册target的update回调，并指定优先级
update回调每帧都会调用
优先级的值越小，越早被调用
```
<br>

- void unscheduleUpdate(void *target)
```
Unschedules the update selector for a given target
@param target The target to be unscheduled.

注销回调
```
<br>

- 
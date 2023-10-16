### Ref 分析

#### ref 类
```
Ref is used for reference count management. If a class inherits from Ref, then it is easy to be shared in different places.
Ref 用于引用计数管理。如果一个类继承自 Ref，那么它很容易在不同的地方共享。
```

#### ref 的公共方法
- void retain();
```
Retains the ownership.
This increases the Ref's reference count.

保留引用，调用这个方法会使引用计数加一
```
<br>

- void release();
```
Releases the ownership immediately.
This decrements the Ref's reference count.
If the reference count reaches 0 after the decrement, this Ref is destructed.

立即释放引用，引用计数减一，如果引用数降为0，这个引用实例会被销毁
```
<br>

- Ref* autorelease();
```
Releases the ownership sometime soon automatically.
This decrements the Ref's reference count at the end of current autorelease pool block.
If the reference count reaches 0 after the decrement, this Ref is destructed.
@returns The Ref itself.

添加到自动释放池，稍后自动释放引用。从`自动释放池`的尾部的Ref递减引用计数，如果引用数降为0，这个引用实例会被销毁
```
<br>

- unsigned int getReferenceCount() const;
```
返回引用数量
```
<br>

- 综上
1. Ref 是用于引用计数的基类
2. 封装了引用计数和销毁的方法
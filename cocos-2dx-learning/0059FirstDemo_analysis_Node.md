### Node 分析

#### 概念
Node is the base element of the Scene Graph. Elements of the Scene Graph must be Node objects or subclasses of it. <br>
The most common Node objects are: Scene, Layer, Sprite, Menu, Label. <br>
<br>

 The main features of a Node are:
 - They can contain other Node objects (`addChild`, `getChildByTag`, `removeChild`, etc)
 - They can schedule periodic callback (`schedule`, `unschedule`, etc)
 - They can execute actions (`runAction`, `stopAction`, etc)

 Subclassing a Node usually means (one/all) of:
 - overriding init to initialize resources and schedule callbacks
 - create callbacks to handle the advancement of time
 - overriding `draw` to render the node

 Properties of Node:
 - position (default: x=0, y=0)
 - scale (default: x=1, y=1)
 - rotation (in degrees, clockwise) (default: 0)
 - anchor point (default: x=0, y=0)
 - contentSize (default: width=0, height=0)
 - visible (default: true)

<br>
Node 是场景图的基本元素。场景图的元素必须是 Node 对象或其子类。<br>
最常见的 Node 对象有：Scene（场景）、Layer（层）、Sprite（精灵）、Menu（菜单）、Label（标签）。<br>
<br>

Node 的主要特征包括：
- 它们可以包含其他 Node 对象（`addChild`、`getChildByTag`、`removeChild` 等）
- 它们可以调度定期的回调（`schedule`、`unschedule` 等）
- 它们可以执行动作（`runAction`、`stopAction` 等）

扩展（继承） Node 通常意味着（其中之一或全部）：
- 重写 `init` 以初始化资源和调度回调
- 创建回调以处理时间的推移
- 重写 `draw` 以渲染节点

Node 的属性包括：
- 位置（默认：x=0，y=0）
- 缩放（默认：x=1，y=1）
- 旋转（以度为单位，顺时针）（默认：0）
- 锚点（默认：x=0，y=0）
- 内容大小（默认：width=0，height=0）
- 可见性（默认：true）

#### 重点公共方法
- static Node * create()
```
Allocates and initializes a node.
@return A initialized node which is marked as "autorelease".
创建并初始化一个节点对象
返回一个已初始化的被标记`自动回收`的节点对象
```
<br>

- virtual void draw(Renderer *renderer, const Mat4& transform, uint32_t flags)
```
Override this method to draw your own node.
The following GL states will be enabled by default:
- `glEnableClientState(GL_VERTEX_ARRAY);`
- `glEnableClientState(GL_COLOR_ARRAY);`
- `glEnableClientState(GL_TEXTURE_COORD_ARRAY);`
- `glEnable(GL_TEXTURE_2D);`
AND YOU SHOULD NOT DISABLE THEM AFTER DRAWING YOUR NODE
But if you enable any other GL state, you should disable it after drawing your node.

@param renderer A given renderer.
@param transform A transform matrix.
@param flags Renderer flag.

重写此方法以绘制你自己的节点。
默认情况下将启用以下 GL 状态：
- `glEnableClientState(GL_VERTEX_ARRAY);`
- `glEnableClientState(GL_COLOR_ARRAY);`
- `glEnableClientState(GL_TEXTURE_COORD_ARRAY);`
- `glEnable(GL_TEXTURE_2D);`
请注意，在绘制节点后，不应该禁用它们。
但是，如果你启用了任何其他的 GL 状态，你应该在绘制节点后禁用它们。

@param renderer 给定的渲染器。
@param transform 变换矩阵。
@param flags 渲染器标志。
```
<br>

-     virtual Rect getBoundingBox() const;
```
Returns an AABB (axis-aligned bounding-box) in its parent's coordinate system.
```
<br>

-     void scheduleUpdate(void);
```
Schedules the "update" method.

It will use the order number 0. This method will be called every frame.
Scheduled methods with a lower order value will be called before the ones that have a higher order value.
Only one "update" method could be scheduled per node.

注册`update`函数
```
<br>

- void unscheduleUpdate(void);
```
Unschedules the "update" method.

注销`update`函数
```
<br>

- virtual void update(float delta);
```
Update method will be called automatically every frame 
if "scheduleUpdate" is called, and the node is "live".

调用了scheduleUpdate，并且节点处于激活状态时，update每帧都会被调用
```
<br>

- virtual Action* runAction(Action* action)    void stopAction(Action* action)
```
动画
```
<br>

- Component* getComponent(const std::string& name)   virtual bool addComponent(Component *component)   virtual bool removeComponent(const std::string& name)
```
获取/添加/移除 组件
```
<br>

#### 综上
1. Node是游戏最基本的元素，场景、精灵、文本等都扩展于Node
2. Node是组件的宿主
3. Node集成了动画
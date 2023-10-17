### Scene 分析

#### 概念
```
Scene is a subclass of Node that is used only as an abstract concept.

Scene and Node are almost identical with the difference that Scene has its
anchor point (by default) at the center of the screen.

For the moment Scene has no other logic than that, but in future releases it might have
additional logic.

It is a good practice to use a Scene as the parent of all your nodes.
 
Scene will create a default camera for you.

Scene（场景）是 Node（节点）的一个子类，仅用作一个抽象概念。

Scene 和 Node 在几乎相同，区别在于 Scene 默认情况下在屏幕中心具有其锚点。

目前，Scene 除此之外没有其他逻辑，但在将来的版本中可能会添加额外的逻辑。

将 Scene 作为所有节点的父节点是一个良好的实践。

Scene 将为你创建一个默认的摄像机。
```

#### 重点方法
- static Scene *create()
```
Creates a new Scene object. 
@return An autoreleased Scene object.
```
<br>

- const std::vector<Camera*>& getCameras()
```
Get all cameras.
@return The vector of all cameras, ordered by camera depth.

返回按深度排序的摄像机列表
```
<br>

- const std::vector<BaseLight*>& getLights()
```
获取场景所有灯光
```
<br>

- virtual void render(Renderer* renderer, const Mat4& eyeTransform, const Mat4* eyeProjection = nullptr)
```
Render the scene.
@param renderer The renderer use to render the scene.
@param eyeTransform The AdditionalTransform of camera.
@param eyeProjection The projection matrix of camera.

渲染场景
```

#### 综上
1. scene 是一个特殊的节点，Scene继承自Node, 是其它当前场景上的节点的根节点
2. scene 拥有节点的属性，又有`leader`的属性，对当前游戏场景拥有整体认知：使用了多少摄像机，灯光使用情况等等
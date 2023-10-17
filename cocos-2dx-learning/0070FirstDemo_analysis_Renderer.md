### Renderer 分析

#### 概念
1. RenderQueue
```
Class that knows how to sort `RenderCommand` objects.
Since the commands that have `z == 0` are "pushed back" in
the correct order, the only `RenderCommand` objects that need to be sorted,
are the ones that have `z < 0` and `z > 0`.
```
<br>

2. Renderer
```
Class responsible for the rendering in.
Whenever possible prefer to use `TrianglesCommand` objects 
since the renderer will automatically batch them.

这个类负责渲染。
在可能的情况下，最好使用 `TrianglesCommand` 对象，
因为渲染器将自动将它们进行批处理。
```
<br>

#### 常量
```cpp
/**The max number of vertices in a vertex buffer object.*/
static const int VBO_SIZE = 65536;
/**The max number of indices in a index buffer.*/
static const int INDEX_VBO_SIZE = VBO_SIZE * 6 / 4;
/**The rendercommands which can be batched will be saved into a list, this is the reserved size of this list.*/
static const int BATCH_TRIAGCOMMAND_RESERVED_SIZE = 64;
/**Reserved for material id, which means that the command could not be batched.*/
static const int MATERIAL_ID_DO_NOT_BATCH = 0;
```
<br>

#### 重点函数
- void addCommand(RenderCommand* command)
```
Adds a `RenderComamnd` into the renderer

保存在 `_renderGroups`（RenderQueue 类型的vector容器）里
```
<br>

- void render()
```
Renders into the GLView all the queued `RenderCommand` objects 
```
<br>

- void visitRenderQueue(RenderQueue& queue)
```
根据渲染队列分组进行渲染
```
<br>

#### 总结
1. Renderer是负责渲染的类，一般情况下都不需要手动去调用
2. 默认最大顶点数65536

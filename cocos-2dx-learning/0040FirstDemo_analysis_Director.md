### Director 分析

[文档](../cocos-2dx-doc-cn/001%20Basic%20Cocos2d-x%20Concepts/001002%20Director/README.md)

#### 概念
```
Cocos2d-x uses the concept of a Director, 
just like in a movie! The Director object controls the flow of operations 
and tells the necessary recipient what to do. 
Think of yourself as the Executive Producer and you tell the Director what to do! 
One common Director task is to control Scene replacements and transitions. 
The Director is a shared singleton (effectively, there's only one instance 
of the class at a time) object that you can call from anywhere in your code.
Cocos2d-x采用了导演（Director）的概念，就像在电影中一样！导演对象控制操作的流程并告诉必要的接收者该做什么。
想象一下自己是执行制片人，你告诉导演要做什么！
一个常见的导演任务是控制场景替换和转场。
导演是一个共享的单例（有效地控制同一时间只有一个类的实例），你可以在代码的任何地方调用它。
```

#### 事件常量
声明了一系列事件号 <br>
``` cpp 
    /** Director will trigger an event before set next scene. */
    static const char* EVENT_BEFORE_SET_NEXT_SCENE;
    /** Director will trigger an event after set next scene. */
    static const char* EVENT_AFTER_SET_NEXT_SCENE;
    
    /** Director will trigger an event when projection type is changed. */
    static const char* EVENT_PROJECTION_CHANGED;
    /** Director will trigger an event before Schedule::update() is invoked. */
    static const char* EVENT_BEFORE_UPDATE;
    /** Director will trigger an event after Schedule::update() is invoked. */
    static const char* EVENT_AFTER_UPDATE;
    /** Director will trigger an event while resetting Director */
    static const char* EVENT_RESET;
    /** Director will trigger an event after Scene::render() is invoked. */
    static const char* EVENT_AFTER_VISIT;
    /** Director will trigger an event after a scene is drawn, the data is sent to GPU. */
    static const char* EVENT_AFTER_DRAW;
    /** Director will trigger an event before a scene is drawn, right after clear. */
    static const char* EVENT_BEFORE_DRAW;
```
``` cpp 
    // 设置下一个场景之前
    const char *Director::EVENT_BEFORE_SET_NEXT_SCENE = "director_before_set_next_scene";
    // 设置下一个场景之后
    const char *Director::EVENT_AFTER_SET_NEXT_SCENE = "director_after_set_next_scene";
    // 投影类型变更
    const char *Director::EVENT_PROJECTION_CHANGED = "director_projection_changed";
    // Schedule::update() 之前
    const char *Director::EVENT_BEFORE_UPDATE = "director_before_update";
    // Schedule::update() 之后
    const char *Director::EVENT_AFTER_UPDATE = "director_after_update";
    // 重置Director
    const char *Director::EVENT_RESET = "director_reset";
    // Scene::render() 之后
    const char *Director::EVENT_AFTER_VISIT = "director_after_visit";
    // 场景绘制完数据发送的GPU之后
    const char *Director::EVENT_AFTER_DRAW = "director_after_draw";
    // 场景绘制之前
    const char *Director::EVENT_BEFORE_DRAW = "director_before_draw";
```

#### 重点公共方法
- Scene* getRunningScene()
```
 Gets current running Scene. Director can only run one Scene at a time.
 获取当前场景，同一时间只会运行一个场景
```
<br>

- GLView* getOpenGLView()
```
Get the GLView.
```
<br>

-  TextureCache* getTextureCache() const
```
Gets singleton of TextureCache.
```
<br>

- Projection getProjection()
```
Gets an OpenGL projection.
```
<br>

- Node* getNotificationNode()
```
This object will be visited after the main scene is visited.
This object MUST implement the "visit" function.
Useful to hook a notification object, like Notifications (http://github.com/manucorporat/CCNotifications)
```
<br>

- void replaceScene(Scene *scene)
```
Replaces the running scene with a new one. The running scene is terminated.
ONLY call it if there is a running scene.
```

- void mainLoop()
```
重中之重的主循环方法
```

- Scheduler* getScheduler()

- ActionManager* getActionManager()

- EventDispatcher* getEventDispatcher()

- Renderer* getRenderer() const

#### 综上
Director 像是游戏世界的上帝；它是游戏的最顶层控制器，掌管场景的生杀大权，渲染，事件派发器，游戏的暂停，恢复等等一系列宏观操作
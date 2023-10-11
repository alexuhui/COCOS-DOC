### Debugging Physics Body and Shapes  物理太可怕了，我真的需要她吗？请对我说不！
[原文 Debugging Physics Body and Shapes](https://docs.cocos2d-x.org/cocos2d-x/v4/en/physics/debugging.html) 
<br>
<br>

#### Debugging Physics Body and Shapes
如果你希望在调试时在你的物理对象周围绘制红色框，只需将以下两行代码添加到你的核心代码中，放在你认为合适的地方，也许是在 AppDelegate？你可以添加以下代码：

```cpp
Director::getInstance()->getRunningScene()->getPhysics3DWorld()->setDebugDrawEnable(true);
Director::getInstance()->getRunningScene()->setPhysics3DDebugCamera(cameraObject);
```

#### 禁用物理
使用内置的物理引擎是个好主意。它是稳固且先进的。然而，如果你希望使用另一种物理引擎，也是可以的。你只需在 base/ccConfig.h 中禁用 CC_USE_PHYSICS 即可。
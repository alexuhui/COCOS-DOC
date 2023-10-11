### Creating a Sprite from SpriteFrameCache  通过SpriteFrameCache创建精灵
[原文 Creating a Sprite from SpriteFrameCache](https://docs.cocos2d-x.org/cocos2d-x/v4/en/sprites/spriteframe_cache.html) 
<br>
<br>

这通过从 SpriteFrameCache 中获取它来创建一个 Sprite。

```cpp
// 我们的 .plist 文件中有每个精灵的名称。我们将从精灵图集中获取名为 "mysprite" 的精灵：
auto mysprite = Sprite::createWithSpriteFrameName("mysprite.png");
```
![sprite](../002002%20Creating%20Sprites/i1.png)

**从 SpriteFrame 创建 Sprite**
创建相同的 Sprite 的另一种方法是通过从 SpriteFrameCache 获取 SpriteFrame，然后使用 SpriteFrame 创建 Sprite。示例：

```cpp
// 这等同于上一个示例，
// 但它是通过从缓存中检索 SpriteFrame 创建的。
auto newspriteFrame = SpriteFrameCache::getInstance()->getSpriteFrameByName("Blue_Front1.png");
auto newSprite = Sprite::createWithSpriteFrame(newspriteFrame);
```

![sprite](../002002%20Creating%20Sprites/i1.png)
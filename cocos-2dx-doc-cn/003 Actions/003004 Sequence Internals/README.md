### Sequence Internals  序列内部方法
[原文 Sequence Internals](https://docs.cocos2d-x.org/cocos2d-x/v4/en/actions/sequence_internals.html) 
<br>
<br>

#### 克隆
克隆的含义正如它听起来的那样。如果你有一个动作，你可以通过使用 `clone()` 将其应用于多个 Node 对象。为什么必须克隆呢？好问题。动作对象具有内部状态。当它们运行时，它们实际上正在更改 Node 对象的属性。如果不使用 `clone()`，则你不会真正拥有一个应用于 Node 的唯一动作。这将产生意想不到的结果，因为你不能确定动作的属性当前设置为什么。

让我们通过一个例子来理解，假设你有一个 `heroSprite`，它的位置是 (0,0)。如果你运行一个动作：

```cpp
MoveBy::create(10, Vec2(400,100));
```

这将在 10 秒内将 `heroSprite` 从 (0,0) 移动到 (400, 100)。`heroSprite` 现在有一个新的位置 (400, 100)，更重要的是动作在其内部状态中有这个位置。现在，假设你有一个 `enemySprite`，其位置为 (200, 200)。如果你尝试将相同的动作：

```cpp
MoveBy::create(10, Vec2(400,100));
```

应用于你的 `enemySprite`，它将最终位于 (800, 200)，而不是你想象的位置。看明白了吗？这是因为动作在执行 `MoveBy` 时已经有了一个内部状态。克隆动作可以防止这种情况发生。它确保你得到一个应用于 Node 的唯一版本的动作。

让我们也在代码中看到这一点，首先是错误的示例。

```cpp
// 创建我们的 Sprites
auto heroSprite = Sprite::create("herosprite.png");
auto enemySprite = Sprite::create("enemysprite.png");

// 创建一个动作
auto moveBy = MoveBy::create(10, Vec2(400,100));

// 在我们的 hero 上运行它
heroSprite->runAction(moveBy);

// 在我们的 enemy 上运行它
enemySprite->runAction(moveBy); // 糟糕，这不会是唯一的！
// 使用动作的当前内部状态作为起点。
```

正确的做法，使用 `clone()`！：

```cpp
// 创建我们的 Sprites
auto heroSprite = Sprite::create("herosprite.png");
auto enemySprite = Sprite::create("enemysprite.png");

// 创建一个动作
auto moveBy = MoveBy::create(10, Vec2(400,100));

// 在我们的 hero 上运行它
heroSprite->runAction(moveBy);

// 在我们的 enemy 上运行它
enemySprite->runAction(moveBy->clone()); // 正确！这将是唯一的
```

**Reverse**
`Reverse` 的含义也正如它听起来的那样。如果运行一系列动作，你可以调用 `reverse()` 来以相反的顺序运行它。也就是说，倒序。但是，它不仅仅是按相反的顺序运行动作。调用 `reverse()` 实际上是以相反的方式操作原始 Sequence 或 Spawn 的属性。

使用上面的 Spawn 示例，反转非常简单。

```cpp
// 反转一个序列、spawn 或动作
mySprite->runAction(mySpawn->reverse());
```

大多数 Action 和 Sequence 对象都是可逆的！

这很容易使用，但让我们确保我们知道发生了什么。假设：

```cpp
// 创建一个 Sprite
auto mySprite = Sprite::create("mysprite.png");
mySprite->setPosition(50, 56);

// 创建一些动作
auto moveBy = MoveBy::create(2.0f, Vec2(500,0));
auto scaleBy = ScaleBy::create(2.0f, 2.0f);
auto delay = DelayTime::create(2.0f);

// 创建一个序列
auto delaySequence = Sequence::create(delay, delay->clone(), delay->clone(),
delay->clone(), nullptr);

auto sequence = Sequence::create(moveBy, delay, scaleBy, delaySequence, nullptr);

// 运行它
newSprite2->runAction(sequence);

// 反转它
newSprite2->runAction(sequence->reverse());
```

实际上发生了什么呢？如果我们将步骤列成一个列表，可能会更有帮助：

1. 创建 mySprite。
2. 将 mySprite 位置设置为 (50, 56)。
3. 启动序列。
4. 序列通过 500 移动 mySprite，在 2 秒内，mySprite 的新位置为 (550, 56)。
5. 序列延迟 2 秒。
6. 序列通过 2x 缩放 mySprite，在 2 秒内。
7. 序列延迟另外 6 秒（注意我们运行了另一个序列来实现这一点）。
8. 我们对序列运行了一个 `reverse()`，因此我们以相反的顺序重新运行每个动作。
9. 序列延迟 6 秒。
10. 序列通过 -2x 缩放 mySprite，在 2 秒内。
11. 序列延迟 2 秒。
12. 序列通过 -500 移动 mySprite，在 2 秒内，mySprite 的新位置为 (50, 56)。

你可以看到，`reverse()` 对于你来说使用很简单，但在内部逻辑中并不那么简单。Cocos2d-x 承担了所有繁重的工作！

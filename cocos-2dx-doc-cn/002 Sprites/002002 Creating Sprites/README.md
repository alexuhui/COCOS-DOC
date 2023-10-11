### Creating Sprites  创建精灵
[原文 Creating Sprites](https://docs.cocos2d-x.org/cocos2d-x/v4/en/sprites/getting_started.html) 
<br>
<br>

对于创建 Sprite，有不同的方法，具体取决于你想要实现什么。你可以使用各种图形格式（包括 PNG、JPEG、TIFF 等）从图像创建 Sprite。让我们逐个讨论一下这些创建方法。<br>

**创建 Sprite**
可以通过指定要使用的图像文件来创建 Sprite。<br>

```cpp
auto mySprite = Sprite::create("mysprite.png");
```
![精灵](./i1.png)<br>

上述语句使用 mysprite.png 图像创建一个 Sprite。结果是创建的 Sprite 使用整个图像。Sprite 的尺寸与 mysprite.png 相同。如果图像文件是 200 x 200，那么创建的 Sprite 尺寸也是 200 x 200。<br>

**使用 Rect 创建 Sprite**
在前面的例子中，创建的 Sprite 的大小与原始图像文件相同。如果要创建一个只包含图像文件某一部分的 Sprite，可以通过指定 Rect 来实现。<br>

Rect 有 4 个值：原点 x、原点 y、宽度和高度。<br>

```cpp
auto mySprite = Sprite::create("mysprite.png", Rect(0, 0, 40, 40));
```
![rect](./i4.png)

Rect 从左上角开始。这与在布局屏幕位置时可能习惯的方式相反，因为它是从左下角开始的。因此，结果的 Sprite 只是图像文件的一部分。在这种情况下，Sprite 的尺寸是从左上角开始的 40 x 40。<br>

如果不指定 Rect，Cocos2d-x 将自动使用你指定的图像文件的全宽度和高度。看下面的例子。如果使用尺寸为 200 x 200 的图像，则以下两个语句将产生相同的结果。<br>

```cpp
auto mySprite = Sprite::create("mysprite.png");

auto mySprite = Sprite::create("mysprite.png", Rect(0, 0, 200, 200));
```

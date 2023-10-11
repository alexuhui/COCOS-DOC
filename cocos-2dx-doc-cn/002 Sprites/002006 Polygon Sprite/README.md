### Polygon Sprite  多边形精灵
[原文 Polygon Sprite](https://docs.cocos2d-x.org/cocos2d-x/v4/en/sprites/polygon.html) 
<br>
<br>

Polygon Sprite（多边形精灵）也是一个 Sprite，用于显示 2D 图像。然而，与普通的 Sprite 对象不同，后者是由只有 2 个三角形组成的矩形，Polygon Sprite 对象由一系列三角形组成。<br>

为什么使用 Polygon Sprite？<br>
简单，性能！<br>

我们可以在这里讨论有关像素填充率的大量技术术语，但要记住的是，Polygon Sprite 根据精灵的形状进行绘制，而不是简单的矩形，它围绕最大宽度和高度。这样可以节省大量不必要的绘制。与 Sprite 对象一样，Polygon Sprite 对象可以用于精灵表。Texture Packer 是一种工具，可以处理使用 Polygon Sprite 对象创建精灵表。

考虑这个例子：

![Polygon Sprite Example](./polygonsprite.png)

注意左右两个版本之间的差异：

左侧是通过使用 2 个三角形以矩形方式绘制的典型 Sprite。

右侧是通过许多较小的三角形以 Polygon Sprite 方式绘制的。

这种权衡对于纯粹出于性能原因是否值得取决于许多因素（精灵的形状/细节、大小、在屏幕上绘制的数量等），但总体来说，在现代 GPU 上，顶点比像素便宜。

AutoPolygon
AutoPolygon 是一个辅助类。它的目的是在运行时将图像处理成 2D 多边形网格。

该过程的每个步骤都有相应的函数，从追踪所有点到三角剖分。结果可以传递给 Sprite 对象的 create 函数以创建 Polygon Sprite。示例：

```cpp
// 自动生成多边形信息。
auto pinfo = AutoPolygon::generatePolygon("filename.png");

// 使用多边形信息创建精灵。
auto sprite = Sprite::create(pinfo);
```
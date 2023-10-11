### How to optimize the graphics performance of your Cocos2d-x games  图形优化
[原文 How to optimize the graphics performance of your Cocos2d-x games](https://docs.cocos2d-x.org/cocos2d-x/v4/en/advanced_topics/optimizing.html) 
<br>
<br>

#### 黄金法则
##### 了解瓶颈并优化瓶颈。
在进行优化时，我们应该始终遵循这个规则。系统中只有20%的代码导致了80%的性能问题。<br>

#### 始终使用工具来分析瓶颈，不要随机猜测。
现在有许多可用于分析图形性能的工具。尽管我们正在优化Android游戏的性能，但Xcode也对调试很有帮助。<br>

Xcode：https://github.com/rstrahl/rudistrahl.me/blob/master/entries/Debugging-OpenGL-ES-With-Xcode-Profile-Tools.md 和官方文档：https://developer.apple.com/library/ios/documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/ToolsOverview/ToolsOverview.html <br>

如今有三个主要的移动GPU供应商，它们提供了不错的图形性能分析工具：<br>

1. 对于ARM Mali GPU：//malideveloper.arm.com/resources/tools/mali-graphics-debugger/
2. 对于Imagination PowerVR GPU：https://community.imgtec.com/developers/powervr/tools/pvrtune/
3. 对于Qualcomm Adreno GPU：https://developer.qualcomm.com/software/adreno-gpu-profiler
在遇到图形问题时使用这些工具。但不是在一开始使用，通常瓶颈存在于CPU上。 <br>

#### 了解目标设备和游戏引擎
了解目标设备的CPU/GPU系列对于解决性能问题很重要，有时性能问题仅发生在某种设备上。你会发现它们共享相同类型的GPU（ARM或PowerVR或Mali）。<br>

了解当前使用的游戏引擎的限制也很重要。如果你知道引擎如何组织图形命令，引擎如何进行批量绘制，你可以在编码过程中避免许多常见问题。 <br>

#### “足够好”的原则。
`（“如果观众无法区分不同呈现的图像，请始终使用更便宜的实现”。）`我们知道具有RGBA444像素格式的PNG比具有RGBA888像素格式的质量更低。但如果我们无法区分两者之间的差异，我们应该坚持使用RGBA4444像素格式。RGBA444格式占用更少的内存，不太可能引起内存问题和带宽问题。<br>

对于音频采样率也是一样的原理。<br>

#### 常见瓶颈
作为经验法则，你的游戏很容易受到CPU瓶颈的影响，而不是图形瓶颈。<br>

##### CPU通常受到绘制调用的数量和游戏循环中的重型计算操作的限制
尽量减少游戏的总绘制调用。我们应该尽可能使用批处理绘制。Cocos2d-x 3.x支持自动批处理，但需要一些努力使其正常工作。<br>

在玩家玩游戏时避免IO操作。尽量预加载精灵表、音频、TTF字体等。<br>

在游戏循环中不要进行重型计算操作，即不要让重型操作每帧调用60次。<br>

绝对不要！<br>

#### GPU通常受到过度绘制（填充率）和带宽的限制。
如果你正在创建一个2D游戏并且不编写复杂的着色器，你可能不会遇到GPU问题。但是过度绘制问题仍然会带来麻烦，它会以太多的带宽消耗减慢图形性能。<br>

尽管现代移动GPU具有瓦片化延迟渲染（TBDR）架构，但只有PowerVR的HSR（隐藏表面消除）可以显著减少过度绘制问题。其他GPU供应商只实现了TBDR +早期z测试，仅在提交不透明几何体时减少过度绘制问题。而Cocos2d-x总是按照从后到前的顺序提交渲染命令。因为在2D中，我们可能有许多透明图像，只有在这个顺序下混合效果才是正确的。<br>

注意：通过使用多边形三角形，我们可以改善填充率。有关更多信息，请参阅此文章：https://www.codeandweb.com/texturepacker/tutorials/cocos2d-x-performance-optimization <br>

但不要过于担心这个问题，实际上它表现得并不太糟糕。<br>

#### 使Cocos2d-x游戏更快的简单检查表
1. 始终使用批处理绘制。将相同层次的精灵图像打包到一个大图集中（纹理打包器可以帮助）。
2. 作为经验法则，尽量保持绘制调用在50以下。换句话说，尽量减少绘制调用的数量。
3. 优先选择16位（RGBA4444 +抖动）而不是原始32位（RGBA8888）纹理。
4. 使用压缩纹理：在iOS上使用PVRTC纹理。在Android平台上使用ETC1。但ETC1没有alpha通道，你可能需要编写一个自定义着色器，并为alpha通道提供单独的ETC1图像。
5. `不要将系统字体用作游戏记分牌。它很慢。尽量使用TTF或BMFont，BMfont更好。`
6. 尽量在使用前预加载音频和其他游戏对象。
7. 使用armeabi-v7a构建Android本机代码，它将启用非常快速的NEON指令。
8. 烘焙光照而不是使用动态光照。
9. 避免使用复杂的像素着色器。
10. 避免在像素着色器中使用discard和alpha测试，这将破坏HSR（隐藏表面删除）。只有在必要时使用。
### 3D
[原文 3D](https://docs.cocos2d-x.org/cocos2d-x/v4/en/scripting/script_component.html) 
<br>
<br>

脚本组件用于扩展C++节点对象。您可以向节点添加一个脚本组件，然后该脚本组件将接收`onEnter`、`onExit`和`update`等事件。<br>

脚本组件支持JavaScript和Lua两种脚本语言。您应该根据开发语言选择适当的脚本组件类型。如果使用JavaScript开发，应使用`ComponentJS`；如果使用Lua开发，应使用`ComponentLUA`。但是，不能混用它们或在C++项目中使用它们！这是因为需要相应语言的正确绑定，而这些绑定仅在各自的项目类型中可用。<br>

Lua示例：<br>

```lua
-- 创建一个精灵并添加Lua组件
local player = Sprite:create("player.png")

local luaComponent = ComponentLua:create("player.lua")
player:addComponent(luaComponent)
```

player.lua:

```lua
local player = {
    onEnter = function(self)
        -- 在onEnter中执行一些操作
    end,

    onExit = function(self)
        -- 在onExit中执行一些操作
    end,

    update = function(self)
        -- 每帧执行一些操作
    end
}

-- 必须返回player以供C++节点知晓
return player
```

JavaScript示例：

```javascript
// 创建一个精灵并添加JavaScript组件
var player = Sprite.create("player.png");

var jsComponent = ComponentJS.create("player.js");
player.addComponent(jsComponent);

// player.js
Player = cc.ComponentJS.extend({
    generateProjectile: function (x, y) {
        // 在这里生成子弹
    },

    onEnter: function() {
        // 在这里处理进入场景时的逻辑
    }
});
```

请注意JavaScript和Lua组件之间的一个区别是，在Lua组件中应该返回对象，在JavaScript中只需扩展`cc.ComponentJS`。<br>

有关更详细的用法，请参考测试项目：`tests/lua-tests/src/ComponentTest` 和 `tests/js-tests/src/ComponentTest`。<br>

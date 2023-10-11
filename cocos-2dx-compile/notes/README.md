### 编译记录

#### 子模块
- 把仓库拉下来发现子模块更新不了
- 处理方法：
.gitmodules 里 `git:` 改成 `https:` <br>
- 缺少poly2tri库，添加子模块 :
``` bash
git submodule add https://github.com/greenm01/poly2tri
```
- .gitmodules 会增加这一段
```
[submodule "poly2tri"]
	path = poly2tri
	url = https://github.com/greenm01/poly2tri.git
```
### Upgrade Spine  升级spine
[原文 Upgrade Spine](https://docs.cocos2d-x.org/cocos2d-x/v4/en/advanced_topics/sqlite.html) 
<br>
<br>


#### 升级Spine
##### 步骤
1. 克隆spine-runtimes的源代码

```bash
git clone https://github.com/EsotericSoftware/spine-runtimes.git
cd spine-runtimes
git checkout 3.8
```

2. 删除cocos2d-x中的spine源代码

```bash
rm -rf cocos2d-x/cocos/editor-support/spine/*
```

3. 更新到最新的spine代码

```bash
cp spine-runtimes/spine-cpp/spine-cpp/include/spine/* \
    cocos2d-x/cocos/editor-support/spine/
cp spine-runtimes/spine-cpp/spine-cpp/src/spine/* \
    cocos2d-x/cocos/editor-support/spine/
cp -r spine-runtimes/spine-cocos2dx/src/spine/* \
    cocos2d-x/cocos/editor-support/spine/
```

4. 编辑cocos2d-x/cocos/editor-support/spine/CMakeLists.txt

```cmake
file(GLOB_RECURSE COCOS_SPINE_SRC
    ${CMAKE_CURRENT_LIST_DIR}/*.cpp
    ${CMAKE_CURRENT_LIST_DIR}/**/*.cpp
)

file(GLOB_RECURSE COCOS_SPINE_HEADER
    ${CMAKE_CURRENT_LIST_DIR}/*.h
    ${CMAKE_CURRENT_LIST_DIR}/**/*.h
)
```
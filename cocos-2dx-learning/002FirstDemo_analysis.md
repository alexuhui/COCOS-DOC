### demo工程分析

#### 工程目录结构
    .
    ├── ...
    ├── FirstDemo                        # 工程根目录
    │   ├── Classes                          # c++代码目录，初始放了一个helloword场景类，一个委托类
    |   |   ├── AppDelegate.cpp                  # 应用委托，一些系统回调（启动，进入后台/前台），做了启动后的游戏初始化工作
    |   |   ├── AppDelegate.h                    # 头文件
    |   |   ├── HelloWorldScene.cpp              # 初始化了一个默认场景 
    |   |   └── HelloWorldScene.h                # 头文件
    │   ├── cmake-build                      # cmake构建的目录，忽略
    │   ├── cocos2d                          # cocos2d引擎库，粗略来看，就是创建项目时从cocos2d-x复制过来的
    |   |   ├── build                            # 应该和构建相关
    |   |   ├── cmake                            # 可能和cmake工具相关
    |   |   ├── cocos                            # 引擎核心源码
    |   |   ├── docs                             # 说明文档
    |   |   ├── extensions                       # 扩展库
    |   |   ├── external                         # 第三方库
    |   |   ├── licenses                         # 许可
    |   |   ├── tools                            # 一些工具
    |   |   └── ...                              # 一些依赖下载脚本、cmake脚本之类的东西
    │   ├── proj.android                     # 可能是用于构建安卓工程的
    │   ├── proj.ios_mac                     # 可能是用于构建ios/mac工程的
    │   ├── proj.linux                       # 可能是用于构建linux工程的
    │   ├── proj.win32                       # 可能是用于构建windows工程的
    │   ├── Resources                        # 资源文件，字体、图片之类的
    |   |   ├── fonts                            # 字体
    |   |   ├── res                              # 资源路径
    |   |   |   └── .gitkeep                     # 新建工程会发现这个神奇文件。因为git不会推空文件夹，只是为了让git不要忽略这个文件夹。说明不可或缺~
    |   |   ├── CloseNormal.png                  # 打开图片，这就是demo的关闭按钮。从HelloWorldScene.cpp读取图片的参数来看，Resources是检索资源的根目录。
    |   |   ├── CloseNormal.png                  # demo的关闭按钮按下状态时显示的图片
    |   |   └── HelloWorld.png                   # cocos的logo，显示在demo中间
    │   ├── .cocos-project.json              # cocos 工程配置
    │   └── CMakeLists.txt                   # cmake构建脚本
    └── ...

引擎库cocos2d-x目录和工程内cocos2d目录对比：<br>
![cocos](./img/002/dir_cocos2d.png) <br>
<br>

- 从目录结构来看，主要需要关注的是`Classes`、`cocos2d`、`Resources`这几个目录
1. `Classes`放源代码，实现业务逻辑
2. `cocos2d`引擎库，游戏底层框架
3. `Resources`资源目录，存放图片模型等
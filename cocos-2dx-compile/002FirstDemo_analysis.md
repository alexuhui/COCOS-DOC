### demo工程分析

#### 工程目录结构
    .
    ├── ...
    ├── FirstDemo                        # 工程根目录
    │   ├── Classes                      # 放了一个helloword场景类，一个委托类
    │   ├── cmake-build                  # cmake构建的目录不用管
    │   ├── cocos2d                      # cocos2d引擎库
    │   ├── proj.android                 # 可能是用于构建安卓工程的
    │   ├── proj.ios_mac                 # 可能是用于构建ios/mac工程的
    │   ├── proj.linux                   # 可能是用于构建linux工程的
    │   ├── proj.win32                   # 可能是用于构建windows工程的
    │   ├── Resources                    # 资源文件，字体、图片之类的
    │   ├── .cocos-project.json          # cocos 工程配置
    │   └── CMakeLists.txt               # cmake构建脚本
    └── ...
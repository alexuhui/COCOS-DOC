### File System Access  文件系统访问
[原文 File System Access](https://docs.cocos2d-x.org/cocos2d-x/v4/en/advanced_topics/filesystem.html) 
<br>
<br>


#### 文件系统访问
尽管你可以使用stdio.h中的函数来访问文件，但有几个原因会让这变得不太方便：

1. 你需要调用特定于系统的API来获取文件的完整路径。
2. 资源在安装后会被打包到Android的.apk文件中。
3. 你希望根据分辨率自动加载资源（如图片）。

为了解决这些问题，FileUtils类已被创建出来。FileUtils是一个辅助类，用于访问位于资源目录下的文件。这包括从文件读取数据和检查文件是否存在。<br>

#### 读取文件内容的函数
这些函数将读取不同类型的文件并返回不同的数据类型：

- `getStringFromFile`：返回类型 `std::string`，支持相对路径和绝对路径
- `getDataFromFile`：返回类型 `cocos2d::Data`，支持相对路径和绝对路径
- `getFileDataFromZip`：返回类型 `unsigned char*`，绝对路径
- `getValueMapFromFile`：返回类型 `cocos2d::ValueMap`，支持相对路径和绝对路径
- `getValueVectorFromFile`：返回类型 `cocos2d::ValueVector`，绝对路径

#### 管理文件或目录的函数
这些函数将管理文件或目录：

- `isFileExist`：支持相对路径和绝对路径
- `isDirectoryExist`：支持相对路径和绝对路径
- `createDirectory`：绝对路径
- `removeDirectory`：绝对路径
- `removeFile`：绝对路径
- `renameFile`：绝对路径
- `getFileSize`：支持相对路径和绝对路径
```
### SQLite  数据库
[原文 SQLite](https://docs.cocos2d-x.org/cocos2d-x/v4/en/advanced_topics/sqlite.html) 
<br>
<br>


SQLite是一个自包含的SQL数据库引擎。这意味着没有涉及到服务器。SQLite在游戏运行时运行，您编写代码连接到数据库并操作其内容。这绝不是一份详尽无遗的指南，实际上，我们只涵盖了SQLite为您提供的1%功能。请阅读他们的网站以获取有关SQLIte为开发人员提供的更多详细信息。<br>

#### 入门。
为了使用SQLite，您必须下载并将其添加到您的项目中。请查看SQLite下载页面以获取更多详细信息。出于我们的目的，您只需要在项目中添加sqlite.h和sqlite.c这两个文件。将这些文件添加到您的环境中，并确保它们是构建过程的一部分。

#### SQL在游戏中是如何工作的？
现在您有了SQLite，您必须了解如何在应用程序中使用数据库。除非您编写代码，否则没有自动受益。没有向导，也没有免费的功能。这由您手工编写，以满足您的具体需求。总的来说，您将需要评估以下事项：

- 您的数据库是否已存在？

- - 是的？连接到它。
- - 不是？创建它，可能使用create table查询。然后连接到它。

<br>

- 您是否连接到数据库？

- - 是的？发出查询以实现您的目标。
- - 不是？连接到它，然后发出查询以实现您的目标。

<br>

- 您是否需要根据玩家的成就更新数据库？

- - 是的？运行插入/更新查询以更改数据库。
- - 不是？可能仅使用选择查询就足以使用数据库驱动游戏玩法。

<br>

- 玩家是否完成了您的游戏？

- - 是的？确保在游戏退出时关闭数据库。未能这样做可能会损坏您的数据库并使其无法使用。


#### 基本数据库创建和操作
让我们来看看如何创建一个简单的数据库，连接到它，然后操作它。

##### 创建一个简单的数据库
为了使用您的数据库，它必须存在。SQLite是基于文件的。简单地创建一个新文件来存储您的数据库就足够了。请注意，我们使用.db文件扩展名来帮助标明这确实是我们的数据库。了解数据库位于玩家设备的何处是很重要的。当您创建数据库时，必须将其放在设备允许玩家写入数据的位置。Cocos2d-x通过一个称为getWriteablePath()的文件系统API使这变得很容易。这是一个示例：

```cpp
sqlite3* pdb;

pdb = NULL;

std::string dbPath = cocos2d::FileUtils::getInstance()->getWritablePath() + "mydatabase.db";

int result = sqlite3_open(dbPath.c_str(), &pdb);

if(result == SQLITE_OK)
  std::cout << "open database successful!" << std::endl;
else
  std::cout << "open database failed!" << std::endl;
```

有了打开的数据库，现在您可以使用它了。

##### 创建表
数据库使用表来存储数据。您的数据库中至少需要一个表。一个注意是，为了创建表，您必须知道您的表将包含什么数据。如果以后需要修改表的结构，您始终可以使用SQL alter table命令。然而，这超出了本文的范围。创建一个简单的表：

```cpp
int result = 0;
std::string sql;

sql = "create table " +
std::string("Master") +
std::string(" (id TEXT PRIMARY KEY, value INT);");

result = sqlite3_exec(pdb, sql.c_str(), NULL, NULL, NULL);

if(result == SQLITE_OK)
{
  // 表成功创建
}
else
{
  // 表未成功创建
}
```

##### 查询数据
当您想要从数据库中获取信息时，必须执行select查询以获取它。select查询是一个只读查询。在运行这些类型的查询时，您不必担心意外修改游戏数据。一个示例select查询：

```cpp
std::string key = "Brown";

std::string sql = "SELECT NAME " +
std::string(" FROM ") +
std::string("Master") +
std::string(" WHERE id='") +
std::string(key.c_str()) +
std::string("' LIMIT 1;");

sqlite3_stmt* statement;

if (sqlite3_prepare_v2(&pdb, sql.c_str(), -1, &statement, 0) == SQLITE_OK)
{
  int result = 0;

  while(true)
  {
      result = sqlite3_step(statement);

      if(result == SQLITE_ROW)
      {
          // 处理行数据。
      }
      else
     

 {
          break;
      }
  }
}
```

##### 插入数据
您可能需要将数据插入到数据库中以便以后使用。使用插入查询来执行此操作。示例：

```cpp
std::string sql = "INSERT INTO Master (id, value) VALUES ('Brown', 42);";
int result = sqlite3_exec(pdb, sql.c_str(), NULL, NULL, NULL);
```

##### 更新数据
```cpp
std::string sql = "UPDATE Master SET value = 43 WHERE id = 'Brown';";
int result = sqlite3_exec(pdb, sql.c_str(), NULL, NULL, NULL);
```

##### 关闭数据库
```cpp
sqlite3_close(pdb);
```
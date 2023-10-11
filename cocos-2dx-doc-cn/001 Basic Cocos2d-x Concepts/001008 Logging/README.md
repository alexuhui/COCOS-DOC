### Logging as a way to output messages  日志输出
[原文 Logging as a way to output messages](https://docs.cocos2d-x.org/cocos2d-x/v4/en/basic_concepts/logging.html) 
<br>
<br>

有时，当你的应用程序正在运行时，你可能希望看到用于信息或调试目的的消息被写入控制台。这已经内置在引擎中，使用 log()。例如：

```cpp
// 一个简单的字符串
log("This would be outputted to the console");

// 一个字符串和一个变量
std::string s = "My variable";
log("string is %s", s.c_str());

// 一个 double 和一个变量
double dd = 42;
log("double is %f", dd);

// 一个整数和一个变量
int i = 6;
log("integer is %d", i);

// 一个浮点数和一个变量
float f = 2.0f;
log("float is %f", f);

// 一个布尔值和一个变量
bool b = true;
if (b == true)
    log("bool is true");
else
    log("bool is false");
```

对于 C++ 用户，如果你愿意，你可以使用 std::cout 代替 log()，不过 log() 可能提供对复杂输出的更简单的格式化。
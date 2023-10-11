### Networking with HTTP  HTTP网络
[原文 Networking with HTTP](https://docs.cocos2d-x.org/cocos2d-x/v4/en/advanced_topics/networking.html) 
<br>
<br>


#### 使用HTTP进行网络通信
有时从另一个来源获取资源或数据可能会很有帮助。一种常见的方法是使用HTTP请求。<br>

HTTP网络通信有三个步骤：<br>

1. 创建一个HttpRequest
2. 为响应请求创建一个setResponseCallback()回调函数。
3. 通过HttpClient发送HttpRequest

HttpRequest可以有四种类型：POST、PUT、DELETE、UNKNOWN。除非指定，默认类型是UNKNOWN。HTTPClient对象控制发送请求和在回调中接收数据。<br>

使用HttpRequest非常简单：<br>

```cpp
HttpRequest* request = new (std::nothrow) HttpRequest();
request->setUrl("//just-make-this-request-failed.com");
request->setRequestType(HttpRequest::Type::GET);
request->setResponseCallback(CC_CALLBACK_2(HttpClientTest::onHttpRequestCompleted, this));

HttpClient::getInstance()->sendImmediate(request);

request->release();
```

请注意，我们为接收响应时指定了setResponseCallback()方法。通过这样做，我们可以查看返回的数据并按需要使用它。同样，这个过程很简单，我们可以轻松完成：

```cpp
void HttpClientTest::onHttpRequestCompleted(HttpClient* sender, HttpResponse* response)
{
  if (!response)
  {
    return;
  }

  // 输出数据
  std::vector<char>* buffer = response->getResponseData();

  for (unsigned int i = 0; i < buffer->size(); i++)
  {
    log("%c", (*buffer)[i]);
  }
}
```
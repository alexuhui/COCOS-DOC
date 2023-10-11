### What is the EventDispatch mechanism？  什么是时间分发机制
[原文 What is the EventDispatch mechanism](https://docs.cocos2d-x.org/cocos2d-x/v4/en/event_dispatcher/getting_started.html) 
<br>
<br>

事件分发（EventDispatch）是一种响应用户事件的机制。<br>

基本原理：<br>

1. 事件监听器（Event listeners）封装了你的事件处理代码。
2. 事件分发器（Event dispatcher）通知监听器有关用户事件的信息。
3. 事件对象包含有关事件的信息。
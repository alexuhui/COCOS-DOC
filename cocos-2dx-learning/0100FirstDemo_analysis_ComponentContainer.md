### ComponentContainer 分析

#### 概念
1. Component
组件，组件可以理解成对Node的扩展。基于组件的开发模式，可以方便实现`插拔式`开发。比如，<br>
有个Node，有个Move组件（继承自Component的类）<br>
需要Move的时候就挂上（或者激活），不需要Move的时候移除（或者禁用）`Move`组件即可<br>
有利于解耦Node上的各种行为<br>
<br>

2. ComponentContainer
组件容器，管理Node上的组件
<br>

#### 数据
```cpp
std::unordered_map<std::string, Component*> _componentMap
```
每个`Node`有一个`ComponentContainer`实例，Node上的组件存储在`_componentMap`字典里
<br>

#### 重点方法
- Component* get(const std::string& name) const
```cpp
    Component* ret = nullptr;

    auto it = _componentMap.find(name);
    if (it != _componentMap.end())
    {
        ret = it->second;
    }

    return ret;
```
通过名字查询组件<br>
<br>

- bool add(Component *com)
```cpp
bool ComponentContainer::add(Component *com)
{
    bool ret = false;
    CCASSERT(com != nullptr, "Component must be non-nil");
    CCASSERT(com->getOwner() == nullptr, "Component already added. It can't be added again");
    do
    {
        auto componentName = com->getName();

        if (_componentMap.find(componentName) != _componentMap.end())
        {
            CCASSERT(false, "ComponentContainer already have this kind of component");
            break;
        }
        _componentMap[componentName] = com;
        com->retain();
        com->setOwner(_owner);
        com->onAdd();

        ret = true;
    } while(0);
    return ret;
}
```
添加组件<br>
从源代码来看，cocos2dx不支持多次绑定同一个组件<br>
<br>

- bool remove(const std::string& name)
移除组件<br>
<br>

- bool remove(Component *com)
移除组件<br>
<br>

- void removeAll()
```cpp
void ComponentContainer::removeAll()
{
    if (!_componentMap.empty())
    {
        for (auto& iter : _componentMap)
        {
            iter.second->onRemove();
            iter.second->setOwner(nullptr);
            iter.second->release();
        }
        
        _componentMap.clear();
        _owner->unscheduleUpdate();
    }
}
```
移除所有组件<br>
注销update<br>
<br>

- void visit(float delta)
执行所有组件的`update`函数
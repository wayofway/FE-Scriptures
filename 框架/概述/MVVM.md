## MVVM

https://segmentfault.com/a/1190000015895017

https://segmentfault.com/a/1190000015581922

Model-ViewModel-View-Controller

采用双向绑定（data-binding）：View的变动，自动反映在 ViewModel，

与MVC框架的主要区别有两点：
**1、实现数据与视图的分离**
**2、通过数据来驱动视图，开发者只需要关心数据变化，DOM操作被封装了。**

![hEQAEJACAgBISAEhIAQEAJCQAgIASHgigT+Dy+Ux4EFPXIkAAAAAElFTkSuQmCC](D:\LEARN\learning_notes\框架、设计模式\images\mvvm1.png)

## MVVM的实现原理：

MVVM的实现主要是三个核心点：

1. **响应式：vue如何监听data的属性变化**
2. **模板解析：vue的模板是如何被解析的**
3. **渲染：vue模板是如何被渲染成HTML的**


# Messaging {#pageTitle}

本章介绍如何把消息表达式转换成`objc_msgSend`调用，如何通过名字引用函数。还介绍了如何利用`objc_msgSend`，如何规避动态绑定

## The objc\_msgSend Function

消息传递的关键依赖于编译器为每个类或者对象创建的结构。每一个类结构包含两个关键的元素：

* 指向superclass的指针
* 类的dispatch table




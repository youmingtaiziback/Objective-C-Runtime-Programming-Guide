# Interacting with the Runtime {#pageTitle}

Objective-C程序与运行时系统在三个层面上有交互：Objective-C代码、NSObject类定义的方法、直接调用runtime函数

## Objective-C Source Code

编译Objective-C代码时，编译器生成数据结构和函数调用来支持语言的动态特性。数据结构里面包含了类和分类的定义、协议的声明。运行时的主要任务就是发消息

## NSObject Methods

有些NSObject直接向runtime查询信息

* `isKindOfClass:`

* `isMemberOfClass:`

* `respondsToSelector:`

* `conformsToProtocol:`

* `methodForSelector:`




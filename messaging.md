# Messaging {#pageTitle}

本章介绍如何把消息表达式转换成`objc_msgSend`调用，如何通过名字引用函数。还介绍了如何利用`objc_msgSend`，如何规避动态绑定

## The objc\_msgSend Function

消息传递的关键依赖于编译器为每个类或者对象创建的结构。每一个类结构包含两个关键的元素：

* 指向superclass的指针
* 类的dispatch table

新对象生成时，内存被分配，成员变量被初始化。isa指针先于其他成员变量被初始化

向一个对象发送消失时，消息函数会沿着isa寻找相应的对象。这就是动态消息绑定

为了加速消息处理，运行时系统缓存使用过的selector和函数地址。每个类有一个单独的cache，用来保存自己定义的或者继承的方法

## Using Hidden Arguments

objc\_msgSend找到函数实现时，会把所有的参数传递给函数实现，并额外传递两个参数：self、\_cmd

这两个参数是在编译期间被加入的

## Getting a Method Address

规避动态绑定的唯一方法就是获取方法地址直接调用。一个方法被调用多次时可以采取直接调用的方式减少时间

```
void (*setter)(id, SEL, BOOL);
int i;

setter = (void (*)(id, SEL, BOOL))[target
    methodForSelector:@selector(setFilled:)];
for ( i = 0 ; i < 1000 ; i++ )
    setter(targetList[i], @selector(setFilled:), YES);
```

前两个参数是self和\_cmd


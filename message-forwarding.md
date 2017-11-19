# Message Forwarding {#pageTitle}

给一个对象发送处理不了的消息会发生错误，但在此之前，运行时系统给了对象处理消息的机会

## Forwarding

向一个对象发送了处理不了的消息时，在发生错误之前，运行时会向对象发送forwardInvocation:消息并附带唯一的参数NSInvocation对象，该对象封装了原始的方法和参数

可以实现`forwardInvocation:`给消息一个默认的回应，或者以其他方式避免错误。一般用`forwardInvocation:`将消息传递给其他对象

任何对象都从NSObject继承了`forwardInvocation:`方法。NSObject默认的实现只是调用了`doesNotRecognizeSelector:`

为了实现`forwardInvocation:`

* 确定消息发往何处
* 发消息并携带原始的参数

```
- (void)forwardInvocation:(NSInvocation *)anInvocation {
    if ([someOtherObject respondsToSelector:[anInvocation selector]])
        [anInvocation invokeWithTarget:someOtherObject];
    else
        [super forwardInvocation:anInvocation];
}
```

被转发的消息的返回值返回给原始的调用者

## Forwarding and Multiple Inheritance

消息转发提供了大多数多重继承的特性。区别是：多重继承把不同的功能集合到一个对象。会是对象变大、变得多接口。消息转发把不同的功能指派给不同的对象。把问题分解给小的对象，这个过程对消息发送者是透明的

## Surrogate Objects

消息转发不仅模拟了多重继承，也使得开发轻量级对象来代表或者覆盖大量对象。代理对象代表消息被传递的对象

_The Objective-C Programming Language_的“Remote Messaging”一张提到的proxy就是这样一种surrogate。


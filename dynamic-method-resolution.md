# Dynamic Method Resolution {#pageTitle}

本章介绍如何动态提供方法的实现

## Dynamic Method Resolution

有时需要动态的提供方法的实现，比如动态属性的@dynamic指令

通过`resolveInstanceMethod:`和`resolveClassMethod:`可以分别为实例和类添加方法

可以通过`class_addMethod`添加方法

```
void dynamicMethodIMP(id self, SEL _cmd) {
    // implementation ....
}

@implementation MyClass
+ (BOOL)resolveInstanceMethod:(SEL)aSEL {
    if (aSEL == @selector(resolveThisMethodDynamically)) {
          class_addMethod([self class], aSEL, (IMP) dynamicMethodIMP, "v@:");
          return YES;
    }
    return [super resolveInstanceMethod:aSEL];
}
@end
```

消息传递机制之前，类有机会提供动态方法解析。如果`respondsToSelector:`或者`instancesRespondToSelector:`被触发，动态方法解析就有机会为一个selector提供IMP。如果实现了`resolveInstanceMethod:`，但是想让特定的方法走消息传递流程，可以针对这些selector返回NO

## Dynamic Loading

Objective-C程序可以在运行时加载类和分类，这些类和分类被和一开始加载的同等对待

实现动态加载的方法

* `objc_loadModules`
* NSBundle提供的更便捷的动态加载的接口




# Dynamic Method Resolution {#pageTitle}

本章介绍如何动态提供方法的实现

## Dynamic Method Resolution

有时需要动态的提供方法的实现，比如动态属性的@dynamic指令

通过resolveInstanceMethod:和resolveClassMethod:可以分别为实例和类添加方法

可以通过class\_addMethod添加方法

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

消息传递机制之前，类有机会提供动态方法解析。如果respondsToSelector:或者instancesRespondToSelector:被触发，动态方法解析就有机会为一个selector提供IMP。如果实现了resolveInstanceMethod:，但是想让特定的方法走消息传递流程，可以针对这些selector返回NO


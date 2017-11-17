# Dynamic Method Resolution {#pageTitle}

本章介绍如何动态提供方法的实现

## Dynamic Method Resolution

有时需要动态的提供方法的实现，比如动态属性的@dynamic指令

通过resolveInstanceMethod:和resolveClassMethod:可以分别为实例和类添加方法


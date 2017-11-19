# Declared Properties {#pageTitle}

编译器遇到属性声明时，会生成与类、分类、协议相关联的描述性元数据。你可以通过函数访问这些元数据，该函数支持在类、协议中按名字查找属性，把属性的attributes拷贝到C字符串数组。每一个类和协议都声明了属性列表

## Property Type and Functions

属性的结构

```
typedef struct objc_property *Property;
```

获取属性列表

```
objc_property_t *class_copyPropertyList(Class cls, unsigned int *outCount)
objc_property_t *protocol_copyPropertyList(Protocol *proto, unsigned int *outCount)
```

获取属性

```
objc_property_t class_getProperty(Class cls, const char *name)
objc_property_t protocol_getProperty(Protocol *proto, const char *name, BOOL isRequiredProperty, BOOL isInstanceProperty)
```

获取属性的attributes

```
const char *property_getAttributes(objc_property_t property)
```

访问一个类的所有属性相关信息的代码就是

```
id LenderClass = objc_getClass("Lender");
unsigned int outCount, i;
objc_property_t *properties = class_copyPropertyList(LenderClass, &outCount);
for (i = 0; i < outCount; i++) {
    objc_property_t property = properties[i];
    fprintf(stdout, "%s %s\n", property_getName(property), property_getAttributes(property));
}
```

## Property Type String

## Property Attribute Description Examples






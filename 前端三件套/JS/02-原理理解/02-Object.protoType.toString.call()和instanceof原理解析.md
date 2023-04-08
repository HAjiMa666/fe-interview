# Object.protoType.toString.call()和instanceof原理解析

> 这两个方法都是用于判断引用类型的具体类型的，但是它们二者的原理却是不一样，我们分析一下

## instanceof

- instanceof是通过判断该对象的原型上是否有这个类型，其原理是原型链。
- `obj1 instanceof Array`

## Object.protoType.toString.call()

- 在早期的ECMA规范中，Object.protoType中有一个内置属性`[[class]]`，这个属性是用于判断具体对象类型的。如此调用，返回一个`[object type]`，这个type是对象的具体类型。
- 在近期最新的ECMA规范中，用这个方法来判断对象具体类型已经不靠谱了，因为`[[class]]`已经被遗弃，取而代之的是`[Symbol.toStringTag]`，该值被用于自定义对象定义默认的toString()方法返回的字符串标签。
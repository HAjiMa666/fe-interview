# instanceof原理是什么

## 基础概念
1. 用于检测构造函数的prototype属性是否出现在某个实例对象的原型链上的
2. 详细来讲，instanceof运算符是通过检查object的原型链上是否包含constructor的原型对象。如果object的原型链中存在constructor的原型对象，那么object就是constructor的一个实例，返回值为true，如果object的原型链中不存在constructor的原型对象，那么object就不是constructor的实例，返回为false。

## 缺点
- 由于instanceof是基于原型链的检查，因此如果某个对象的原型链比较深，那么检查的效率会比较低

## 原理实现

```js
  function myInstanceof(obj, constructor) {
    let proto = Object.getPrototypeOf(obj);
    while (proto) {
      if (proto === constructor.prototype) {
        return true;
      }
      proto = Object.getPrototypeOf(proto);
    }
    return false;
  }
```
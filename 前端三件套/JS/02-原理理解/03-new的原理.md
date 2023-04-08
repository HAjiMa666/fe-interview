# 你知道new创建出来的对象经历了什么操作嘛？

1. 创建一个空对象，将空对象的`[[prototype]]`指向构造函数的原型。
2. 将构造函数内的this指向这个空对象。
3. 执行构造函数内部代码，为这个对象添加属性
4. 判断其构造函数返回值是否为引用类型，若为引用类型，则返回这个新对象，若不是，则返回其新对象。

## 输出代码
```js
const Foo = function () {
  return {
    a: "czx",
  };
};

const Bar = function () {
  return 123;
};

const a = new Foo(); // {a:'czx'}
const b = new Bar(); // Bar{}
```

## 原理实现
```js
const newImplements = (constructor, args) => {
  let newObj = null;
  let result = null;
  if (typeof constructor !== "function") {
    throw "constructor must be a function";
  }
//创建了一个新对象, 并且新对象的[[prototype]]指向了构造函数的原型
  newObj = Object.create(constructor.prototype);
  //执行构造函数内部代码,为新对象添加属性
  result = constructor.apply(newObj, args);
  //判断result是否是引用类型.
  if (typeof result === "object" || typeof result === "function") return result;
  else return newObj;
};

const Foo = function () {
  return 123;
};

const Bar = function () {
  return {
    name: "czx",
  };
};

console.log(newImplements(Foo));
console.log(new Bar());
```
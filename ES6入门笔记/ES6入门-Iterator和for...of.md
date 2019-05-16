- Iterator遍历器

  遍历器（Iterator）就是这样一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。

- Iterator 的作用有三个：一是为各种数据结构，提供一个统一的、简便的访问接口；二是使得数据结构的成员能够按某种次序排列；三是 ES6 创造了一种新的遍历命令`for...of`循环，Iterator 接口主要供`for...of`消费。

- Iterator 的遍历过程是这样的。

  （1）创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。

  （2）第一次调用指针对象的`next`方法，可以将指针指向数据结构的第一个成员。

  （3）第二次调用指针对象的`next`方法，指针就指向数据结构的第二个成员。

  （4）不断调用指针对象的`next`方法，直到它指向数据结构的结束位置。

  每一次调用`next`方法，都会返回数据结构的当前成员的信息。具体来说，就是返回一个包含`value`和`done`两个属性的对象。其中，`value`属性是当前成员的值，`done`属性是一个布尔值，表示遍历是否结束。

- ES6 规定，默认的 Iterator 接口部署在数据结构的`Symbol.iterator`属性，或者说，一个数据结构只要具有`Symbol.iterator`属性，就可以认为是“可遍历的”（iterable）。

- 原生具备 Iterator 接口的数据结构如下。

  - Array
  - Map
  - Set
  - String
  - TypedArray
  - 函数的 arguments 对象
  - NodeList 对象

  ```
  let arr = ['a', 'b', 'c'];
  let iter = arr[Symbol.iterator]();
  
  iter.next() // { value: 'a', done: false }
  iter.next() // { value: 'b', done: false }
  iter.next() // { value: 'c', done: false }
  iter.next() // { value: undefined, done: true }
  ```

- 调用Iterator接口的场合

  - 解构赋值
  - 扩展运算符
  - yield*后面跟的是一个可遍历的结构
  - 最简单的实现，generator函数

- return()提前for..of退出。throw()配合generator函数使用

- `for...of`循环可以代替数组实例的`forEach`方法。

  ```
  const arr = ['red', 'green', 'blue'];
  
  for(let v of arr) {
    console.log(v); // red green blue
  }
  ```

  ```
  const arr = ['red', 'green', 'blue'];
  
  arr.forEach(function (element, index) {
    console.log(element); // red green blue
    console.log(index);   // 0 1 2
  });
  ```

  JavaScript 原有的`for...in`循环，只能获得对象的键名，不能直接获取键值。ES6 提供`for...of`循环，允许遍历获得键值。

- set和map也具有接口

- 数据结构

  - `entries()` 返回一个遍历器对象，用来遍历`[键名, 键值]`组成的数组。对于数组，键名就是索引值；对于 Set，键名与键值相同。Map 结构的 Iterator 接口，默认就是调用`entries`方法。
  - `keys()` 返回一个遍历器对象，用来遍历所有的键名。
  - `values()` 返回一个遍历器对象，用来遍历所有的键值。

  ```
  let arr = ['a', 'b', 'c'];
  for (let pair of arr.entries()) {
    console.log(pair);
  }
  // [0, 'a']
  // [1, 'b']
  // [2, 'c']
  ```

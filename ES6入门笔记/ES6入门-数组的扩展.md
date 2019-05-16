- 拓展运算符(...)。好比rest参数的逆运算，将一个数组转为用都好分隔的参数序列。

  ```
  console.log(1, ...[2, 3, 4], 5)
  // 1 2 3 4 5
  ```

- 由于扩展运算符可以展开数组，所以不再需要`apply`方法，将数组转为函数的参数了。

  ```
  // ES5 的写法
  function f(x, y, z) {
    // ...
  }
  var args = [0, 1, 2];
  f.apply(null, args);
  
  // ES6的写法
  function f(x, y, z) {
    // ...
  }
  let args = [0, 1, 2];
  f(...args);
  ```

- 拓展运算符应用

  直接复制的话，是复制了指向底层数据结构的指针，而不是克隆一个全新的数组

  ```
  const a1 = [1, 2];
  const a2 = a1;
  
  a2[0] = 2;
  a1 // [2, 2]
  ```

  ES5通过变通方法复制数组，例如data.concat()返回原数组的克隆，这样修改a2就不会对a1产生影响。拓展运算符提供了复制数组的简便写法。

  ```
  const a1 = [1, 2];
  // 写法一
  const a2 = [...a1];
  // 写法二
  const [...a2] = a1;
  ```

- 合并数组

  ```
  const arr1 = ['a', 'b'];
  const arr2 = ['c'];
  const arr3 = ['d', 'e'];
  
  // ES5 的合并数组
  arr1.concat(arr2, arr3);
  // [ 'a', 'b', 'c', 'd', 'e' ]
  
  // ES6 的合并数组
  [...arr1, ...arr2, ...arr3]
  // [ 'a', 'b', 'c', 'd', 'e' ]
  ```

  都是浅拷贝，修改了原数组会同步反应到新数组

- 解构赋值结合

  ```
  const [first, ...rest] = [1, 2, 3, 4, 5];
  first // 1
  rest  // [2, 3, 4, 5]
  
  const [first, ...rest] = [];
  first // undefined
  rest  // []
  
  const [first, ...rest] = ["foo"];
  first  // "foo"
  rest   // []
  ```

- 字符串

  将字符串转为真正的数组

  ```
  [...'hello']
  // [ "h", "e", "l", "l", "o" ]
  'x\uD83D\uDE80y'.length // 4
  [...'x\uD83D\uDE80y'].length // 3
  ```

  凡是涉及到操作四个字节的 Unicode 字符的函数，都有这个问题。因此，最好都用扩展运算符改写。

  ```
  let str = 'x\uD83D\uDE80y';
  
  str.split('').reverse().join('')
  // 'y\uDE80\uD83Dx'
  
  [...str].reverse().join('')
  // 'y\uD83D\uDE80x'
  如果不用扩展运算符，字符串的reverse操作就不正确。
  ```

- 任何iterator借口的对象，都可以用拓展运算符转化为真正的数组

- Array.from()：将类似数组的对象和可遍历的对象转化为真正的数组。可以用`Array.prototype.slice`方法替代。

  ```
  let arrayLike = {
      '0': 'a',
      '1': 'b',
      '2': 'c',
      length: 3
  };
  
  // ES5的写法
  var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']
  
  // ES6的写法
  let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
  
  ```

  `Array.from`还可以接受第二个参数，作用类似于数组的`map`方法，用来对每个元素进行处理，将处理后的值放入返回的数组。

  ```
  Array.from(arrayLike, x => x * x);
  // 等同于
  Array.from(arrayLike).map(x => x * x);
  
  Array.from([1, 2, 3], (x) => x * x)
  // [1, 4, 9]
  
  ```

- Array.of()用于将一组值，转换为数组

  ```
  Array.of(3, 11, 8) // [3,11,8]
  Array.of(3) // [3]
  Array.of(3).length // 1
  
  ```

- 数组实例的`copyWithin`方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组。

  ```
  Array.prototype.copyWithin(target, start = 0, end = this.length)
  
  ```

  - target（必需）：从该位置开始替换数据。如果为负值，表示倒数。
  - start（可选）：从该位置开始读取数据，默认为 0。如果为负值，表示倒数。
  - end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。

  ```
  // 将3号位复制到0号位
  [1, 2, 3, 4, 5].copyWithin(0, 3, 4)
  // [4, 2, 3, 4, 5]
  
  // -2相当于3号位，-1相当于4号位
  [1, 2, 3, 4, 5].copyWithin(0, -2, -1)
  // [4, 2, 3, 4, 5]
  
  ```

- find()和findIndex()

  用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为`true`的成员，然后返回该成员。如果没有符合条件的成员，则返回`undefined`。

  ```
  [1, 4, -5, 10].find((n) => n < 0)
  // -5
  ```

  数组实例的`findIndex`方法的用法与`find`方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回`-1`。

  ```
  [1, 5, 10, 15].findIndex(function(value, index, arr) {
    return value > 9;
  }) // 2
  ```

  这两个方法都可以接受第二个参数，用来绑定回调函数的`this`对象。

  ```
  find函数接收了第二个参数person对象，回调函数中的this对象指向person对象。
  ```

- fill()使用给定值，填充一个数组

  ```
  ['a', 'b', 'c'].fill(7)
  // [7, 7, 7]
  
  new Array(3).fill(7)
  // [7, 7, 7]
  ```

- `entries()`，`keys()`和`values()`——用于遍历数组。它们都返回一个遍历器对象（详见《Iterator》一章），可以用`for...of`循环进行遍历，唯一的区别是`keys()`是对键名的遍历、`values()`是对键值的遍历，`entries()`是对键值对的遍历。

- includes()返回一个布尔值，表示某个数组是否包含给定的值，与字符串的includes方法类似。

  ```
  [1, 2, 3].includes(2)     // true
  [1, 2, 3].includes(4)     // false
  [1, 2, NaN].includes(NaN) // true
  ```

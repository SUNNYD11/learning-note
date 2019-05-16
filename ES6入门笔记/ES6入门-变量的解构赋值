- 基本用法

  ```
  let [a,b,c] = [1,2,3]；
  
  let [head, ...tail] = [1, 2, 3, 4];
  head // 1
  tail // [2, 3, 4]
  
  let [x, y, ...z] = ['a'];
  x // "a"
  y // undefined
  z // []
  ```

  从数组中提取值，按照对应位置，对变量赋值。解构不成功，foo的值就会等于undefined。只要某种数据结构具有iterator接口，都可以采用数组形式的解构赋值。

- 允许指定默认值

  ```
  let [foo = true] = [];
  foo // true
  
  let [x, y = 'b'] = ['a']; // x='a', y='b'
  let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
  ```

  用===判断是否有值，等于undefined，如果一个数组成员是null，默认值不会生效。

  默认值可以引用结构赋值的其他变量，但引用变量必须已经声明。

  ```
  let [x = 1, y = x] = [1, 2]; // x=1; y=2
  let [x = y, y = 1] = [];     // ReferenceError: y is not defined
  ```

- 对象的结构赋值

  ```
  let { foo, bar } = { foo: "aaa", bar: "bbb" };
  foo // "aaa"
  bar // "bbb"
  ```

  对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

  如果变量名与属性名不一致，要写成：

  ```
  let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
  baz // "aaa"
  
  let obj = { first: 'hello', last: 'world' };
  let { first: f, last: l } = obj;
  f // 'hello'
  l // 'world'
  ```

- 内部机制：先找到同名属性，在赋给对应的变量。

- 可用于嵌套结构的对象。

- 字符串的解构赋值：

  ```
  const [a, b, c, d, e] = 'hello';
  a // "h"
  b // "e"
  c // "l"
  d // "l"
  e // "o"
  ```

- 函数参数的解构赋值

  ```
  function add([x, y]){
    return x + y;
  }
  
  add([1, 2]); // 3
  ```

- 用途

  - 交换变量的值

    ```
    let x = 1;
    let y = 2;
    
    [x, y] = [y, x];
    ```

  - 从函数返回多个值

    ```
    function example() {
      return [1, 2, 3];
    }
    let [a, b, c] = example();
    
    ```

  - 函数参数的定义

    ```
    function f([x, y, z]) { ... }
    f([1, 2, 3]);
    ```

  - 提取json

    ```
    let jsonData = {
      id: 42,
      status: "OK",
      data: [867, 5309]
    };
    
    let { id, status, data: number } = jsonData;
    
    console.log(id, status, number);
    // 42, "OK", [867, 5309]
    ```

  - 函数参数的默认值

  - 遍历map结构

    ```
    const map = new Map();
    map.set('first', 'hello');
    map.set('second', 'world');
    
    for (let [key, value] of map) {
      console.log(key + " is " + value);
    }
    // first is hello
    // second is world
    
    // 获取键名
    for (let [key] of map) {
      // ...
    }
    
    // 获取键值
    for (let [,value] of map) {
      // ...
    }
    ```

  - 输入模块的指定方法

    ```
    const { SourceMapConsumer, SourceNode } = require("source-map");
    ```

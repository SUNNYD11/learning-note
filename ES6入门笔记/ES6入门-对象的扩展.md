- 允许直接写入变量和函数，作为对象的属性和方法

  ```
  function f(x, y) {
    return {x, y};
  }
  
  // 等同于
  
  function f(x, y) {
    return {x: x, y: y};
  }
  
  --------------
  module.exports = { getItem, setItem, clear };
  // 等同于
  module.exports = {
    getItem: getItem,
    setItem: setItem,
    clear: clear
  };
  ```

  ```
  const o = {
    method() {
      return "Hello!";
    }
  };
  
  // 等同于
  
  const o = {
    method: function() {
      return "Hello!";
    }
  };
  ```

- 允许字面量定义对象时，用方法二（表达式）作为对象的属性名，即把表达式放在方括号内。

  ```
  obj['a' + 'bc'] = 123;
  ```

  ```
  let lastWord = 'last word';
  
  const a = {
    'first word': 'hello',
    [lastWord]: 'world'
  };
  
  a['first word'] // "hello"
  a[lastWord] // "world"
  a['last word'] // "world"
  ```

- `Object.assign`方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。

  ```
  const target = { a: 1 };
  
  const source1 = { b: 2 };
  const source2 = { c: 3 };
  
  Object.assign(target, source1, source2);
  target // {a:1, b:2, c:3}
  ```

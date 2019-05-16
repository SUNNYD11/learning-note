- 字符的unicode表示法

  ```
  "\u0061"
  // "a"
  
  "\uD842\uDFB7"
  // "𠮷"
  
  "\u20BB7"
  // " 7"，JavaScript 会理解成\u20BB+7。由于\u20BB是一个不可打印字符，所以只会显示一个空格，后面跟着一个7。
  ```

  ES6 对这一点做出了改进，只要将码点放入大括号，就能正确解读该字符。

  ```
  "\u{20BB7}"
  // "𠮷"
  
  "\u{41}\u{42}\u{43}"
  // "ABC"
  
  let hello = 123;
  hell\u{6F} // 123
  
  '\u{1F680}' === '\uD83D\uDE80'
  // true
  ```

- codePointAt()：方法会正确返回 32 位的 UTF-16 字符的码点。

- String.fromCodepoint()：可以识别大于`0xFFFF`的字符，弥补了`String.fromCharCode`方法的不足。在作用上，正好与`codePointAt`方法相反。但一个是定义在string对象上，一个是定义在字符串的实例对象上。

- 字符串的遍历器接口，是的字符串可以被 for...of循环遍历。

- includes()：返回布尔值，表示是否找到了参数字符串

  startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。

  endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。

  ```
  let s = 'Hello world!';
  
  s.startsWith('Hello') // true
  s.endsWith('!') // true
  s.includes('o') // true
  ```

- repeat()；返回一个新的字符串，表示将原字符串重复了n次，小数取整。

- padStart(),padEnd()：字符串补全长度

  ```
  'x'.padStart(5, 'ab') // 'ababx'
  'x'.padStart(4, 'ab') // 'abax'
  
  'x'.padEnd(5, 'ab') // 'xabab'
  'x'.padEnd(4, 'ab') // 'xaba'
  ```

- 模板字符串

  ```
  $('#result').append(`
    There are <b>${basket.count}</b> items
     in your basket, <em>${basket.onSale}</em>
    are on sale!
  `);
  ```

  用反引号（）标识。如果在模板字符串中需要使用反引号，则前面要用反斜杠转义。

  如果使用模板字符串表示多行字符串，所有的空格和缩进都会被保留在输出之中。

  如果你不想要这个换行，可以使用trim方法消除它。

  模板字符串中嵌入变量，需要将变量名写在`${}`之中。

  还能调用函数

  ```
  function fn() {
    return "Hello World";
  }
  
  `foo ${fn()} bar`
  // foo Hello World bar
  ```

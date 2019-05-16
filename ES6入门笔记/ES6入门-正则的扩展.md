- RegExp构造函数

  ```
  var regex = new RegExp('xyz', 'i');
  // 等价于
  var regex = /xyz/i;
  
  var regex = new RegExp(/abc/ig, 'i');
  //原有正则对象的修饰符会被第二个参数i覆盖
  ```

- 字符串的正则方法

  `match()`、`replace()`、`search()`和`split()`，ES6 将这 4 个方法，在语言内部全部调用`RegExp`的实例方法，从而做到所有与正则相关的方法，全都定义在`RegExp`对象上。

- 对正则添加了u修饰符，含义为"unicode模式"，会正确处理四个字节的 UTF-16 编码

  ```
  /^\uD83D/u.test('\uD83D\uDC2A') // false
  /^\uD83D/.test('\uD83D\uDC2A') // true
  ```

- 点字符

  含义是除了换行符以外的任意单个字符。对于码点大于`0xFFFF`的 Unicode 字符，点字符不能识别，必须加上`u`修饰符。

  ```
  var s = '𠮷';
  
  /^.$/.test(s) // false
  /^.$/u.test(s) // true
  ```

- y修饰符，确保匹配必须从剩余的第一个位置开始，这也就是“粘连”的涵义。当发现字符串里没有的非法字符，`g`修饰符会忽略非法字符，而`y`修饰符不会，这样就很容易发现错误。

- sticky属性表示是否设置了y修饰符。flags属性会返回正则表达式的修饰符

- s修饰符，可以使.可以匹配任意单个字符

  ```
  /foo.bar/s.test('foo\nbar') // true
  ```

  dotAll属性，返回布尔值，表示该正则表达式是否处在dotAll模式。

- 后行断言，`x`只有在`y`后面才匹配，必须写成`/(?<=y)x/`。比如，只匹配美元符号之后的数字，要写成`/(?<=\$)\d+/`。”后行否定断言“则与”先行否定断言“相反，`x`只有不在`y`后面才匹配，必须写成`/(?<!y)x/`。比如，只匹配不在美元符号后面的数字，要写成`/(?<!\$)\d+/`。

  ```
  /(?<=\$)\d+/.exec('Benjamin Franklin is on the $100 bill')  // ["100"]
  /(?<!\$)\d+/.exec('it’s is worth about €90')                // ["90"]
  ```

- 具名组匹配：允许为每一个组匹配指定一个名字，既便于阅读代码，又便于引用。

  ```
  const RE_DATE = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;
  
  const matchObj = RE_DATE.exec('1999-12-31');
  const year = matchObj.groups.year; // 1999
  const month = matchObj.groups.month; // 12
  const day = matchObj.groups.day; // 31
  ```

  “具名组匹配”在圆括号内部，模式的头部添加“问号 + 尖括号 + 组名”（`?<year>`），然后就可以在`exec`方法返回结果的`groups`属性上引用该组名。同时，数字序号（`matchObj[1]`）依然有效。

- 解构赋值和替换

  ```
  let {groups: {one, two}} = /^(?<one>.*):(?<two>.*)$/u.exec('foo:bar');
  one  // foo
  two  // bar
  ```

  ```
  let re = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/u;
  
  '2015-01-02'.replace(re, '$<day>/$<month>/$<year>')
  // '02/01/2015'
  ```

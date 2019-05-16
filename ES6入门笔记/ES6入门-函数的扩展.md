- 函数参数的默认值

  允许为函数参数设置默认值，直接写在参数定义后面

- 指定了默认值以后，函数的length属性，将返回没有指定默认值的参数个数。如果设置了默认值的参数不是尾参数，那么`length`属性也不再计入后面的参数了。

  ```
  (function (a = 0, b, c) {}).length // 0
  (function (a, b = 1, c) {}).length // 1
  ```

- 设置了参数的默认值，在声明初始化时，参数会形成一个单独的作用域。

  ```
  var x = 1;
  
  function f(x, y = x) {
    console.log(y);
  }
  
  f(2) // 2
  ```

- rest参数，形式(…变量名)用于获取函数的多余参数，这样就不需要使用`arguments`对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。

  ```
  function add(...values) {
    let sum = 0;
  
    for (var val of values) {
      sum += val;
    }
  
    return sum;
  }
  
  add(2, 5, 3) // 10
  ```

  rest参数后不能再有其他参数，length属性不包括rest参数。

- name属性，返回函数的函数名

- 箭头函数：用箭头(=>)定义函数

  ```
  var f = v => v;
  
  // 等同于
  var f = function (v) {
    return v;
  };
  ```

  简化回调函数

  ```
  // 正常函数写法
  [1,2,3].map(function (x) {
    return x * x;
  });
  
  // 箭头函数写法
  [1,2,3].map(x => x * x);
  ```

  注意：

  - 函数体内的this是定义时所在的对象，而不是使用时所在的对象
  - 不可以当做构造函数，不能使用new命令
  - 不可以用arguments对象，该对象不存在
  - 不可以使用yield命令，不能用作generator函数
  - this，arguments，super，new.target在箭头函数之中都不存在，指向外层函数的对应变量。

- 双冒号运算符，用来取代call、apply、bind

  函数绑定运算符是并排的两个冒号（`::`），双冒号左边是一个对象，右边是一个函数。该运算符会自动将左边的对象，作为上下文环境（即`this`对象），绑定到右边的函数上面。

  ```
  foo::bar;
  // 等同于
  bar.bind(foo);
  
  foo::bar(...arguments);
  // 等同于
  bar.apply(foo, arguments);
  
  const hasOwnProperty = Object.prototype.hasOwnProperty;
  function hasOwn(obj, key) {
    return obj::hasOwnProperty(key);
  }
  ```

- 尾调用：某个函数的最后一步是调用另一个函数。

- 尾递归：函数调用自身，称为递归。如果尾调用自身，就称为尾递归。尾递归优化，返回一个函数，将结果传给函数继续执行。

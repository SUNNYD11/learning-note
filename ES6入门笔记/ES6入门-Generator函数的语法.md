- 语法上，首先可以把它理解成，Generator 函数是一个状态机，封装了多个内部状态。

  执行 Generator 函数会返回一个遍历器对象，也就是说，Generator 函数除了状态机，还是一个遍历器对象生成函数。返回的遍历器对象，可以依次遍历 Generator 函数内部的每一个状态。

- 两个特征。一是，`function`关键字与函数名之间有一个星号；二是，函数体内部使用`yield`表达式，定义不同的内部状态（`yield`在英语里的意思就是“产出”）。

  ```
  function* helloWorldGenerator() {
    yield 'hello';
    yield 'world';
    return 'ending';
  }
  
  var hw = helloWorldGenerator();
  ```

- Generator 函数的调用方法与普通函数一样，也是在函数名后面加上一对圆括号。不同的是，调用 Generator 函数后，该函数并不执行，返回的也不是函数运行结果，而是一个指向内部状态的指针对象，也就是上一章介绍的遍历器对象（Iterator Object）。

  下一步，必须调用遍历器对象的`next`方法，使得指针移向下一个状态。也就是说，每次调用`next`方法，内部指针就从函数头部或上一次停下来的地方开始执行，直到遇到下一个`yield`表达式（或`return`语句）为止。换言之，Generator 函数是分段执行的，`yield`表达式是暂停执行的标记，而`next`方法可以恢复执行。

- 由于 Generator 函数返回的遍历器对象，只有调用`next`方法才会遍历下一个内部状态，所以其实提供了一种可以暂停执行的函数。`yield`表达式就是暂停标志。

  （1）遇到`yield`表达式，就暂停执行后面的操作，并将紧跟在`yield`后面的那个表达式的值，作为返回的对象的`value`属性值。

  （2）下一次调用`next`方法时，再继续往下执行，直到遇到下一个`yield`表达式。

  （3）如果没有再遇到新的`yield`表达式，就一直运行到函数结束，直到`return`语句为止，并将`return`语句后面的表达式的值，作为返回的对象的`value`属性值。

  （4）如果该函数没有`return`语句，则返回的对象的`value`属性值为`undefined`。

- `yield`表达式本身没有返回值，或者说总是返回`undefined`。`next`方法可以带一个参数，该参数就会被当作上一个`yield`表达式的返回值。第一次使用next传入方法是无效的

- `for...of`循环可以自动遍历 Generator 函数时生成的`Iterator`对象，且此时不再需要调用`next`方法。不包含return的返回。

  ```
  function* foo() {
    yield 1;
    yield 2;
    yield 3;
    yield 4;
    yield 5;
    return 6;
  }
  
  for (let v of foo()) {
    console.log(v);
  }
  // 1 2 3 4 5
  ```

- Generator 函数返回的遍历器对象，都有一个`throw`方法，可以在函数体外抛出错误，然后在 Generator 函数体内捕获。

  ```
  var g = function* () {
    try {
      yield;
    } catch (e) {
      console.log('内部捕获', e);
    }
  };
  
  var i = g();
  i.next();
  
  try {
    i.throw('a');
    i.throw('b');
  } catch (e) {
    console.log('外部捕获', e);
  }
  // 内部捕获 a
  // 外部捕获 b
  遍历器对象i连续抛出两个错误。第一个错误被 Generator 函数体内的catch语句捕获。i第二次抛出错误，由于 Generator 函数内部的catch语句已经执行过了，不会再捕捉到这个错误了，所以这个错误就被抛出了 Generator 函数体，被函数体外的catch语句捕获。
  ```

- 一旦 Generator 执行过程中抛出错误，且没有被内部捕获，就不会再执行下去了。如果此后还调用`next`方法，将返回一个`value`属性等于`undefined`、`done`属性等于`true`的对象，即 JavaScript 引擎认为这个 Generator 已经运行结束了。

- Generator 函数返回的遍历器对象，还有一个`return`方法，可以返回给定的值，并且终结遍历 Generator 函数。

  ```
  function* gen() {
    yield 1;
    yield 2;
    yield 3;
  }
  
  var g = gen();
  
  g.next()        // { value: 1, done: false }
  g.return('foo') // { value: "foo", done: true }
  g.next()        // { value: undefined, done: true }
  ```

  遍历器对象`g`调用`return`方法后，返回值的`value`属性就是`return`方法的参数`foo`。并且，Generator 函数的遍历就终止了，返回值的`done`属性为`true`，以后再调用`next`方法，`done`属性总是返回`true`。

  如果`return`方法调用时，不提供参数，则返回值的`value`属性为`undefined`。

  如果 Generator 函数内部有`try...finally`代码块，那么`return`方法会推迟到`finally`代码块执行完再执行。

- `next()`、`throw()`、`return()`这三个方法本质上是同一件事，可以放在一起理解。它们的作用都是让 Generator 函数恢复执行，并且使用不同的语句替换`yield`表达式。

- `yield*`表达式，用来在一个 Generator 函数里面执行另一个 Generator 函数。

  ```
  function* foo() {
    yield 'a';
    yield 'b';
  }
  function* bar() {
    yield 'x';
    yield* foo();
    yield 'y';
  }
  
  // 等同于
  function* bar() {
    yield 'x';
    yield 'a';
    yield 'b';
    yield 'y';
  }
  
  // 等同于
  function* bar() {
    yield 'x';
    for (let v of foo()) {
      yield v;
    }
    yield 'y';
  }
  
  for (let v of bar()){
    console.log(v);
  }
  // "x"
  // "a"
  // "b"
  // "y"
  ```

  如果`yield*`后面跟着一个数组，由于数组原生支持遍历器，因此就会遍历数组成员。

  ```
  function* gen(){
    yield* ["a", "b", "c"];
  }
  
  gen().next() // { value:"a", done:false }
  ```

  上面代码中，`yield`命令后面如果不加星号，返回的是整个数组，加了星号就表示返回的是数组的遍历器对象。

- 协程：多个线程（单线程情况下，即多个函数）可以并行执行，但是只有一个线程（或函数）处于正在运行的状态，其他线程（或函数）都处于暂停态（suspended），线程（或函数）之间可以交换执行权。

- 

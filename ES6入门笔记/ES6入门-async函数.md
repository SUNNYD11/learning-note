- async 函数是什么？一句话，它就是 Generator 函数的语法糖。

- `async`函数就是将 Generator 函数的星号（`*`）替换成`async`，将`yield`替换成`await`，仅此而已。

- 内置执行器

  ```
  asyncReadFile();//调用了asyncReadFile函数，然后它就会自动执行，输出最后结果
  ```

- 更好的语义

  `async`和`await`，比起星号和`yield`，语义更清楚了。`async`表示函数里有异步操作，`await`表示紧跟在后面的表达式需要等待结果

- 更广的适用性

  `co`模块约定，`yield`命令后面只能是 Thunk 函数或 Promise 对象，而`async`函数的`await`命令后面，可以是 Promise 对象和原始类型的值（数值、字符串和布尔值，但这时等同于同步操作）。

- 返回值是 Promise

  `async`函数的返回值是 Promise 对象，这比 Generator 函数的返回值是 Iterator 对象方便多了。你可以用`then`方法指定下一步的操作。

- 进一步说，`async`函数完全可以看作多个异步操作，包装成的一个 Promise 对象，而`await`命令就是内部`then`命令的语法糖。

- `await`命令后面是一个 Promise 对象。如果不是，就返回对应的值。

  ```
  async function f() {
    // 等同于
    // return 123;
    return await 123;
  }
  
  f().then(v => console.log(v))
  // 123
  ```

  只要一个`await`语句后面的 Promise 变为`reject`，那么整个`async`函数都会中断执行。

  有时，我们希望即使前一个异步操作失败，也不要中断后面的异步操作。这时可以将第一个`await`放在`try...catch`结构里面，这样不管这个异步操作是否成功，第二个`await`都会执行。

- 注意点：

  - `await`命令后面的`Promise`对象，运行结果可能是`rejected`，所以最好把`await`命令放在`try...catch`代码块中。

  - 多个`await`命令后面的异步操作，如果不存在继发关系，最好让它们同时触发。

    ```
    // 写法一
    let [foo, bar] = await Promise.all([getFoo(), getBar()]);
    
    // 写法二
    let fooPromise = getFoo();
    let barPromise = getBar();
    let foo = await fooPromise;
    let bar = await barPromise;
    ```

  - `await`命令只能用在`async`函数之中，如果用在普通函数，就会报错。

- async实现原理

  将 Generator 函数和自动执行器，包装在一个函数里。

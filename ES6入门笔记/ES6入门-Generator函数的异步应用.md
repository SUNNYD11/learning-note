- 异步：可以理解成该任务被人为分成两段，先执行第一段，然后转而执行其他任务，等做好了准备，再回过头执行第二段。

- 回调函数：把任务的第二段单独写在一个函数里面，等到重新执行这个任务的时候，就直接调用这个函数。

- "协程"（coroutine），意思是多个线程互相协作，完成异步任务。

  协程遇到`yield`命令就暂停，等到执行权返回，再从暂停的地方继续往后执行。它的最大优点，就是代码的写法非常像同步操作，如果去除`yield`命令，简直一模一样。

- Generator 函数是协程在 ES6 的实现，最大特点就是可以交出函数的执行权（即暂停执行）。

- 函数体内外的数据交换和错误处理机制

  `next`返回值的 value 属性，是 Generator 函数向外输出数据；`next`方法还可以接受参数，向 Generator 函数体内输入数据。

  Generator 函数内部还可以部署错误处理代码，捕获函数体外抛出的错误。使用指针对象的`throw`方法抛出的错误，可以被函数体内的`try...catch`代码块捕获。

  ```
  function* gen(x){
      try {
          var y = yield x + 2;
      } catch (e){
          console.log(e+3);
      }
      return y;
  }
  var g = gen(1);
  let a = g.next().value;
  console.log(a)
  if(a === 2){
  console.log(g.next())
  }else{
      g.throw('出错了');
  }
  // 出错了3
  ```

- Thunk 函数是自动执行 Generator 函数的一种方法。

- 编译器的“传名调用”实现，往往是将参数放到一个临时函数之中，再将这个临时函数传入函数体。这个临时函数就叫做 Thunk 函数。

- Thunkify模块。生产环境的转换器

- Thunk 函数的自动流程管理，在于可以自动执行 Generator 函数.

  ```
  function run(fn) {
    var gen = fn();
  
    function next(err, data) {
      var result = gen.next(data);
      if (result.done) return;
      result.value(next);
    }
  
    next();
  }
  
  function* g() {
    // ...
  }
  
  run(g);
  ```

  内部的`next`函数就是 Thunk 的回调函数。`next`函数先将指针移到 Generator 函数的下一步（`gen.next`方法），然后判断 Generator 函数是否结束（`result.done`属性），如果没结束，就将`next`函数再传入 Thunk 函数（`result.value`属性），否则就直接退出。

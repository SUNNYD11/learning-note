- Promise 是异步编程的一种解决方案，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。

- 从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

- 两个特点：

  - 对象的状态不受外界影响。
  - 一旦状态改变，就不会再变。

- 用法

  ```
  const promise = new Promise(function(resolve, reject) {
    // ... some code
  
    if (/* 异步操作成功 */){
      resolve(value);
    } else {
      reject(error);
    }
  });
  ```

- Promise 实例具有`then`方法，也就是说，`then`方法是定义在原型对象`Promise.prototype`上的。它的作用是为 Promise 实例添加状态改变时的回调函数。

- `Promise.prototype.catch`方法是`.then(null, rejection)`的别名，用于指定发生错误时的回调函数。

  如果异步操作抛出错误，状态就会变为`rejected`，就会调用`catch`方法指定的回调函数，处理这个错误。另外，`then`方法指定的回调函数，如果运行中抛出错误，也会被`catch`方法捕获。

- Promise.all():将多个promise实例，包装成一个新的promise实例。

  ```
  const p = Promise.all([p1, p2, p3]);
  ```

  `Promise.all`方法接受一个数组作为参数数，p1、p2、p3都是 Promise 实例。（`Promise.all`方法的参数可以不是数组，但必须具有 Iterator 接口，且返回的每个成员都是 Promise 实例。）

  `p`的状态由`p1`、`p2`、`p3`决定，分成两种情况。

  （1）只有`p1`、`p2`、`p3`的状态都变成`fulfilled`，`p`的状态才会变成`fulfilled`，此时`p1`、`p2`、`p3`的返回值组成一个数组，传递给`p`的回调函数。

  （2）只要`p1`、`p2`、`p3`之中有一个被`rejected`，`p`的状态就变成`rejected`，此时第一个被`reject`的实例的返回值，会传递给`p`的回调函数。

- `Promise.race`方法同样是将多个 Promise 实例，包装成一个新的 Promise 实例。

  ```
  const p = Promise.race([p1, p2, p3]);
  ```

  上面代码中，只要`p1`、`p2`、`p3`之中有一个实例率先改变状态，`p`的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给`p`的回调函数。

- 有时需要将现有对象转为 Promise 对象，`Promise.resolve`方法就起到这个作用`Promise.resolve`

  方法允许调用时不带参数，直接返回一个`resolved`状态的 Promise 对象。需要注意的是，立即`resolve`的 Promise 对象，是在本轮“事件循环”（event loop）的结束时，而不是在下一轮“事件循环”的开始时。

  ```
  setTimeout(function () {
    console.log('three');
  }, 0);
  
  Promise.resolve().then(function () {
    console.log('two');
  });
  
  console.log('one');
  
  // one
  // two
  // three
  ```

- `Promise.reject(reason)`方法也会返回一个新的 Promise 实例，该实例的状态为`rejected`。

------

- 应用：

  - 加载图片，一旦加载完成，`Promise`的状态就发生变化。

    ```
    const preloadImage = function (path) {
      return new Promise(function (resolve, reject) {
        const image = new Image();
        image.onload  = resolve;
        image.onerror = reject;
        image.src = path;
      });
    };
    ```

  - 使用 Generator 函数管理流程，遇到异步操作的时候，通常返回一个`Promise`对象。

  - promise.try()：让同步函数同步执行，异步函数异步执行。

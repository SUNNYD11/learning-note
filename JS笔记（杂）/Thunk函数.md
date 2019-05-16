# Thunk函数

[引用](https://segmentfault.com/a/1190000007525293)

## 1.背景

Thunk函数的诞生是源于一个编译器设计的问题：`求值策略`，即函数的参数到底应该何时求值。

```
var x = 1;
function f(m) {
    return m * 2;
}
f(x + 5);
```

x+5何时求值，有两种思路

- 传值调用(call by value)，即在进入函数体之间，先计算x+5的值，再将这个值（6）传入函数f，例如c语言，这种做法的好处是实现比较简单，但是有可能会造成性能损失。
- 名调用(call by name)，即直接将表达式(x+5)传入函数体，只在用到它的时候求值。



## 2.Thunk函数的含义

编译器的`传名调用`实现，往往就是将参数放到一个临时函数之中，再将这个临时函数转入函数体，这个临时函数就叫做`Thunk函数`。

```
function f(m) {
    return m*2;
}

f(x + 5);

// 等价于以下代码
var thunk = function () {
    return x + 5;
};

function f(thunk) {
    return thunk() * 2;
}
```



## 3.javascript中的Thunk函数

1.高阶函数：可以接受另一个函数作为参数传递或者返回值输出的函数。

2.柯里化：只传递给函数一部分参数来调用它，让它返回一个函数去处理剩下的参数。

3.在Javascript语言中，Thunk函数替换的不是表达式，而是多参数函数，将其替换成单参数的版本，且只接受回调函数作为参数。

```
// 正常版本的readFile（多参数版本）
fs.readFile(fileName, callback);

// Thunk版本的readFile（单参数版本）
var readFileThunk = Thunk(fileName);
readFileThunk(callback);

var Thunk = function (fileName){
  return function (callback){
    return fs.readFile(fileName, callback); 
  };
};
```



## 4.Thunkify 模块

生产环境转换器，将参数有毁掉函数的函数转换成thunk函数的形式，变量called保证回调函数只运行一次。

```
function thunkify(fn){
  return function(){
    var args = new Array(arguments.length);
    var ctx = this;

    for(var i = 0; i < args.length; ++i) {
      args[i] = arguments[i];
    }

    return function(done){
      var called;

      args.push(function(){
        if (called) return;
        called = true;
        done.apply(null, arguments);
      });

      try {
        fn.apply(ctx, args);
      } catch (err) {
        done(err);
      }
    }
  }
};
```



## 5.Generator 函数的流程管理

 yield 命令用于将程序的执行权移出 Generator 函数，那么就需要一种方法，将执行权再交还给 Generator 函数。

这种方法就是 Thunk 函数，因为它可以在回调函数里，将执行权交还给 Generator 函数。为了便于理解，我们先看如何手动执行上面这个 Generator 函数。

Thunk 函数真正的威力，在于可以自动执行 Generator 函数。下面就是一个基于 Thunk 函数的 Generator 执行器。

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

run(gen);
```

上面代码的 run 函数，就是一个 Generator 函数的自动执行器。内部的 next 函数就是 Thunk 的回调函数。 next 函数先将指针移到 Generator 函数的下一步（gen.next 方法），然后判断 Generator 函数是否结束（result.done 属性），如果没结束，就将 next 函数再传入 Thunk 函数（result.value 属性），否则就直接退出。

有了这个执行器，执行 Generator 函数方便多了。不管有多少个异步操作，直接传入 run 函数即可。当然，前提是每一个异步操作，都要是 Thunk 函数，也就是说，跟在 yield 命令后面的必须是 Thunk 函数。

```
var gen = function* (){
  var f1 = yield readFile('fileA');
  var f2 = yield readFile('fileB');
  // ...
  var fn = yield readFile('fileN');
};

run(gen);
```

上面代码中，函数 gen 封装了 n 个异步的读取文件操作，只要执行 run 函数，这些操作就会自动完成。这样一来，异步操作不仅可以写得像同步操作，而且一行代码就可以执行。

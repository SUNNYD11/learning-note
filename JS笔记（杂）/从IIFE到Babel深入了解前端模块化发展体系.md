- IIFE：

  - 一开始只是简单的用文件区分，一个html加上若干个js文件来区分不同的模块。
  - 导致的问题是无法区分变量，js文件之间可以相互修改变量。
  - 解决方法：用函数将变量包裹起来，这样变量就不会直接被声明在全局变量window上。但是函数仍然window上。
  - 改进解决方法：IIFE，立即执行的匿名函数。执行完会很快被释放，所以不会污染全局对象。

- CommonJS：在web浏览器之外，为js建立模块生态系统的约定的项目。

  - node.js模块系统，每个文件都被视为一个单独的模块，每个模块的变量是私有的，实现方法是通过吧nodejs的模块包装在一个函数中。

    ```
    (function(exports, require, module, __filename, __dirname) {
    // Module code actually lives in here
    // 实际上，模块内的代码被放在这里
    });
    ```

  - 和IIFEd不同:

    - 暴露自己的方法或者变量的能力：exports(导出对象)、module(模块的引用)
    - 引入其他模块的能力：(require)
    - 能表示自己的物理位置：(_filename:绝对文件名，__dirname:目录路径)

  - 弊端：初衷为了js在多个环境下都实现模块化，但是nodejs的实现依赖了nodejs的环境变量(module,exports,require,global)

- RequireJS & AMD

  - 解决浏览器环境下，使用require()复制过程中，会导致阻塞的问题。异步的模块化管理。
  - 缺点，依赖前置，所有依赖的模块都要提前执行好。

- SeaJS & CMD

  - 解决AMD依赖问题，特点依赖就近+延迟执行。

  

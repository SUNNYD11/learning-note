# CMD

- 每一个node.js执行文件，都会创建一个module对象，module对象会创建一个exports熟悉，初始化的值是{}

  - Module.exports和exports的初始值都是{}
  - Exports是指向module.exports的引用
  - Module.exports赋值后已经和exports指向的变量不同了
  - requir()返回的是module.exports而不是exports
  - export 只是 module.exports 的引用或者别名。真正起作用的是 module.exports ，如果给 exports 重新赋值，那么 exports 和 module.exports 将不再有关系。

- 标准模板分装模板定义

  ```
  define(function(require, exports, module) {
  
    // The module code goes here
  
  });
  ```

  Math.js

  ```
  define(function(require, exports, module) {
    exports.add = function() {
      var sum = 0, i = 0, args = arguments, l = args.length;
      while (i < l) {
        sum += args[i++];
      }
      return sum;
    };
  });
  ```

# CommonJS

- 规范：1.定义  2.引用  3.标识

- 唯一的出口，module.exports对象

  - module变量就是整个模块，module变量有个属性叫exports，是exports变量的引用，最后到处的还是module.exports。所以可以用module.exports={}，和exports.a='aaa'导出，但不用用exports={}。
  - 因为最后导出的是module.exports属性, 所以如果是对exports的属性赋值, 那么会让module.exports对象的属性也一起变化, 而直接对整个exports对象赋值, 那么exports和module.exports变成了两个完全不同的对象, 在内存中指向的地址都不一样啦, exports对象当然影响不到module.exports

- 引用。require('moduleName')，然后require方法会返回模块中导出的module.exports对象

- 模块的标识：

  1. 是符合"小驼峰"式命名法的字符串. (从node_modules/系统模块中引入)
  2. 以'.' 或 '..' 开头相对路径模块(相对当前目录引入)
  3. 绝对路径(例如/var/www等绝对路径)

  需要提到的一小点是, *文件后缀名".js"可以省略.*

- 同步加载模块，速度慢，性能等问题

# AMD

- 异步加载模块，提前加载

- **其核心接口是**：define(id?, dependencies?, factory) ，它要在声明模块的时候指定所有的依赖 dependencies ，并且还要当做形参传到factory 中，对于依赖的模块提前执行，依赖前置。

- ```js
  define("module", ["dep1", "dep2"], function(d1, d2) {
    return someExportedValue;
  });
  require(["module", "../file"], function(module, file) { /* ... */ });
  ```

- 

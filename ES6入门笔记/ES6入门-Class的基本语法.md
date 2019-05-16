- Class：ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过`class`关键字，可以定义类。

- ES6 的`class`可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的`class`写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

  ```
  //定义类
  class Point {
    constructor(x, y) {
      this.x = x;
      this.y = y;
    }
  
    toString() {
      return '(' + this.x + ', ' + this.y + ')';
    }
  }
  上面代码定义了一个“类”，可以看到里面有一个constructor方法，这就是构造方法，而this关键字则代表实例对象。也就是说，ES5 的构造函数Point，对应 ES6 的Point类的构造方法。
  ```

- 使用的时候，也是直接对类使用`new`命令，跟构造函数的用法完全一致。

  ```
  class Bar {
    doStuff() {
      console.log('stuff');
    }
  }
  
  var b = new Bar();
  b.doStuff() // "stuff"
  ```

- constructor方法

  `constructor`方法是类的默认方法，通过`new`命令生成对象实例时，自动调用该方法。一个类必须有`constructor`方法，如果没有显式定义，一个空的`constructor`方法会被默认添加。

  `constructor`方法默认返回实例对象（即`this`），完全可以指定返回另外一个对象。

- 类不存在变量提升

- class的静态方法；类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上`static`关键字，就表示该方法不会被实例继承，而是直接通过类来调用，这就称为“静态方法”。

  可以被继承，可以和非静态方法重名

  ```
  class Foo {
    static classMethod() {
      return 'hello';
    }
  }
  
  Foo.classMethod() // 'hello'
  
  var foo = new Foo();
  foo.classMethod()
  // TypeError: foo.classMethod is not a function
  ```

- 构造方法this指向实例，静态方法中的this，指向类。

- class的静态属性和实例 属性

  - 静态属性指的是 Class 本身的属性，即`Class.propName`，而不是定义在实例对象（`this`）上的属性。
  - 目前，只有这种写法可行，因为 ES6 明确规定，Class 内部只有静态方法，没有静态属性。
  - 类的实例属性可以用等式，写入类的定义之中。

- ES6 为`new`命令引入了一个`new.target`属性，该属性一般用在构造函数之中，返回`new`命令作用于的那个构造函数。如果构造函数不是通过`new`命令调用的，`new.target`会返回`undefined`，因此这个属性可以用来确定构造函数是怎么调用的。

  确保是new调用的

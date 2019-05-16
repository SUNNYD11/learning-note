- 类的修饰器

  用来修改类的行为

  ```
  @testable
  class MyTestableClass {
    // ...
  }
  
  function testable(target) {
    target.isTestable = true;
  }
  
  MyTestableClass.isTestable // true
  @testable就是一个修饰器。它修改了MyTestableClass这个类的行为，为它加上了静态属性isTestable。testable函数的参数target是MyTestableClass类本身。
  ```

- 修饰器是一个对类进行处理的函数。修饰器函数的第一个参数，就是所要修饰的目标类。

  ```
  @decorator
  class A {}
  
  // 等同于
  
  class A {}
  A = decorator(A) || A;
  ```

- 二进制和八进制表示法

  ```
  0b111110111 === 503 // true   0b二进制
  0o767 === 503 // true    0o八进制
  ```

- Number.parseInt(), Number.parseFloat()

  将全局方法`parseInt()`取整和`parseFloat()`小数，移植到`Number`对象上面，行为完全保持不变。

- Number.isInteger()：判断一个数值是否为整数

- Math对象的扩展：

  - Math.trunc()用于去除一个数的小数部分，返回整数部分。

  - Math.sign()判断一个是正负零。

  - Math.cbrt()计算立方根

  - `Math.hypot`方法返回所有参数的平方和的平方根

  - 指数运算：**

    ```
    2 ** 2 // 4
    2 ** 3 // 8
    ```

    ```
    // 相当于 2 ** (3 ** 2)
    2 ** 3 ** 2
    // 512
    ```

    ```
    let a = 1.5;
    a **= 2;
    // 等同于 a = a * a;
    
    let b = 4;
    b **= 3;
    // 等同于 b = b * b * b;
    ```


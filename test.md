# 测试总结

## 目的

- 测试可以确保得到预期结果。
- 加快开发速度。
- 方便维护。
- 提供用法的文档。



------



## 类型

- 单元测试（unit testing）- 通过模拟输入和预测输出的方式测试独立的函数或者类。
- 功能测试（feature testing）
- 集成测试（integration testing）- 测试多个模块间的联动是否和期望相同。
- UI 测试 (也被称为 Functional Test) - 关注点不在内部实现方式，而是测试产品在真实使用场景（比如在浏览器）中是否可以达到预想的结果。

------



## 测试工具类型

提供**测试结构**：[Mocha](https://link.zhihu.com/?target=https%3A//mochajs.org/), [Jasmine](https://link.zhihu.com/?target=http%3A//jasmine.github.io/), [Jest](https://link.zhihu.com/?target=https%3A//facebook.github.io/jest/), [Cucumber](https://link.zhihu.com/?target=https%3A//github.com/cucumber/cucumber-jshttps%3A//github.com/cucumber/cucumber-js)

有**断言**测试：[Chai](https://link.zhihu.com/?target=http%3A//chaijs.com/), [Jasmine](https://link.zhihu.com/?target=http%3A//jasmine.github.io/), [Jest](https://link.zhihu.com/?target=https%3A//facebook.github.io/jest/), [Unexpected](https://link.zhihu.com/?target=http%3A//unexpected.js.org/)

生成、**展示和监控**测试结果：[Mocha](https://link.zhihu.com/?target=https%3A//mochajs.org/), [Jasmine](https://link.zhihu.com/?target=http%3A//jasmine.github.io/), [Jest](https://link.zhihu.com/?target=https%3A//facebook.github.io/jest/), [Karma](https://link.zhihu.com/?target=https%3A//karma-runner.github.io/)

通过对比生成的组件和数据结构的快照，确保更改是来自前一次运行的：[Jest](https://link.zhihu.com/?target=https%3A//facebook.github.io/jest/), [Ava](https://link.zhihu.com/?target=https%3A//github.com/avajs/ava)

提供 **Mocks、Spies 和 Stubs**：[Sinon](https://link.zhihu.com/?target=http%3A//sinonjs.org/), [Jasmine](https://link.zhihu.com/?target=http%3A//jasmine.github.io/), [enzyme](https://link.zhihu.com/?target=http%3A//airbnb.io/enzyme/docs/api/), [Jest](https://link.zhihu.com/?target=https%3A//facebook.github.io/jest/), [testdouble](https://link.zhihu.com/?target=https%3A//github.com/testdouble/testdouble.js)

生成**代码覆盖**报告：[Istanbul](https://link.zhihu.com/?target=https%3A//gotwarlost.github.io/istanbul/), [Jest](https://link.zhihu.com/?target=https%3A//facebook.github.io/jest/), [Blanket](https://link.zhihu.com/?target=http%3A//blanketjs.org/)

提供一个**浏览器或类浏览器环境**，并提供接口可以控制它们的执行场景：[Protractor](https://link.zhihu.com/?target=http%3A//www.protractortest.org/)**,** [Nightwatch](https://link.zhihu.com/?target=http%3A//nightwatchjs.org/), [Phantom](https://link.zhihu.com/?target=http%3A//phantomjs.org/)**,** [Casper](https://link.zhihu.com/?target=http%3A//casperjs.org/)

------



## 单元测试

功能测试指的是，站在外部用户的角度，测试软件的某项功能。

与内部代码实现无关，只测试功能是否正常。

很多时候，单元测试都可以通过，但是整体功能会失败。

- Mocha：常用的测试框架

  （1）需要测试的脚本

  ```
  function add(x, y) {
    return x + y;
  }
  
  module.exports = add;
  ```

  （2）测试脚本。测试脚本与所要测试的源码脚本同名，但是后缀名为.test.js（表示测试）或者.spec.js（表示规格）。比如，add.js的测试脚本名字就是add.test.js。

  ```
  var add = require('./add.js');
  var expect = require('chai').expect;
  
  describe('加法函数的测试', function() {
    it('1 加 1 应该等于 2', function() {
      expect(add(1, 1)).to.be.equal(2);
      //断言。是判断源码的实际执行结果与预期结果是否一致，如果不一致就抛出一个错误。上面这句断言的意思是，调用add(1, 1)，结果应该等于2。
    });
  });
  ```

  测试脚本里面应该包括一个或多个`describe`块，每个`describe`块应该包括一个或多个`it`块。

  `describe`块称为"测试套件"（test suite），表示一组相关的测试。它是一个函数，第一个参数是测试套件的名称（"加法函数的测试"），第二个参数是一个实际执行的函数。

  `it`块称为"测试用例"（test case），表示一个单独的测试，是测试的最小单位。它也是一个函数，第一个参数是测试用例的名称（"1 加 1 应该等于 2"），第二个参数是一个实际执行的函数。

  所有的测试用例（`it`块）都应该含有一句或多句的断言。它是编写测试用例的关键。断言功能由断言库来实现，Mocha本身不带断言库，所以必须先引入断言库。

  ```
  var expect = require('chai').expect;
  ```

  上面代码引入的断言库是`chai`，并且指定使用它的`expect`断言风格。

  （3）打开`package.json`文件，改写`scripts`字段的`test`脚本。

  ```
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  
  // 改成
  
  "scripts": {
    "test": "mocha *.test.js"
  },
  ```

  （4）npm test。命令会提示测试是否通过

------



## 功能测试

- 功能测试必须在真正浏览器做，现在有四种方法。

  - 使用本机安装的浏览器
  - 使用 Selenium Driver
  - 使用 Headless Chrome
  - 使用 Electron

- Nightmare：使用 Electron 模拟真实浏览器环境。提供大量人性化、易用的 API。

  （1）浏览器自动化脚本`taobao.test.js`。

  ```
  var Nightmare = require('nightmare');
  var nightmare = Nightmare({ show: true });
  ```

  上面代码表示新建一个 Nightmare 实例，并且运行功能中，自动打开浏览器窗口。

  ```
  nightmare
    .goto('https://www.taobao.com/')
    .type('#q', '电视机')
    .click('form[action*="/search"] [type=submit]')
    .wait('#spulist-grid')
    .evaluate(function () {
      return document.querySelector('#spulist-grid .grid-item .info-cont')
        .textContent.trim();
    })
    .end()
  ```

  上面代码表示，打开淘宝首页，在搜索框键入`电视机`，点击“搜索”按钮，等待`#spulist-grid`元素出现，在页面内注入（`evaluate`）代码，将执行结果返回。

  ```
    .then(function (result) {
      console.log(result);
    })
    .catch(function (error) {
      console.error('Search failed:', error);
    });
  ```

  Nightmare 会返回一个 Promise 对象，`then`方法指定操作成功的回调函数，`catch`方法指定操作失败的回调函数。

  （2）运行node taobao.test.js。会显示电视机搜索结果的第一项。 

------




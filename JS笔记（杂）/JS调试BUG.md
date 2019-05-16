## Chorme断点调试

- 重现bug
- 用断点暂停代码
  - 打开调试器
  - 点击source标签
  - 点击“event listener breakpoints”事件监听断点，展开
  - 在mouse类型里选择click
  - 然后在点击页面里的按钮，就会暂停在click函数那里
- 逐步调试代码
  - 在 DevTools 的“Source”面板上，点击“Step into next function call”，这个按钮能让你逐步查看 onClick() 函数的运行，每次一行。当 DevTools 高亮显示如下一行代码时就停止
  - 现在点击“Step over next function call”按钮，这会让 DevTools 执行 inputsAreEmpty() 而不进入他
- 设置另一个断点
  - 代码行断点，在代码左侧点击放置一个蓝色图标，这样devtools就会在执行到这行代码前暂停
  - 还会打印出变量值
- 检查变量值
  - 用watch expressions 能够监控变量值，还能降任何有效的js表达式存储在里面。
  - 在 DevTools 上的“Source”面板上点击“Watch”，然后这部分会展开。
  - 点击“Add Expression”
  - 输入 typeof sum
  - 按 Enter 键，DevTools 会显示 typeof sum: "string"。冒号右边的值就是你的 Watch Expression 的结果。
  - 在console里面直接输入也会直接打印出来对应数据
- 应用修复方法
  - 在source里面，用正确代码直接替换错误代码
  - 按command+s保存修改，点击运行就能看到正确结果
- 利用console.table()来打印数组和对象
- 要检查click事件问题，在click内部第一行打断点，然后按图标或者f10逐步执行
- 打印变量方法：
  - 在执行完当前行以后，点击变量，鼠标悬浮在上方，就能看到结果
  - 执行完当前行后，打开sources边上的console，输入变量回车就能看到变量的值
  - 上面的方法，输入$(this)可以打印当前选中的元素
- 检查顺序：
  1. js是否成功的执行
  2. js是否存在逻辑问题，变量问题，参数问题

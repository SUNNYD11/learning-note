- 特点：易于使用，能应用在多个页面，层叠，缩减文件大小（减少类似font元素的HTML标记消耗）

- 元素：文档结构的基础，如p，span，每个元素生成一个框，也被称为盒。

- 替换元素：用来替换元素内容的部分。如img，由文档本身之外的一个图像文件替换

- 非替换元素：内容有用户代理在元素本身生成的框中显示。如span、段落、标题、表格

- 块级元素：生成一个元素框，填充其父元素的内容区，旁边不能有其他元素，如p，div

- 行内元素：在一个文本行内生成元素框，不会在本身之前或之后生成分隔符，如a。

- display：none，block，inline，inline-block

  参考：https://www.cnblogs.com/zhuzhenwei918/p/6058457.html

  - none：表示此元素将不被显示。例如用于二级下拉菜单
  - block：将元素显示为块级元素，前后带有换行符。可以将行内元素设置为block来设置宽高和上下padding和margin
  - inline：将元素显示为行内元素，前后没有换行符，也不能设置宽高和上下padding，margin
  - inline-block：既可以像block设置宽高属性，又能保持inline不换行的特性
  - inherit：继承父元素的display值

- positon：static、fixed、absolute、relative

  - 参考：https://www.cnblogs.com/theWayToAce/p/5264436.html
  - static：默认值，没有定位
  - relative（正常流所在的位置仍然保留，不改变display属性）：相对定位，通过top，bottom，left，right的设置对于正常位置进行定位，可通过z-index进行层次分级。以父级的左上角进行定位。
  - absolute（与relative区别是正常流的位置不再存在，设定以后行内元素display变成block，width没有设置的话变为auto）：绝对定位，相对于static定位以外的第一个父元素进行定位。通过left，top，bottom进行规定，可通过z-index进行层次分级
  - fixed：绝对定位，相对于浏览器，通过LTRB进行规定，可通过z-index进行层次分级
  - relative和absolute的主要区别
    - 在正常流中的位置存在与否
    - relative定位的层总是相对于最近的父元素
    - 对于absolute定位的层总是相对于其最近的第一位absolute或者relative的父层（并不一定是直接父层），如果都没有定义，则现象对于body进行定位

- link：加载外部样式表，必须放在head元素中，不能放在类似title元素内部。例`<link href="assets/plugins/bootstrap/css/bootstrap.min.css" rel="stylesheet" type="text/css"/>`

  rel代表关系，关系为stylesheet，type描述了使用了link标记加载的数据的类型。href的值是样式表的url

- style元素：以`<style type="text/css">`开头,`</style>`结尾，中间写一个或多个样式

- @import指令：例@import url（aaa.css），与link类似，用于加载一个外部样式表，必须放在所有css样式之前。可以用于一个外部样式表需要使用其他外部样式，此时不能包含任何文档标记，所以不能用link，但是可以用.@import

- 注释：用`/*`和`*/`包围

- 内联样式：在html里使用style属性来设置一个内联样式。可以和body内部的标记关联，但不能用@import，也不能包含完整的样式表。不推荐使用。 

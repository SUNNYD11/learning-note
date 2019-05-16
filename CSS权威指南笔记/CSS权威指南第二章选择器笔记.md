# 基本规则

- 规则结构：由选择器和声明块组成。声明块由一个或多个声明组成，每个声明则是属性-值对，每个样式表由一系列规则组成

- 元素选择器：选择器通常是某个html元素，如p、h3、甚至是html本身

- 属性可以有多个关键字，由空格分隔

- 选择器/声明分组，利用逗号/分号分隔

  `h2，p {color:red;font-size:18px;}`

- 通配选择器:*，可以和任何元素匹配

  `* {color:red}`

- 类选择器：根据class属性选择

  `.warning{font-weight:bold;}表示所有class为warning的元素都加粗`

  `p.warning{font-weight:bold;}表示所有p标签里class为warning的元素都加粗`

- ID选择器：用#+对应id

  `#lead{font-weight:bold;}表示id为lead的元素加粗`

- 属性选择器：

  - 简单属性选择器：选择有某个属性的元素

    `h1[class]{color:red} 表示选择有class属性的所有h1元素，变红`

    `img[alt]{border:3px;}让所有带alt属性的图像border为3px`

  - 根据全部具体属性值选择

    `h1[class="a"]{color:red} 标识选择有class=a属性的所有h1元素，变红`

    部分具体属性

    `h1[class~="a"]{color:red} 标识选择有class=a属性的所有h1元素，变红。即根据属性值中出现的一个用空格分隔的词来完成选择。

- 伪类：根据一些条件所需要应用的样式

  ```
  a:visit{color:red} //表示当A被访问过了以后显示红色
  :link //未被访问过的
  :focus //拥有输入焦点的元素
  :hover //鼠标停留
  :active //用户输入激活的元素
  :first-letter {color:red} //设置首字母样式
  :first-line {color:purple} //设置第一行的样式
  :before/after{color:silver} //设置之前之后元素的样式
  ```

- 小姐：冲突的声明要通过层叠过程排序，由此确定最终的文档表示，过程的核心是选择器及其相关声明的特殊性以及继承机制。


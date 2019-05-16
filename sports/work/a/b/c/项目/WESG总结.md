- 学习使用TMS-Light组件，学习kissy语法

- 建站中台使用，预发正式路径切换

- 加深css熟练度

- 绑定host
  10.*.olympic.alisports.com 
  10.*.cdn.olympic.alisports.com

- 1. 安装环境，DEF tnpm i @al*t -g

     安装light条件 def install @al*t

  2. def lnit light-奥林匹克-打开light页面，def dev

  3. 创建/下载模块

  4. 打开def目录下mod里下载的模块修改，通过模块预览查看修改效果

  5. 修改完成上传，def p -d   dev p -o上传模块

  6. 如果有新的修改，先git checkout -b xxx/0.0.x+1，在发布，-d,-o，然后模块更新，页面升级

  7. 建立页面，配置接口路径

  8. 建立缓存页面，查看线上数据

- 根据控制台，网络请求接受的数据作为mock数据，及时了解接口有没有更新。

- 代码：

  - eval拼接字符串成变量，方便for循环
  - for(let x in aaa)获取对象键名，let x of aaa，获取对象键值，但只能获取具有数字索引的属性

- 需求：三个页面，战队库页面，选手库页面，赛事对阵页面

  - 获取数据，根据字段判断显示内容

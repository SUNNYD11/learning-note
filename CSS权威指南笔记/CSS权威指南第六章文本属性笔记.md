- 缩进文本：text-indent

  ```
  p {text-indent:3em;} //首行缩进
  ```

- 水平对齐：text-align

  right，left，center，justify，只影响元素中的文本

- 垂直对齐

  - 行高：line-height，控制行间距，line-height值和字体大小之差就是行间距，除以二，将行间距的一半分别应用到内容区的顶部和底部。

  - 防止继承父元素的line-height，可以设置缩放因子

    ```
    {line-height:1;}
    ```

  - vertcal-align，只应用于行内元素和替换元素，不能继承。值：baseline、sub、super、top、middle、bottom、text-bottom

  - baseline要求一个元素的基线与其父元素的基线对齐。sub基线低于父元素基线，super高于，但是没有定义降低升高的距离。bottom将元素行内框底端和行框底端对齐。text-bottom指行内文本的底端。middle，通常应用于图像，行内元素框的中点与父元素基线上方四分之一处的一个点对齐。

- 字间隔和字母间隔：word-sapcing、letter-spacing

- 文本转换：text-transform处理大小写。uppercase、lowercase

- 文本装饰：text-decoration，例如underline会对元素加下划线，overline会在顶端画上划线，line-through在文本中间画一个贯穿线。

- 文本阴影：text-shadow，每个阴影都有一个颜色和三个长度值来定义，三个长度分别确定阴影与文本右下偏移值和模糊半径。

- 处理空白符：white-space，对空白符，换行符，是否自动换行进行设置。

- 文本方向：directon，影响块级元素中文本的书写方向，表中列布局的方向，内容水平填充其元素框的方向，两端对齐元素中最后一行的位置。

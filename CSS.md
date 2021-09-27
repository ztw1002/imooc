# CSS

CSS使 **样式和结构分离**

用外链引入样式表：将CSS单独存为.css文件，然后使用`<link>`标签引入它

```html
<link rel="stylesheet" href="css/css.css">
```



## CSS3 选择器

### 标签选择器

直接使用元素的标签名当做选择器，将选择页面上所有该种标签



去掉**小圆点**

```css
ul {
  list-style:none;
}
```



去掉**下划线**

```css
a {
  text-decoration: none;
}
```



### 类名选择器

同一个标签可以同时属于多个类，类名用空格隔开



**原子类**
在做网页项目前，可以将所有的常用自豪、文字颜色、行高、外边距、内边距等都设置为单独的类

```css
.fs12 {
  font-size:12px;
}

.color-red {
  color:red;
}
```

设置好原子类之后，就可以快速添加一些元素样式

```html
<p class="fs18 color-red">
  我是一个文字
</p>
```

### 复合选择器

| 选择器名称 | 示例       | 市例的意义                                |
| ---------- | ---------- | ----------------------------------------- |
| 后代选择器 | .box .spec | 选择类名为box的标签内部的类名为spec的标签 |
| 交集选择器 | li.spec    | 选择既是li标签，也属于spec类的标签        |
| 并集选择器 | ul, ol     | 选择所有 ul 和 ol 标签                    |

#### 后代选择器

使用空格表示”后代“

```css
.box p {
  color: red;
}
```

”后代“并不一定是”儿子“

### 伪类（用户赋予一个元素的状态）

添加到选择器的描述性词语，**指定要选择的元素的特殊状态**，超级链接拥有4个特殊状态

| 伪类      | 意义                                             |
| --------- | ------------------------------------------------ |
| a:link    | 没有被访问的超级链接                             |
| a:visited | 已经被访问过的超级链接                           |
| a:hover   | 正被鼠标悬停的超级链接                           |
| a:active  | 正被激活的超级链接（按下按键但是还没有松开按键） |

a标签的伪类书写顺序： LOVE HATE
link  visited  hover  active

```html
<style>
  a:link {
    color: blue;
  }
  a:visited {
    color: yellow;
  }
</style>

<body>
  <p>
    <a href="http://www.imooc.com">前往慕课网</a>
  </p>
  <p>
    <a href="http://www.jd.com">前往慕课网</a>
  </p>
</body>
```



### 元素关系选择器

| 名称           | 举例   | 意义                          |
| -------------- | ------ | ----------------------------- |
| 子选择器       | div>p  | div的子标签p                  |
| 相邻兄弟选择器 | img+p  | 图片后面紧跟着的段落将被选中  |
| 通用兄弟选择器 | p~span | p元素之后的所有同层级span元素 |

**子选择器**
当使用 > 符号分隔两个元素时，它只会匹配哪些作为第一个元素的直接后代元素，即两个标签为父子关系

```css
.box>p {
  
}
```

后代选择器不一定限制是子元素

```css
.box p {
  
}
```

<img src="https://i.loli.net/2021/09/26/BewjHrSV6YFGv5y.png" alt="image-20210926223011248" style="zoom: 33%;" />

**相邻兄弟选择器**（+）
相邻兄弟选择器（+）介于两个选择器之间，当第二个元素紧跟在第一个元素之后，并且两个元素都是属于同一个父元素的子元素，则第二个元素将被选中

```css
img+span {
  color: red;
}
```



**通用兄弟选择器**（~），a~b  选择  a元素之后的 所有**同层级**b元素 

```css
h3~span {
  font-style: italic;
}
```



### 序号选择器

| 举例                 | 意义                                                |
| -------------------- | --------------------------------------------------- |
| :first-child         | 第一个子元素                                        |
| :last-child          | 最后一个子元素                                      |
| :nth-child(3)        | 第3个子元素                                         |
| :nth-of-type(3)      | 第3个某类型子元素（将选择同种标签指定序号的子元素） |
| :nth-last-child(3)   | 倒数第3个子元素                                     |
| :nth-last-of-type(3) | 倒数第3个某类型子元素                               |

<img src="https://i.loli.net/2021/09/26/Qh1PZF8IJvgGrbE.png" alt="image-20210926230409687" style="zoom:50%;" />

**:nth-child()**
可以写成 **an + b** 的形式，**表示从b开始每a个选一个**，

```css
.box2 p:nth-child(2n+1) {
  color: green;
}
```

<img src="https://i.loli.net/2021/09/26/j4Hq3SurBaKxklZ.png" alt="image-20210926234006040" style="zoom: 50%;" />

### 属性选择器

[alt] 有这个属性
[alt = "北京故宫"] 精准匹配
[alt ^= "abc"] 开头匹配
[alt *= "abc"] 任意位置匹配
[alt |= "abc"] abc-开头
[alt ~= "abc"] abc为空格分开的独立部分

## CSS3 新增伪类

| 伪类      | 意义                                 |
| --------- | ------------------------------------ |
| :empty    | 选择空标签                           |
| :focus    | 选择当前获得焦点的表单元素           |
| :enabled  | 选择当前有效的表单元素               |
| :disabled | 选择当前无效的表单元素               |
| :checked  | 选择当前已经勾选的单选按钮或者复选框 |
| :root     | 选择根元素，即`<html>`标签           |

```css
input:disabled {
  border: 1px solid rgb(17.89,100);
}
```



## 伪元素（新创造出来的元素）

::before 和 ::after

- ::before 创建一个伪元素，其将成为匹配选中的 **元素的第一个子元素**，必须设置 content 属性表示其中的内容

- ::after 创建一个伪元素，其将成为匹配选中的 **元素的最后一个子元素**，必须设置 content 属性表示其中的内容

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    p::after {
      content:"太帅了";
    }
  </style>
</head>
<body>
  <p>
    朱天文
  </p>
</body>
</html> 
```



**::selection**
该伪元素应用于文档中被用户**使用鼠标圈选的部分**

### first-letter 和 ::first-line

- ::first-letter 会选中某元素中（必须是块级元素）第一行的第一个字母

- ::first-line 会选中某元素中（必须是块级元素）**第一行全部文字**

## 层叠性

多个选择器可以同时作用于同一个标签，效果叠加

层叠性的冲突处理：id权重 > class权重 > 标签权重

复杂选择器可以通过（id的个数，class的个数，标签的个数）的形式）计算权重



**!important提升权重**

- 如果我们需要将某个选择器的某条属性提升权重，可以在属性后面写!important

```css
.spec {
  color: blue !important;
}
```



## 常用文本样式属性

### color 属性

可设置文本的前景色（十六进制表示法、rgb表示法、rgba表示法）

```css
.para1 {
  color: #ff3366;
}
```



### font-size 属性

设置字号，单位为px

### font-weight 属性

| 示例                 | 意义     |
| -------------------- | -------- |
| font-weight: normal  | 正常粗细 |
| font-weight: bold    | 加粗     |
| font-weight: lighter | 更细     |
| font-weight: bolder  | 更粗     |

设置斜体： **font-style: italic;**

### text-decoration 属性

| 示例                           | 意义       |
| ------------------------------ | ---------- |
| text-decoration: underline;    | 没有下划线 |
| text-decoration: line-through; | 删除线     |

### font-family 属性（设置字体）

字体可以是列表形式，一般英语字体放到前面，后面的字体是前面字体的”后备“字体

```css
font-family: serif, "Times New Roman", "微软雅黑";
```

### text-indent 属性（定义首行文本内容之前的缩进量）

缩进两个字符：

```css
text-indent: 2em;
```

### line-height 属性

- line-height 属性用于**定义行高**

属性的单位可以是以 px 为单位的数值
也可以是没有单位的数值，**表示字号的倍数（推荐）**
也可以写成百分数，表示字号的倍数



### 单行文本垂直居中

设置  **行高 = 盒子高度**



### 单行文本水平居中

设置 **text-align: center**



## 文本的继承性

只需要给祖先标签设置，即可在后代所有标签中生效

- color
- font- 开头的
- list- 开头的
- text- 开头的
- line- 开头的

文字相关属性有继承性，所以通常**设置body标签的字号、颜色、行高等，这样就能当做整个网页的默认样式了**



### 就近原则

在继承的情况下，选择器权重计算失效，而是”**就近原则**“
继承的标签不如选中的标签权重大



## 盒模型

所有 HTML 标签都可以看成矩形盒子，由width、height、padding、border构成，称为”盒模型“

**padding：内边距**
padding的四数值写法：上右下左

```css
padding: 10px 20px 30px 40px;
```

**margin：外边距**（盒子和其它盒子之间的距离）

margin的塌陷：**竖直方向的margin有塌陷现象**，小的margin会塌陷到大的margin中，从而**margin不叠加，只以大值为准**

盒子的总宽度 = width + 左右padding + 左右border

<img src="https://i.loli.net/2021/09/27/UEgqw5tn9Hj47vN.png" alt="image-20210927192856874" style="zoom:67%;" />



一些元素有默认的margin，在开始制作网页的时候，要将他们清除

```css
* {
  margin: 0;
  padding: 0;
}
```



### 盒子的水平居中

- 将盒子左右两边的 margin 都设置为 auto，盒子将水平居中

```css
.box {
  margin: 0 auto;
}
```

文本居中是 **text-align: center;** 和盒子水平居中是两个概念
文字垂直居中（行高等于盒子高）：line-height: 100px;

**盒子的垂直居中，需要使用绝对定位技术实现**



### box-sizing 属性

将盒子添加 **box-sizing: border-box;** 之后， 盒子的 width、height数字就表示盒子实际占有的宽高（不含margin）了，**即padding、border变为内缩的，不再外扩**

### display 属性

**行内元素和块级元素**

| display属性类型 | 是否能并排显示 | 是否能设置宽高 | 当不设置width尚需经时 | 举例                              |
| --------------- | -------------- | -------------- | --------------------- | --------------------------------- |
| 块级元素        | 否             | 是             | width自动撑满         | div、section、header、h、li、ul等 |
| 行内元素        | 是             | 否             | width自动收缩         | a、span、em、b、u、i等            |



### 行内块

**img** 和 **表单元素**是特殊的 **行内块**，它们既能够设置宽度高度，也能够并排显示



### 行内元素和块级元素的相互转换

- 使用 **display:block;** 即可将元素**转为块级元素**
- 使用 **display:inline-block;** 即可将元素**转为行内块**



### 元素的隐藏

- 使用 **display: none;** 可以将元素隐藏，**元素将彻底放弃位置**
- 使用 **visibility: hidden;** 可以将元素隐藏， 但是**元素不放弃自己的位置**



## 浮动定位于背景样式

### 浮动（最本质功能：实现并排）

- 要设置浮动的话，**并排的盒子都要设置浮动**
- **父盒子要有足够的宽度**，否则子盒子会掉下去



### 浮动的顺序贴靠特性

- 子盒子会按顺序进行贴靠，**如果没有足够控件，则会寻找再前一个兄弟元素**

![image-20210927202456255](https://i.loli.net/2021/09/27/Xd1zpkMKgqPNfc2.png)



### 浮动的元素一定能设置宽高

- **浮动的元素不再区分块级元素、行内元素**，已经脱离文档流，**都可以设置宽度和高度**



### 使用浮动实现网页布局

- 垂直显示的盒子，不要设置浮动，**只有并排显示的盒子才要设置浮动**
- 一个大盒子中，又是一个小天地，内部可以继续使用浮动

### BFC 规范

**块级格式化上下文**，是页面上的一个**隔离的独立容器**，容器里面的子元素不会影响到外面的元素，反之亦然

**一个盒子不设置 height，当内容子元素都浮动时，无法撑起自身**，是因为这个盒子没有形成BFC



### 如何创建 BFC（BFC：块级格式化上下文）

- 1. float 的值不是none
  2. position 的值不是 static 或者 relative
  3. display 的值是 inline-block、flex 或者 inline-flex
  4. overflow:hidden;

### overflow:hidden;    // 溢出将被隐藏，但是盒子的 padding 部分的溢出还在

是非常好用的让盒子形成 BFC 的方法



### BFC 的其他作用

- BFC可以**取消盒子margin塌陷**
- BFC可以**阻止元素被浮动元素覆盖**

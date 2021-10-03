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



## 浮动定位与背景样式

### 浮动（本质功能：实现并排）

- 要设置浮动的话，**并排的盒子都要设置浮动**
- **父盒子要有足够的宽度**，否则子盒子会掉下去

- 不并排的盒子不用写浮动

### 浮动的顺序贴靠特性

- 子盒子会按顺序进行贴靠，**如果没有足够控件，则会寻找再前一个兄弟元素**

<img src="https://i.loli.net/2021/09/28/3TqVWtQXiDsIknY.png" alt="image-20210928095904590" style="zoom:50%;" />

div 属于块级元素，**块级元素天生竖直排列**

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

### overflow:hidden;    // 溢出盒子边框的内容将被隐藏，但是盒子的 padding 部分的溢出还在

是非常好用的**让盒子形成 BFC** 的方法



### BFC 的其他作用

- BFC可以**取消盒子margin塌陷**
- BFC可以**阻止元素被浮动元素覆盖**



### 清除浮动

**浮动一定要封闭到一个盒子中**，否则就会对页面后续元素产生影响

- 清除浮动方法1：**让内部有浮动的父盒子形成BFC**，它就能关闭住内部的浮动，**最好的方法就是overflow:hidden属性**
- 清除浮动方法2：给后面的父盒子**设置 clear:both 属性**，clear 表示清除浮动对自己的影响，both 表示左右浮动都清除
  - 但是margin会失效
- 清除浮动方法3：使用`::after`伪元素给盒子添加最后一个子元素（**一定要转成块元素**），并且给`::after`设置 clear:both
- 清除浮动方法4：在两个父盒子之间“**隔墙**”，隔一个携带 clear:both的盒子



### 相对定位

盒子可以**相对自己原来的位置**进行位置调整

```html
	<style type="text/css">
	* {
		margin: 0;
		padding: 0;
	}
		div {
			width: 400px;
			height: 400px;
			border: 1px solid #000;
			margin: 40px auto;
		}
		p {
			width: 100px;
			height: 100px;
			background-color: orange;
      
			position: relative;
			top: 100px;
			left: 100px;
		}
	</style>
	<body>
		<div id="">
			<p></p>
		</div>
	</body>
```

相对定位有4个描述词，left 向右移动；right 向左移动；top 向下移动；bottom 向上移动，值可以是负数



### 相对定位的性质

会在 **老家留坑，本质上仍然是在原来的位置**，只不过渲染在新的地方而已，渲染的图形可以比喻成**“影子”**，不会对页面其他元素产生任何影响

### 相对定位的用途

- **微调位置**
- 相对定位的元素，可以当做绝对定位的参考盒子

### 绝对定位

盒子可以在浏览器中**以坐标进行位置精确描述**，拥有自己的绝对位置

**位置描述词**：left 到左边的距离；right 到右边的距离；top 到上边的距离； bottom 到下边的距离



### 绝对定位脱离标准文档流

绝对定位的元素将释放自己的位置，对其他元素不会产生任何干扰，而是对他们进行压盖

脱离文档流不会影响后面的任何元素

**脱离文档流的方法**：浮动、绝对定位、固定定位



### 绝对定位的参考盒子

绝对定位的盒子并不是永远以浏览器作为基准点

绝对定位的盒子会以**自己祖先元素中，离自己最近的拥有定位属性点盒子**，当做基准点，这个盒子通常是相对定位的，所以这个性质也叫作**“子绝父相”**



### 绝对定位的盒子垂直居中

```html
position: absolute;
top: 50%;
margin-top: -自己高度一半;
```

如果元素脱离标准文档流，这个元素就不能使用margin实现水平居中



### 堆叠顺序 z-index 属性

- z-index属性是一个没有单位的正整数，数值大的能够压住数值小的

### 绝对定位的用途

- 用来制作“压盖”、“遮罩”效果
- 结合CSS精灵
- 结合JS实现动画



### 固定定位

不管页面如何卷洞，它**永远固定在那里**

```css
position: fixed;
top: 100px;
left: 100px;
```

**注意事项**

- **只能以页面为参考点**，没有子固父相
- 固定定位**脱离标准文档流**

### 总结

使用浮动要注意父盒子要有足够的宽度，

3个定位：相对定位，固定定位，绝对定位



BFC：块级格式化上下文，页面上一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之亦然。

如何创建BFC：

- 只要浮动了就是BFC
- 只要定位不是相对定位或是没定位，就是BFC
- display 的值是 inline-block 或者 flex 或者 inline-flex
- overflow: hidden

BFC的作用：清除浮动、取消盒子的margin塌陷、阻止元素被浮动类元素覆盖



### 绝对定位如何实现垂直居中

```css
top: 50%
margin-top:-自己身高的一半
```



## 边框与圆角

border 属性需要三个要素

```css
border: 1px solid red;
```

solid：实线
dashed：虚线
dotted：点状线

书写小属性可以层叠大属性

四个方向的边框
border-top/right/bottom/left 上/右/下/左边框

### 去掉边框

```css
border-left: none;	/*该属性即可去掉左边框，以此类推
```

transparent：透明色

### 圆角

- **border-radius**属性的值通常为 px 单位，表示圆角的半径
  border-radius 也可以以百分比为单位

  border-radius: 10%;

当border-radius: 50%，则为一个圆或椭圆

### 盒子阴影：box-shadow

![image-20211001153053799](https://i.loli.net/2021/10/01/Ur37IZaFm1HbVw4.png)

<img src="https://i.loli.net/2021/10/01/cGLjmoAT7wr4UIa.png" alt="image-20211001160556759" style="zoom: 50%;" />

### background-color 属性

padding 区域是有背景颜色的

### background-image 属性

用来设置背景图片，图片路径要写到 **url() 圆括号中**
如果样式表示外链的，那么要**书写从CSS出发到图片的路径**

### backgournd-repeat 属性

 <img src="https://i.loli.net/2021/10/01/vPa4ud7q2grSFLf.png" alt="image-20211001220158969" style="zoom: 33%;" />

背景透明的图片会把网页的背景当做自己的背景，解决方法：

```css
background: white url(images/archer.png);
```

### background-size 属性（用来设置背景图片的尺寸）

```css
background-size: 100px 200px;
```

值也可以用百分数来设置，表示为盒子宽、高的百分之多少

需要**等比例设置的值，写auto**



**contain 和 cover**

- contain 看完整
- cover 不留白

### background-clip 属性

### （设置元素的背景裁切到哪个盒子）

| 值          | 意义                          |
| ----------- | ----------------------------- |
| border-box  | 背景延伸至边框（默认值）      |
| padding-box | 背景延伸至**内边**（padding） |
| content-box | 背景被裁剪至**内容区**        |

### background-attachment（背景固定）

决定背景图像的位置是在视口内固定，或者随着包含它的区块滚动

| 值     | 意义                                   |
| ------ | -------------------------------------- |
| fixed  | 自己滚动条不动，外部滚动条不动         |
| local  | 自己滚动条动，外部滚动条动             |
| scroll | 自己滚动条不动，外部滚动条动（默认值） |

### background-position属性

### （可以设置背景图片出现在盒子的什么位置）

```css
background-position: 100px 200px;

background-position: top right;
```

可以用top、bottom、center、left、right描述图片出现的位置

**background一些常用的背景相关小属性，可以合写到一条background属性中**

### 线性渐变（属于 背景图片属性 管理）

![image-20211001232834489](https://i.loli.net/2021/10/01/OHJim6WuqQrIfwC.png)

可以有多个颜色值，并且可以用百分数定义它们出现的位置

```css
background-image: linear-gradient(to bottom, blue, yellow 20%, red);

background-image: linear-gradient(45deg, red, blue);
```

### 浏览器私有前缀

| 品牌    | 前缀     |
| ------- | -------- |
| chrome  | -webkit- |
| firefox | -moz-    |
| ie/edge | -ms-     |
| 欧朋    | -o-      |



### 径向渐变（圆形）

```css
background-image:radial-gradient(50% 50%, red, blue);
															 /* 圆心坐标 (实际工作用得不多）*/
```



### 总结：background系列属性

background-color
background-image
background-repeat
background-position（可以实现CSS精灵）
background-size
background-clip（背景裁切）
background-attachment（背景固定）



实现渐变背景

```css
background-image: linear-gradient(to bottom, blue, yellow 20%, red);
```



## 2D 与 3D

### 旋转变形

- 将 transform 属性的值设置为rotate()，即可实现旋转变形

```css
transform: rotate(45deg);
								
```

```css
.pic1 {
  transform: rotate(45deg);
  								/*旋转角度，角度为正则为顺时针*/
}
```

### transform-origin属性

可以使用 transform-origin 属性设置自己的**自定义变换原点**

```css
.pic6 {
  /*以左上角为中心店进行旋转*/
  transform-origin: 0 0;
  transform: rotate(3odeg);
}
```

### transform-scale 缩放变形

```css
transform: scale(3);
						 /*缩放倍数*/
```

当数值小于1时，表示缩小元素，大于1表示放大元素

### 位移变形

将transform属性的值设置为translate()，即可实现位移变形

```css
transform: translate(100px, 200px);
									/*向右移动 向下移动*/
```

位移变形会**老家留坑**，**形影分离**



### 3D 旋转

**将transform属性的值设置为 rotateX() 或者 rotateY()，即可实现绕横轴、纵轴旋转**

```css
transform: rotateX(30deg);
transform: rotateY(30deg);
```

**perspective属性**：用来定义**透视强度**，可以理解为“人眼到舞台的距离”，单位px

<img src="https://i.loli.net/2021/10/02/LIwTGmN4vaqhO89.png" alt="image-20211002130254708" style="zoom:50%;" />

```css
.box1 {
  width: 202px;
  height: 202px;
  border: 1px solid #000
  margin: 50px auto;
  perspective: 300px;
}
.box1 p {
  transform: rotateX(30deg);
}
```

### 空间移动

当元素进行3D旋转后，即可**继续添加** translateX()、translateY()、translateZ()属性**让元素在空间进行移动**



**空间移动要添加在3D旋转之后**

```css
transform: rotateX(30deg) translateX(30px) translateZ(100px);
```



**制作一个正方体**

正方体的每个面都是从舞台经过不同的3D旋转、空间移动到自己的位置



## 动画

### transition过渡

过渡可以为一个元素在不同样式之间变化自动添加“补间动画”
定义**开始状态** -> 定义**结束状态**

transition属性有4个要素

![image-20211002133057598](https://i.loli.net/2021/10/02/2tCOc3P9oKugETs.png)

```css
.box1 {
  width: 200px;
  height: 200px;
  background-color: orange;
  transition: width 5s linear 0s;
}
.box1:hover {
  width:800px;
}
```

### 哪些属性可以参与过渡

- 所有数值类型的属性，都可以参与过渡，比如width、height、left、top、border-radius

- 背景颜色和文字颜色都可以被过渡
- 所有变形（包括2D和3D）都能被过渡

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<style type="text/css">
		.box1 p {
			position: relative;
			width: 200px;
			height: 200px;
			background-color: orange;
			transition: left 1s linear 0s;
			left: 0;
		}
		.box1 :hover p{
      /*
      如果此处是 .box1 p:hover {
        ...
      }
      则会出现鼠标必须跟随方框移动，才能使得方块正常移动的行为，否则方块会滞留在鼠标的位置来回抖动*/
			left: 1000px;
		}
	</style>
	<body>
		<div class="box1">
			<p></p>
		</div>
	</body>
</html>
```

如果要所有属性都参与过渡，可以写all

```css
transition: all 1s linear 0s;
```

transition的第三个参数就是变化速度曲线

浮动是实现并排的，绝对定位是实现压盖的

### 动画定义

使用 **@keyframes 来定义动画**，keyframe表示关键帧
项目上线前，要补上@-webkit-这样的私有前缀

<img src="https://i.loli.net/2021/10/03/kJOuoMsjzqKL9Sr.png" alt="image-20211003105318642" style="zoom:50%;" />

### 动画的调用

使用 animation 属性调用动画

<img src="https://i.loli.net/2021/10/03/9tdhDVQzpHjyk43.png" alt="image-20211003105455478" style="zoom: 50%;" />

第五个参数就是**动画的执行次数**，次数写 infinate 则永远执行

### alertnate 和 forwards

alertnate：（偶数次）自动逆向执行
forwards：停止在最后结束状态

### 多关键帧动画

```css
@keyframes changeColor {
  0% {
    background-color: red;
  }
  20% {
    background=color: yellow;
  }
  40% {
    background-color: blue;
  }
  60% {
    background-color: green;
  }
  80% {
    background-color: purple;
  }
  100% {
    background-color: orange;
  }
}
```


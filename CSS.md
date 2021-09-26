# CSS

CSS使 **样式和结构分离**

用外链引入样式表：将CSS单独存为.css文件，然后使用`<link>`标签引入它

```html
<link rel="stylesheet" href="css/css.css">
```



## CSS3 选择器

### 标签选择器

直接使用元素的标签名当做选择器，将选择页面上所有该种标签



去掉小圆点

```css
ul {
  list-style:none;
}
```



去掉下划线

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

### 伪类

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

![image-20210926234006040](https://i.loli.net/2021/09/26/j4Hq3SurBaKxklZ.png)

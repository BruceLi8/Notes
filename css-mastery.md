# CSS Mastery

## 一、基础

基础不牢，地动山摇。

### 结构化的代码

可维护性或许是代码最重要的特征。如果代码失去结构，那么将难以阅读，随之带来很多困难：修改Bug, 优化性能。编写易于阅读的代码是很重要的，特别是代码的内容，易于修改以满足未来需求。

#### 关注点分离：“Small pieces, loosely joined".小块：一个小模块的代码只做意见事。由于对其他组件松耦合，那么这些模块可以容易地被其他模块重用。这些小块就像乐高积木，每一块都很简单，但是却能够以许多方式组合在一起形成高度复杂的物件。

渐进式增强：用以平衡最新的HTML和CSS特性的向后兼容性。

```markup
<input type="text" id="field-email" name="field-email">
```

```markup
<input type="email" id="field-email" name="field-email">
```

如果某个浏览器没有实现新的字段类型, 如type="email"，那么将会回退到默认值，如type="text"。能够解析新字段类型的浏览器，将能够按照预期地工作。

CSS属性地渐进式增强：

```css
.overlay {
    background-color: #000;
    background-color: rgba(0, 0, 0, 0.8);
}
```

#### 厂商前缀：

```css
.myThing {
    -webkit-transform: translate(0, 10px);
    -moz-transform: translate(0, 10px);
    -ms-transform: translate(0, 10px);
    transform: translate(0, 10px);
}
```

-webkit开头的属性作用于基于WebKit的浏览器，如Safari。对于Chrome和Opera则是基于Blink引擎的，其最初是基于WetKit的，所以-webkit前缀通常也能在这两款浏览器上正常工作。

-moz开头的属性作用于Firefox.

-ms开头的属性作用于IE.

#### 条件规则和探测脚本：

```css
@supports (display: grid) {
    /* rules for when grid layout is supported go here */
}
```

问题在于：这条规则自身比较新，所以我们只对没有被任何古老浏览器实现的前沿特性使用它，例如grid布局。对于其他情况，我们可以使用JS检测。

### 创建结构化和语义化丰富的HTML

语义化的标记是好的HTML文本的基础。

有意义的元素：

1. h1, h2, ...
2. p, ul, ol, dl
3. stong, em
4. blockquote, cite
5. pre, code
6. time, figcaption, caption

同样也包含对form和table有基础样式的相关元素，比如

1. fieldset, legend, label
2. caption, thead, tbody, tfoot

#### Class和ID属性

命名是编写代码中，最重要的部分之一。选一个名字能够说明是什么，暗示其意图、其应该的样子。所以清晰，明确的名字是重要的。

即使我们为了样式化添加一个class名作为一个明确的hook, 但是我们应该避免使用名字表明其视觉上的效果。换句话说，我们应该选择一个**表明组件是什么类型的名字。**

#### **结构化的元素**

section, header, footer, nav, artile, aside, main

引入这些元素是为了创建HTML的逻辑部分。可以使用他们来表示包含独立区域的部分（article），导航组件（nav）, 特定部分的头部（header）。

```markup
<article class="post">
    <header class="post-header">
        <h1>How I became a CSS Master</h1>
    </header>
</article>
```

```css
.post {
    /* styles here */
}
.post-header {
    /* other styles here */
}
```

从语义化的文档中，解耦出样式，使得其更轻便，目的更明确，从而提高可维护性。

使用Div和Span

当没有更合适的语义化元素满足目的时，div是一个合适的元素。

"divitis": 倾向于堆砌div，或者不管有更适合的元素，对任何内容都使用div。只在有必要提供简单清晰的样式钩子是使用div，但是不要觉得使用div就是一种不好的事情。

#### 文本表述文本元素，重新定义

&lt;b&gt;和&lt;i&gt;元素是历史残留。应该使用有语义的&lt;em&gt;或&lt;strong&gt;。

#### ARIA Role属性

landmark role属性：

* navigation
* banner
* form
* main
* search
* complementary
* contentinfo
* application

[http://www.w3.org/TR/wai-aria/roles\#role\_definitions](%20%20%20http://www.w3.org/TR/wai-aria/roles#role_definitions)

{% embed url="http://blog.paciellogroup.com/2013/02/using-wai-aria-landmarks-2013/" %}

#### Validatio

HTML: [http://validator.w3.org/](%20%20%20http://validator.w3.org/)

#### 开发者插件[   http://chrispederick.com/work/web-developer/](%20%20%20http://chrispederick.com/work/web-developer/)

css:[   http://jigsaw.w3.org/css-validator/](%20%20%20http://jigsaw.w3.org/css-validator/)

## 二、获取样式目标节点

### CSS选择器

Type selectors\(Element selectors\)：用于获取特定类型的元素。

```css
p {
    color: black;
}
```

后代选择器：获取一个元素或一组元素的后代。通过两个其他的选择器之间加一个空格使用后代选择器。

```css
blockquote p {
    padding-left: 2em;
}
```

ID选择器和类选择器：ID选择器使用hash字符区分，类选择器使用句号区分。

```css
#intro {
    font-weight: bold;
}
.date-posted {
    color: #ccc;
}
```

孩子选择器和兄弟选择器：孩子选择器只选择元素的直接后代（孩子）。相邻兄弟选择器选择在邻接另一个元素后面，并且有共同双亲的元素。

```css
#nav > li {
    background: url(folder.png) no-repeat left top;
}
h2 + p {
    font-size: 1.4em;
    font-weight: bold;
    color: #777;
}
```

兄弟选择器：

```css
h2 ~ p {
    font-size: 1.4rem;
    font-weight: bold;
    color: #777;
}
```

注：相邻兄弟选择器和兄弟选择器不能选中之前的兄弟。

通用选择器：匹配所有元素。

```css
* {
    padding: 0;
    margin: 0;
}
```

这样通常有一些未预料的情况，特别是格式化了表单的UI元素，例如button和select。更好的做法是显式地写出元素：

```css
h1, h2, h3, h4, h5, h6,
ul, ol, li, dl, p {
    padding: 0;
    margin: 0;
}
```

一些处理这个问题的库：

Eric Meyer’s CSS Reset \( [http://meyerweb.com/eric/tools/css/reset/](http://meyerweb.com/eric/tools/css/reset/) \) and 

Nicolas Gallagher’s Normalize.css \( [http://necolas.github.com/normalize.css/](http://necolas.github.com/normalize.css/)

后者选择了一种有些不同的方法：Normalize确保了所有元素在不同浏览器上有一致的样式，而不是将margin和padding重置到0。

属性选择器：

```css
abbr[title]:hover {
    cursor: help;
}

input[type="submit"] {
    cursor: pointer;
}

a[href^="http:"] {}
img[src$=.jpg"] {}
a[href*="/about/"] {}

a[rel~=next] {} /* 匹配空格分隔的字符串列表 */
a[hreflang|=en] /* 匹配以这个值开头，或等于这个值、这个值后跟-, 例如en, en-US */
```

伪元素：有时想要获取的目标不代表一个元素，但是不像写额外的标记。对于大多数常见的情况，CSS提供了一些方法处理这种情况。

::first-letter, ::fitst-line获取第一个字符，第一行

::befor, ::after代表一块内容开头和结束假设的元素。这对插入一下字符和排版装饰很有用。

伪类：有时想要获取一个目标元素，其基于文档结构外的一些东西。例如，超链接的状态或表单元素。

伪类选择器的顺序很重要：a:link, a:visited, a:hover, a:focus, a:active.

否定选择器：

```css
.comment:target:not(.comment-downvoted) {
    background-color: #fffec3;
}
```

结构性伪类：

第n个孩子选择器：

```css
tr:nth-child(odd) {
    background: yellow;
}

tr:nth-child(3n+4) {
}

tr:nth-last-child(N) {}

tr:nth-of-type(N) {}
tr:nth-last-of-type(N) {}
```

结构化伪类的妙用：

```css
/* 有四个column的第一个column */
.column:nth-last-of-type(4):first-child {}

/* 其余column */
.column:nth-last-of-type(4):first-child ~ .column {
    /* Rules for when there is exactly four .column elements */
}
```

### 层叠

重要性顺序：

1. 用户标记!important的样式
2. 作者标记!important的样式
3. 作者样式
4. 用户样式
5. 浏览器或user agent的样式



### 特殊性

1. 内敛样式，a等于1
2. b等于ID选择器的总数
3. c等于class，伪类，属性选择器的总数
4. d等于类型选择器，伪元素选择器的总数

### 继承

对某些属性，比如color或font size,为某个元素的所有子元素都添加该属性。继承的样式没有特殊性。

通过通用选择器设置的属性值，特殊性是0，将覆盖继承的属性值。

### 将样式应用到文档

link和style标签

```markup
<style>
    @import url("/c/modules.css")
</style>
```

import可用于HTML中的head style块，或包含在外部样式表中。后者会导致浏览器加载后续的CSS文件。

当元素上有多个相同特殊性的相同属性时，最后声明的获胜。

性能

现代浏览器至少需要两个东西开始渲染：HTML和CSS。应该尽快下载在HTML和**所有**CSS文件。

减少HTTP请求

总是保持CSS的文件数量是一个或两个。避免使用@import。

压缩和缓存内容

CSS压缩可能减少60%-80%的文件大小，从而可以减少带宽，减少加载时间。

避免出现阻塞渲染的JavaScript

传统做法：在body的结束标签的前面，加载script

现代做法：在head中的script标签上添加async和defer属性。

defer: 异步加载，在下载完成后立即执行。

async: 异步下载，等待HTML加载完成后执行。

## 视觉格式化模型

有一些很重要但是却难懂的CSS概念：浮动、定位、盒模型。这些概念控制着元素在页面上组织展示的形式，形成了很多布局方案的基础。

### 盒模型

页面上的每个元素都可以视为由元素内容、内边距、边框、外边距组成。

如果为元素添加背景，那么背景将作用于内容区域盒内边距。通常，内边距用于创建一个内容周围的一个槽（gutter）,从而使内容不与背景边界平齐。外边距是盒子的可视化区域外部透明的空间，使得我们可以控制元素间的距离。

outline： 不影响布局；outline在元素的border外画一条线。其不影响盒子的宽度和高度，所以在debug负载的布局或演示布局效果的时候很有用。

#### box-sizing

在默认情况下，盒子的宽度和高度指的是内容区域（content）的宽度和高度。content区域矩形由元素渲染内容的边界组成。添加边框和内边距不会影响content box的尺寸，但是会增加元素的总体尺寸。

box-sizing的默认值是content-box。有时候，让width和height不只是作用于content box是很有用的，特别是在响应式布局中。

如果把box-sizing属性值设置为border-box，那么宽度和高度将会包含padding和border的空间。

margin可设置为负值，从而可以用于推拉元素在页面上的位置。

百分比margin：宽度为占父元素的width百分比值。上下的margin和padding则不一样。此时，父元素的高度还未声明。CSS规范指出：上下margin和padding的值，由containter block的宽度得出。

### 视觉格式化模型

display: block, inline, none

positioning models: floats, absolute positioning, relative positioning.除非指定，所有盒子在正常流中被定位，有默认属性static。如同名字那样，在正常流中一个盒子的位置由元素在HTML中的位置确定。

块级盒子在垂直方向一次显示，盒子间的垂直距离由盒子垂直margin决定。

内联盒子被水平放置在行内，沿着文本方向，当文本换行时，换到新的一行。其水平间距可以通过使用水平内边距，边框，外边距调整。然而，垂直的内边距，边框，外边距不会对内联盒子的高度产生影响。

形成一行文本的水平盒子被称为行盒子（line box），调整行盒子的尺寸的唯一方式是改变行高，或设置内部的水平边框，内边距，外边距。

当使用table元素时，table表现得为block，table内部根据生成得行与列排列。也可以通过设置display: table, table-row, table-cell，实现HTML中的表格，而不使用table标记。

#### 匿名盒子

```markup
<section>
    some text
    <p>Some more text</p>
</section>
```

some text会形成匿名块盒子。

#### 外边距合并

上下外边距合并，内外盒子的外边距合并，无内容元素上下外边距合并。

这就是为什么空白段落元素站住很小空间的原因：所有margin合并在一起组成了一个小的外边距。


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







\*\*\*\*


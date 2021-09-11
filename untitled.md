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


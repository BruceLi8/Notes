# Webpack实战

## 一、Webpack简介

        webpack核心功能： 解决模块间依赖，将各个模块按照特定的规则和顺序组织在一起，最终形成一个或多个JS文件。这个过程称为模块打包。

模块化的优点：

1. 通过导入和导出语句可以清晰地看到模块间的依赖关系。
2. 模块可以借助工具打包，在页面中只需要加载合并后的资源文件，减少了网络开销。
3. 多个模块之间作用于隔离，不会有命名冲突。

### 模块打包工具\(module bundler\)

工作方式分为两种：

1. 将存在依赖关系的模块按照特定规则合并为单个JS文件，一次全部加在进页面中。
2. 在页面初始化时加在一个入口模块，其他模块异步地进行加载。

#### npm scripts: scripts 是npm提供的脚本命令功能，可以在script中直接使用模块所添加的指令（比如： 用“webpack"取代之前的"npx webapck"）

output.path要求使用绝对路径

        项目上线是安装依赖，可通过npm install --production过滤掉DevDependencies中的冗余模块，加快安装和发布的速度。



## 二、模块打包

### CommonJS

        CommonJS是JavaScript社区于2009年提出的一系列标准。Node.js的实现中采用了CommonJS标准中的一部分，并在其基础上进行了一系列调整。一般谈到CommonJS其实是Node.js中的版本，而非它的原始定义。

script标签引入JavaScript文件与CommonJS模块的区别：

script标签的顶层作用域是全局作用域，进行变量及函数声明时会污染全局作用域；

CommonJS模块会形成一个属于模块自身的作用域。

#### 模块导出的两种方式：

1.module.exports

```javascript
module.exports = {
    name: 'calculator',
    add: function (a, b) {
        return a + b;
    }
}
```

2. exports.属性

```javascript
exports.name = 'calculator';
exports.add = function (a, b) {
    return a + b;
}
```

内在机制：将exports指向module.exports, 并且module.exports在初始化时是一个空对象。

注意：

1. 这种方式不能给exports赋值，否则会导致其失效。
2. 两种方式不要混用。
3. 导出语句不代表模块的结尾。在module.exports或exports后的代码依旧会执行。

#### 模块导入：

1. require的模块第一次被加载。此时会首先执行该模块，然后导出内容。
2. require的模块曾经被加载过。此时模块内代码不会再次执行 ，而是直接导出上次执行后得到的结果。

        如果我们加载一个模块，不需要获取其导出的内容，只是想通过执行它而产生模中作用，此时直接使用require即可。

        require可以接收表达式，从而可以动态指定模块的加载路径。

### ES6 Module

        每个文件作为一个模块，每个模块拥有自身的作用域。import和export作为保留关键字，在ES6中加入。

        ES6 Module会自动采用**严格模式**

#### **模块导出**

**1.命名导出**

```javascript
// 写法1
export const name = 'calculator';
export const add = function(a, b) { return a + b; }

// 写法2
const name = 'calculator';
const add = function (a, b) { return a + b; }

export { name, add }
```

使用命名导出时，可通过as关键字对变量重命名。

```javascript
const name = 'calculator';
const add = function (a, b) { return a + b; }

export { name, add as getSum }
```

2.默认导出

#### 模块导入

1. 命名导入：对应命名导出的模块，同时也可使用as对导入变量重命名。
2. 导入多个变量时，可以使用整体导入，减少对当前作用域的影响。import \* as &lt;myModule&gt;
3. 对默认导入，变量名可以自由指定。

#### 重导出

```javascript
export { name, add } from './calculator.js';
```

### CommonJS 与ES Module的区别

#### 动态与静态：

CommonJS对模块依赖的解决是动态的：模块依赖的建立发生在代码的运行阶段；

ES6 Module对模块依赖的解决是静态的： 模块依赖的建立发生在代码的编译阶段；

ES6 Module相比CommonJS具有的优势：

1. 死代码检测和排除
2. 模块变量类型检查。有助于确保模块之间传递的值或接口类型的正确。
3. 编译器优化。CommonJS传递的是对象，ES6 Module支持直接导入变量，减少引用层级。

#### 值拷贝与动态映射：

CommonJS获取的是一份导出值的拷贝。对导入值的修改操作不会影响导出模块。

ES6 Module中获取的是值的动态映射，且这个值是动态只读的。

#### 循环依赖：

CommonJS中，若遇到循环依赖，我们没有办法得到预想中的效果。

```javascript
// The require function
function __webpack_requrie__(moduleId) {
    if(installedModules(moduleId) {
        return installedModules[moduleId].exports;
    }
    // Create a new module (and put it into the cache)
    var module = installedModules[moduleId] = {
        i: moudleId,
        l: false,
        exports: {}
    };
    ...
}
```

代码解释：循环引用中，再次引用时，直接从installedModules里面取值，此时module.exports是空对象。                      

ES Module中，由于动态映射的特性，循环依赖在在返回时，值从undefined变化为已定义的值，从而解决了循环依赖。

####                                                                                       


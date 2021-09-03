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



​










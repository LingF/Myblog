title: PostCSS初探
date: 2015-12-25 09:59:05
tags: [PostCSS, 提升]
---

## PostCSS
### 她是什么？

#### 介绍
![PostCSS Logo](/uploads/2/00.png)

看着logo，怎么有种教会的感觉。通过[postcss/postcss·GitHub](https://github.com/postcss/postcss)介绍的第一句`PostCSS is a tool for transforming styles with JS plugins`得知，她就是一个借助js插件转换样式的工具。

#### 她的原理
当然，实际上她并不像介绍的那么简单。

> PostCSS自身包括 `css分析器`，`css节点树API`，`source map生成器` 以及 `css节点树拼接器` 4部分。

css的组成单元是一条一条的样式规则（rule），每一条样式规则又包含一个或多个属性&值的定义。所以，PostCSS的执行过程是，先 `css分析器` 读取css字符内容，得到一个完整的节点树，接下来，对该节点树进行一系列转换操作（基于 `节点树API` 的插件），最后，由 `css节点树拼接器` 将转换后的节点树重新组成css字符。期间可生成 `source map` 表明转换前后的字符对应关系：

[![PostCSS原理](/uploads/2/0.png)](http://ai.github.io/about-postcss/en/?full#22)

---

### 先看一个例子

#### 平时码的代码，或者依靠Sublime Text插件生成的css3

![示例1](/uploads/2/1.png)

#### 这里的问题？
一时看不出问题？那先不急，我们先来看看 transition [属性支持](http://caniuse.com/#search=transition)的情况：
![示例2](/uploads/2/2.png)
我们可以得到一些特殊的情况：IE >= 10支持 / Firefox8 需要-moz-前缀 / Android Browser 4.1、4.3都需要-webkit-前缀

说到这里我们就想，啥啥啥？-ms-，-o-，这些前缀去哪了？这图会不会不准额！拿浏览器测一下就知道，当然我还是挺信任 [CanIUse.com](http://caniuse.com) 的数据的。例如IE，别说前缀了，压根IE9就不支持，IE10+都直接支持无需前缀。

> 现在终于知道示例1的代码问题了，就是多了很多不必要的浏览器前缀支持，造成了css的冗余，这是很揪心的。。。

#### 如何解决呢？PostCss出场了~

当我们用上她，开发时可以这样码css:

![示例3](/uploads/2/3.png)

通过PostCSS处理过后：

![示例4](/uploads/2/4.png)

> [transform](http://caniuse.com/#search=transform)是需要-ms-前缀的，她就自动加上了，是不是省时又省心。不仅减少输入的代码量，并且根据情况生成所需的前缀，除去了css冗余，代码漂亮了效率也杠杠滴。

然而PostCSS并不会自己去进行这种转换(从原理中得知)，这里自动添加浏览器前缀实质上是[Autoprefixer](https://github.com/postcss/autoprefixer)插件来处理，而Autoprefixer则是PostCSS的最流行插件之一。

---

### 插件库
这里只列出了尝试过的部分插件：

| 插件名 | 作用 | 备注 |
| ------------- |:-------------:| -----:|
| [autoprefixer](https://github.com/postcss/autoprefixer) | 自动添加浏览器前缀 | 可指定支持的浏览器版本 |
| [alias](https://github.com/seaneking/postcss-alias) | 定义自己的css属性别名规则 | [PostCSS Crip](https://github.com/johnie/postcss-crip)定义了大量简写，可参考  |
| [font-magician](https://github.com/jonathantneal/postcss-font-magician) | 自动引入自定义字体 | 引用字体的地址改成本地地址还是可以拿来用的 |
| [center](https://github.com/jedmao/postcss-center) | 水平居中/垂直居中 | css痛点 |
| [will-change](https://github.com/postcss/postcss-will-change) | 使用backface-visibility迫使浏览器创建一个新层 | 支持则使用，不支持亦无损耗 |
| [color-rgba-fallback](https://github.com/postcss/postcss-color-rgba-fallback) | 添加一个十六进制颜色作为降级处理 | 为了兼容 <= IE8 |
| [import](https://github.com/postcss/postcss-import) | @import内联合并成一个文件 | 自动发现bower_components或node_modules的CSS文件位置 |
| [css mqpacker](https://github.com/hail2u/node-css-mqpacker) | 合并相同的媒体查询 | |
| [precss](https://github.com/jonathantneal/precss) | `插件包` | 让你像sass一样书写css |
| [cssnano](http://cssnano.co/optimisations/) | `插件包` |  |
| [cssgrace](https://github.com/cssdream/cssgrace) | `综合类插件` |  作者'一丝' |

> 官方提供的插件列表和目录 [plugins list](https://github.com/postcss/postcss/blob/master/docs/plugins.md) / [searchable catalog](http://postcss.parts/)

---

### PreCSS
#### 这又是什么？
上面说的增加浏览器前缀等等都是后处理css的方式，当然PostCSS不仅仅能后处理，她也能做预处理的事。PreCSS这个插件包整合了一些预处理插件，让我们可以像使用sass那样的预处理器一样书写css。

> PreCSS做了一个表率，当然，我们也能构建我们自己的预处理器，扩展想要的特性只要增加相应的插件就能实现。这也是我认为PostCSS比单单用sass来的灵活的地方。

---

### 未完待续...





---
title: 优先级 和 CSS 预处理
date: 2018-12-20 22:30:16
tags:
---
## 前言扯淡
前两天电话面试，被问道了一些 CSS 的基础问题，虽然答上来了，但是不够全面，而且给自己最大的感受是自己对一些概念十分模棱两可，最直观的体现是有时候知道这个概念，却不知道他叫什么。自以为懂，最为致命。
需求是最好的学习API的方式，面试找工作是最好的学习沉淀的过程。快俩个月没写博客了，终于今天在回顾时有一点点小的感悟，打算记录下来，主要是给自己看。废话不多说，开始正文。
## 首先是 [优先级](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Specificity)
链接是文档，优先级主要是指CSS属性的优先级。
>浏览器通过优先级来判断哪一些属性值与一个元素最为相关，从而在该元素上应用这些属性值。优先级是基于不同种类选择器组成的匹配规则。

简单来说，当你给一个元素声明（或该元素继承而来）多个相同属性时（前提），浏览器选择哪一个作为该元素的应用。
```
<div>
  <h1 id="title" class="title" style="color: yellow;">优先级</h1>
</div>
<!--优先级显示为 pink-->
```
```
*{
  color: red;
}

h1{
  color: green;
}

.title{
  color: blue;
}

#title{
  color: black;
}

h1{
  color: pink !important;
}
```
#### 优先级如何确定：
选择器优先级，下面三种优先级递增：（不细看文档都不知道这些平时在用的选择器的所有名称）
1. **ID选择器**（例如, #title）
2. **类选择器**（class selectors） (例如,.title)，**属性选择器**（attributes selectors）（例如, [type="radio"]），**伪类**（pseudo-classes）（例如, :hover）
3. **类型选择器**（type selectors）（例如, h1）和 **伪元素**（pseudo-elements）（例如, ::before）

**通配选择符**（universal selector）(\*), **关系选择符**（combinators） (+, >, ~, ' ')  和 **否定伪类**（negation pseudo-class）(:not()) 对优先级没有影响。（但是，在 :not() 内部声明的选择器是会影响优先级）。
给元素添加的**内联样式**  (例如, style="color: yellow;") 总会覆盖外部样式表的任何样式 ，因此可看作是具有最高的优先级。
**!important** 是例外，此声明将覆盖任何其他声明，技术上!important与优先级无关，但它与它直接相关。
#### 如何利用优先级
1. 选择器越具体，优先级越高。
2. 相同优先级情况下，后面的样式覆盖前面的。
3. !important 最特殊，有他的声明最优先，但应该避免使用。

上面内容均来自 MDN，也就是我给的链接，还有很多如`无视DOM树中的距离`等没有记录。大家还是直接看MDN为宜。这些真的是简单的基础内容，但确实有很多细节，如果能够因为无意看到我的文章去看MDN文档而收获一些东西，便是此文的意义了。
扩展阅读 [真正理解"CSS选择器的优先级"](https://github.com/jincdream/jincdream.github.io/issues/14)
## CSS预处理（预编译）
当面试关问我知不知道CSS预处理的时候，我一时并没有将其与平常再用的 LESS、SCSS 等预编译器对上。也就是我文章开头提到的，有时我们以为熟知的东西，事实上我们那么陌生。

---
(以下内容来自 [再谈 CSS 预处理器](http://efe.baidu.com/blog/revisiting-css-preprocessors/))
CSS 预处理器是什么？一般来说，它们基于 CSS 扩展了一套属于自己的 DSL，来解决我们书写 CSS 时难以解决的问题：
- 语法不够强大，比如无法嵌套书写导致模块化开发中需要书写很多重复的选择器；
- 没有变量和合理的样式复用机制，使得逻辑上相关的属性值必须以字面量的形式重复输出，导致难以维护。

所以这就决定了 CSS 预处理器的主要目标：提供 CSS 缺失的样式层复用机制、减少冗余代码，提高样式代码的可维护性。

---
这篇文章不打算继续将 LESS、SASS 等的嵌套、变量等语法规则。一来这些内容非一篇文章讲得清（我懒），再者看官方文档是最好的入门方式，同时像上面百度EFE的文档比我写肯定高到不知道哪里去了。
那么我为什么会将 CSS 预处理和 优先级 放在同一篇文章写呢。也是面试官连续问的这俩个问题（真的很基础了，对我这种转行前端新人十分照顾），再者其实两者有一些联系，CSS 预编译也是在变相解决 优先级 的问题，因为我们需要完美利用优先级，所以我们在写 CSS 时往往选择器需要十分详细，如下
```
div{}
div>ul{}
div>ul>li{}
div>ul>li>a{}
```
本着 Dry 宗旨，CSS 预编译的嵌套规则就是为了解决优先级啊。

---
本文仅供个人学习使用
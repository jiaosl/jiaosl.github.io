---
title: '你知道MVC,MVP和MVVM之间的故事吗?'
date: 2017-05-15 22:19:49
tags: [MVVM, MVC,　MVP]
categories: javaScript
---


## MVC
MVC全名是Model View Controller，是模型(model)－视图(view)－控制器(controller)的缩写，一种软件设计典范，用一种业务逻辑、数据、界面显示分离的方法组织代码，将业务逻辑聚集到一个部件里面，在改进和个性化定制界面及用户交互的同时，不需要重新编写业务逻辑。MVC被独特的发展起来用于映射传统的输入、处理和输出功能在一个逻辑的图形化用户界面的结构中。

![MVC](http://upload-images.jianshu.io/upload_images/1969397-5fa6f0a2f5c42267.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<!-- more -->
**MVC优点：**

>
1. 业务逻辑全部分离到Controller中，模块化程度高。当业务逻辑变更的时候,只需要Controller换成另外一个Controller就行了（Swappable Controller）。
2. 观察者模式可以做到多视图同时更新。

**MVC缺点:**

>1. Controller测试困难。因为视图同步操作是由View自己执行，而View只能在有UI的环境下运行。在没有UI环境下对Controller进行单元测试的时候，Controller业务逻辑的正确性是无法验证的：Controller更新Model的时候，无法对View的更新操作进行断言。
2. View无法组件化。View是强依赖特定的Model的，如果需要把这个View抽出来作为一个另外一个应用程序可复用的组件就困难了。因为不同程序的的Domain Model是不一样的


![向下发展到MVP](http://upload-images.jianshu.io/upload_images/1969397-c0770a4fa1137451.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
## MVP
MVP 是从经典的模式MVC演变而来，它们的基本思想有相通的[地方](http://baike.baidu.com/item/%E5%9C%B0%E6%96%B9/2262175)：Controller/Presenter负责逻辑的处理，Model提供数据，View负责显示。
作为一种新的模式，MVP与MVC有着一个重大的区别：在MVP中View并不直接使用Model，它们之间的通信是通过Presenter (MVC中的Controller)来进行的，所有的交互都发生在Presenter内部，而在MVC中View会从直接Model中读取数据而不是通过 Controller。

![MVP](http://upload-images.jianshu.io/upload_images/1969397-4e308fafe7dd4c04.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**MVP的优点:**
> 1. 模型与视图完全分离，我们可以修改视图而不影响模型
2. 可以更高效地使用模型，因为所有的交互都发生在一个地方——Presenter内部
3. 我们可以将一个Presenter用于多个视图，而不需要改变Presenter的逻辑。这个特性非常的有用，因为视图的变化总是比模型的变化频繁。
4. 如果我们把逻辑放在Presenter中，那么我们就可以脱离用户接口来测试这些逻辑（单元测试）

**MVP缺点:**
> 由于对视图的渲染放在了Presenter中，所以视图和Presenter的交互会过于频繁，如果Presenter过多地渲染了视图，往往会使得它与特定的视图的联系过于紧密。一旦视图需要变更，那么Presenter也需要变更了。比如说，原本用来呈现Html的Presenter现在也需要用于呈现Pdf了，那么视图很有可能也需要变更。

![向下发展到MVVM](http://upload-images.jianshu.io/upload_images/1969397-c0770a4fa1137451.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## MVVM
因为WPF技术出现，从而使MVP设计模式有所改进，MVVM 模式便是使用的是[数据绑定](http://baike.baidu.com/item/%E6%95%B0%E6%8D%AE%E7%BB%91%E5%AE%9A)基础架构。它们可以轻松构建UI的必要元素。MVVM代表的是Model-View-ViewModel。ViewModel的含义就是 "Model of View"，视图的模型。它的含义包含了领域模型（Domain Model）和视图的状态（State）。

![MVVM](http://upload-images.jianshu.io/upload_images/1969397-f456db77eeeb902b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**MVVM优点:**
> MVVM模式和MVC模式一样，主要目的是分离视图（View）和模型（Model），有几大优点
**1. 低耦合**。视图（View）可以独立于Model变化和修改，一个ViewModel可以绑定到不同的"View"上，当View变化的时候Model可以不变，当Model变化的时候View也可以不变。
**2. 可重用性**。你可以把一些视图逻辑放在一个ViewModel里面，让很多view重用这段视图逻辑。
**3. 独立开发**。开发人员可以专注于业务逻辑和数据的开发（ViewModel），设计人员可以专注于页面设计，使用Expression Blend可以很容易设计界面并生成xml代码。
**4. 可测试**。界面素来是比较难于测试的，而现在测试可以针对ViewModel来写。

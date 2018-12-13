---
layout: post
title: functional programming
category: technology
tags: functional programming
description: functional programming
---

[Python中的闭包与惰性计算](https://blog.csdn.net/Solo95/article/details/78844141)  
Code is Data, 函数也可以是返回值  
[柯里化](https://www.cnblogs.com/lovesqcc/p/5398758.html)  
闭包和partial function都能实现，本质为通过保存前面的参数，不断地完善参数列表，从而方便地产生一系列定制函数。  

正则表达式用状态机实现，非图灵完备。但[Lambda表达式是图灵完备的](http://chillyc.info/2017/Lambda%E8%A1%A8%E8%BE%BE%E5%BC%8F%E4%B8%8E%E5%9B%BE%E7%81%B5%E5%AE%8C%E5%A4%87/)。  
[Lambda演算](https://en.wikipedia.org/wiki/Lambda_calculus)  
[中文](https://www.cnblogs.com/kirohuji/p/7080876.html)
[不动点组合子](https://zh.wikipedia.org/wiki/%E4%B8%8D%E5%8A%A8%E7%82%B9%E7%BB%84%E5%90%88%E5%AD%90)  
[浅谈Y组合子](http://jjyy.guru/y-combinator)  

[Haskell](https://www.w3cschool.cn/hsriti/)  
[Haskell与范畴论](https://www.cnblogs.com/catch/p/3973104.html)  
[函数编程中functor和monad的形象解释](https://www.jdon.com/idea/functor-monad.html)  

C++支持lambda匿名函数，作为某类STL中的函数参数传入，能使代码更简洁。  
事实上，简单来说（并不严谨），functor（函子）即为该类STL，其作用是指导如何使用传入的各参数及lambda函数。  
在这个语境下，object及object间的态射关系（函数）组成了一个范畴，而functor为这些范畴间的映射，既映射了对象，也通过使用lambda函数映射了态射（函子在态射组合上必须满足分配律）。  
Haskell语境下范畴中的元素对象是Haskell的类型，态射箭头是Haskell的函数。  
自函子（Endofunctor）即输入输出类型相同的此类STL。  
举例来说，<int,+>、<double,+>都满足半幺群的定义，给它们一人定义一个态射吧，就叫 f1 和 f2。一个函数 double func(int s, lambda f)就可以看作是一个从范畴<int,f1>到范畴<double,f2>的映射。你可以再传入一个lambda f函数来辅助规定一下这个 int 的 f1 怎么映射到 double 的 f2 上去。这一整个func就是一个函子。  
若func定义为 int func(int s, lambda f)，那它就可以作为一个自函子了。  
事实上，很多模版都可以写成这样的形式，以减少函数重载所带来的重复代码，你只需要写一个对应的lambda匿名函数来规定怎么映射态射即可。  

至此，我们可以从实例的角度理解这句名言：“一个单子(Monad)说白了不过就是自函子范畴上的一个幺半群(Monoid)而已,有什么难以理解的”。  
首先，Monad中对象是一堆函子，或者说该monoid的对象即为自函子，这些函子间的态射是符合结合律的。  
Monad可以简单地理解为一个函子的模版，定义了函子的基本处理流程（态射）。具体要映射哪个函子由编程者传进去就行，函子只是个参数，如同上文的 int 与 double 一样。Monad把一个函子包装一下再传出来，就完成了函子的态射。Monad包装函子，帮函子变得更完善，以能够显式地传递状态（纯函数编程中这并不容易），而不至于把代码可读性弄得太差。  

[为什么需要Monad?](https://www.jdon.com/46884)  
其实跟装饰器有点像。[V2EX](https://www.v2ex.com/t/445290)  

Lisp宏, 元编程, vim宏
Lisp通过统一编码的S-表达式（树结构）来完成 Code is Data 这一特性。代码可以像数据一样被操作。  
# 编译器

    GCC, G++, CPP, GPP
      随着开源运动的兴起，自由软件基金会开发了自己的开源免费的C语言编译器GNU C Compiler，简称GCC。
      GCC中提供了C Preprocessor这个C语言的预处理器，简称CPP。后来GCC又加入了对C++等其它语言的支持，
      所以他的名字也改为GNU Compiler Collection。G++则是专门用来处理C++语言的。在GNU的官方手册中，
      有一个章节叫做G++ and GCC介绍了这二者的区别。G++是GCC编译器集合的一个前端。
      关于前端、后端的概念下面有更详细的介绍。而GPP呢，这个名字比较特殊，如果你用的是Linux系统，
      可能并没有这个命令。但是在某些特殊的系统下，例如DOS，是无法创建G++这样带有特殊符号的文件名的。
      所以按照DJGPP编译器的做法，GPP其实就是G++。

    LLVM与GCC
      回顾GCC的历史，虽然它取得了巨大的成功，但开发GCC的初衷是提供一款免费的开源的编译器，仅此而已。
      可后来随着GCC支持了越来越多的语言，GCC架构的问题也逐渐暴露出来。
      但GCC到底有什么问题呢？
      我们一起看看这篇文章：The Architecture of Open Source Applications: LLVM。
      http://www.aosabook.org/en/llvm.html
      LLVM的优点也正是GCC的缺点。

    传统编译器
      传统编译器的工作原理基本上都是三段式的，可以分为前端（Frontend）、优化器（Optimizer）、后端（Backend）。
      前端负责解析源代码，检查语法错误，并将其翻译为 抽象的 语法树（Abstract Syntax Tree）。
      优化器对这一中间代码进行优化，试图使代码更高效。
      后端则负责将优化器优化后的中间代码转换为目标机器的代码，
      这一过程后端会最大化的利用目标机器的特殊指令，以提高代码的性能。

    这种三段式的结构还有一个好处，开发前端的人只需要知道如何将源代码转换为优化器能够理解的中间代码就可以了，
    他不需要知道优化器的工作原理，也不需要了解目标机器的知识。这大大降低了编译器的开发难度，使更多的开发人员可以参与进来。

    虽然这种三段式的编译器有很多有点，并且被写到了教科书上，但是在实际中这一结构却从来没有被完美实现过。
    做的比较好的应该属Java和.NET虚拟机。虚拟机可以将目标语言翻译为bytecode，
    所以理论上讲我们可以将任何语言翻译为bytecode，然后输入虚拟机中运行。
    但是这一动态语言的模型并不太适合C语言，所以硬将C语言翻译为bytecode并实现垃圾回收机制的效率是非常低的。

    GCC也将三段式做的比较好，并且实现了很多前端，支持了很多语言。
    但是上述这些编译器的致命缺陷是，他们是一个完整的可执行文件，
    没有给其它语言的开发者提供代码重用的接口。即使GCC是开源的，
    但是源代码重用的难度也比较大。


    LLVM最初是Low Level Virtual Machine的缩写，定位是一个虚拟机，但是是比较底层的虚拟机。
    它的出现正是为了解决编译器代码重用的问题，LLVM一上来就站在比较高的角度，
    制定了LLVM IR这一中间代码表示语言。LLVM IR充分考虑了各种应用场景，
    例如在IDE中调用LLVM进行实时的代码语法检查，对静态语言、动态语言的编译、优化等。

    LLVM Compiler

    从上面这个图中我们发现LLVM与GCC在三段式架构上并没有本质区别。
    LLVM与其它编译器最大的差别是，它不仅仅是Compiler Collection，也是Libraries Collection。
    举个例子，假如说我要写一个XYZ语言的优化器，我自己实现了PassXYZ算法，
    用以处理XYZ语言与其它语言差别最大的地方。而LLVM优化器提供的PassA和
    PassB算法则提供了XYZ语言与其它语言共性的优化算法。
    那么我可以选择XYZ优化器在链接的时候把LLVM提供的算法链接进来。
    LLVM不仅仅是编译器，也是一个SDK。

    Pass Linkage

    Apple LLVM compiler 4.2和LLVM GCC 4.2
    现在我们可以回答本文最前面我遇到的那个问题了。Apple LLVM compiler 4.2是一个真正的LLVM编译器，
    前端使用的是Clang，基于最新的LLVM 3.2编译的。LLVM GCC 4.2编译器的核心仍然是LLVM，
    但是前端使用的是GCC 4.2编译器。从LLVM的下载页面可以看出，
    LLVM从1.0到2.5使用的都是GCC作为前端，直到2.6开始才提供了Clang前端。
    


The LLVM Compiler Infrastructure
================================

      This directory and its subdirectories contain source code for LLVM,
      a toolkit for the construction of highly optimized compilers,
      optimizers, and runtime environments.

      LLVM is open source software. You may freely distribute it under the terms of
      the license agreement found in LICENSE.txt.

      Please see the documentation provided in docs/ for further
      assistance with LLVM, and in particular docs/GettingStarted.rst for getting
      started with LLVM and docs/README.txt for an overview of LLVM's
      documentation setup.

      If you are writing a package for LLVM, see docs/Packaging.rst for our
      suggestions.


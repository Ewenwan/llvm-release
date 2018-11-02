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


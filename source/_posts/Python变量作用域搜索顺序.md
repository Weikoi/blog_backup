---
title: Python变量作用域搜索顺序
date: 2019-08-24 19:50:05
categories:
- Python
tags:
- Python
- 编程语言
- 基础知识
---


#### Python变量作用域的查找顺序

python解释器在解引用一个变量时遵循所谓‘l->e->g->b’原则。

即，首先在local即局部作用域中查找变量声明和值，如果没有找到，在函数的closure属性中查找变量（只有闭包函数要考虑）即enclosing，如果还没有找到则在全局作用域中查找变量即global，如果还是没有找到则在built-in的变量中查找，也就是python的关键字和默认的全局函数，内置作用域（e.g. list tuple open print）。

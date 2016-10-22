---
title: C program 日记02-对日记2的纠正
tag: [pointer,misunderstanding]
category: C语言日记
date: 2016-09-24
---

# 理解const和引出的问题
**2016.9.24 重庆 小雨**

我对日记2中的自己的一些"理解或猜想"有些担心。于是就有了这篇日记

### 指针不是类型吗？

上一篇日记中

> 原来我以为`char *`可以看作是一种数据类型，比如字符串指针类型，这是当时的有偏差的理解，其实`*`一直都是指针运算符...

然后我在[ANSI C Yacc grammar]()中找到了关于指针的分词模式定义：
```
pointer
	: '*'
	| '*' type_qualifier_list
	| '*' pointer
	| '*' type_qualifier_list pointer
	;

type_qualifier_list
	: type_qualifier
	| type_qualifier_list type_qualifier
	;

type_qualifier
	: CONST
	| VOLATILE
	;

```

和指针的使用：
```
declarator
	: pointer direct_declarator
	| direct_declarator
	;

abstract_declarator
	: pointer
	| direct_abstract_declarator
	| pointer direct_abstract_declarator
	;

direct_declarator
	: IDENTIFIER
	| '(' declarator ')'
	| direct_declarator '[' constant_expression ']'
	| direct_declarator '[' ']'
	| direct_declarator '(' parameter_type_list ')'
	| direct_declarator '(' identifier_list ')'
	| direct_declarator '(' ')'
	;
```
类似于`*`,`*`

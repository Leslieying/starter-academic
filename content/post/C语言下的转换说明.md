---
title: C语言下的转换说明
date: 2018-11-23 09:06:46
summary: ""
---
## C语言下的转换说明修饰符

* scanf()和getchar()函数的不同在于,getchar()函数和scanf(%c)接受包括转行符在内的所有字符，而使用其他转换修饰符的scanf()则可以通过转换说明限制输入的字符类型。例如，在声明中，`char a;`声明a变量是一个字符，但是我偏偏打进去一个数字96，结果编译器没有报错。为什么呢，因为getchar读取了数字96并且把他存成了一个字符串变量。而scanf()则可以通过%d等来告诉计算机，只要真的数字而不是string。所以，当你用scanf输入错误的数据类型时，会得到

```C
warning: format ‘%d’ expects argument of type ‘int *’, but argument 2 has type ‘char *’ [-Wformat=]
   scanf("%d", &a);
          ~^   ~~
          %hhd
```

意思就是数据类型不匹配。同样地，如果一开始声明变量就是字符串外的其他类型，那么也一样会报错。
所以一个输入流程应该是

```C
input > if char > %convertion(if %c or getchar: pass) > variable
```

在获取用户输入的时候，就要尤其注意，要添加一段`while (getchar() != '\n') continue;`来跳开换行符。

* printf()函数也可以通过转换说明修饰符（例如%d, %c ）来对输出进行转换。例如下面的代码：

```C
 #include <stdio.h>
 int main(void)
 {
 int a;
 scanf("%d", &a);
 printf("%c\n", a);

 return 0;
  }
```

我输入一个int整数，结果可以转化为相应的字符。因为在计算机中，无论是整数还是字符，都只是二进制的01序列而已。所以，转换说明也相当于一个翻译的作用，例如将十进制输出为十六进制（%x）。

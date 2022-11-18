# llvm-learn
A tiny demo for LLVM learning

LLVM环境

```shell
MacOS M1 Pro - Apple Silicon (ARM Architecture)
llvm@11
clang version 11.1.0
```

C语言程序（Demo）

```c
#include <stdio.h>

int main() {
    int a=1,b=2;
    int c = a + b;
    printf("the sum of a + b = %d", c);
    return 0;
}
```

使用clang编译生成.o文件要经历的中间过程

```shell
clang test.c -o test
```



Step-1: 前端语法分析

```shell
clang -Xclang -ast-dump -fsyntax-only test.c
```

Step-2: 前端中间代码生成IR

```shell
clang -S -emit-llvm test.c
```

Step-3: 后端优化IR

```shell
clang -S -emit-llvm -O3 test.c
```

Step-4: LLVM后端生成汇编代码

```shell
llc test.ll
```

Pipeline

```shell
.c --frontend--> AST --frontend--> LLVM IR --LLVM opt--> LLVM IR --LLVM llc--> .s Assembly --OS Assembler--> .o --OS Linker--> executable
```


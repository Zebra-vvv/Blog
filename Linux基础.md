# gcc



## gcc编译四步骤

### 1、预处理

```bash
gcc -E
```

+ 展开宏、头文件，删除注释、空行



### 2、编译

```bash
gcc -S
```

+ 检查语法规范，将高级语言翻译成汇编语言



### 3、汇编

```bash
gcc -c 
```

+ 将汇编指令翻译成机器指令，生成.o目标文件



### 4、链接

```
gcc 无参数
```

+ 链接阶段将目标文件与所需的库文件（如标准库）链接在一起，生成最终的可执行文件。



​        这里是一个**简单的示例**，演示如何执行每个编译步骤并生成相应的文件。我们将使用一个名为 `main.c` 的源代码文件，其中包含一个简单的 C 函数。我们假设你正在使用 Linux 或类似系统，并且已经安装了 `gcc` 编译器。

1. **预处理（Preprocessing）：**
   创建一个名为 `main.c` 的源代码文件，内容如下：

```c
#include <stdio.h>

#define MY_CONSTANT 42

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

然后在终端中执行预处理：

```bash
gcc -E main.c -o main.i
```

这将生成一个名为 `main.i` 的预处理后的文件。

2. **编译（Compiling）：**
   使用生成的预处理文件进行编译：

```bash
gcc -S main.i -o main.s
```

这将生成一个名为 `main.s` 的汇编代码文件。

3. **汇编（Assembling）：**
   使用生成的汇编文件进行汇编：

```bash
gcc -c main.s -o main.o
```

这将生成一个名为 `main.o` 的目标文件。

4. **链接（Linking）：**
   使用生成的目标文件进行链接，生成最终的可执行文件：

```bash
gcc main.o -o my_program
```

这将生成一个名为 `my_program` 的可执行文件。

最终，你可以运行生成的可执行文件：

```bash
./my_program
```

这个示例演示了如何手动执行编译的各个步骤，并生成相应的文件。在实际开发中，通常使用简化的编译命令，`gcc` 会自动执行这些步骤并生成最终的可执行文件。



---



# 静态库和动态库



## 静态库制作及使用

### 1、将 .c 生成 .o 文件

```bash
gcc -c add.c -o add.o
```

### 2、使用 ar 工具制作静态库

```bash
ar rcs libadd.a add.o
```

### 3、编译静态库到可执行文件中

```bash
gcc test.c libadd.a -o a.out
```



+ **头文件守卫的概念**

除了头文件守卫之外，还有一些其他方法可以实现防止头文件的重复包含。以下是一些常见的方法：

1. **`#pragma once` 指令：** 一些编译器支持 `#pragma once` 指令，它可以代替传统的头文件守卫。它的作用与头文件守卫相同，但更简洁。例如：

    ```c
    #pragma once

    // 头文件内容
    ```

    注意，`#pragma once` 的可移植性有限，不是所有编译器都支持。

2. **`#define` 和 `#ifdef`：** 你也可以使用 `#define` 和 `#ifdef` 指令来检查宏是否已经定义，从而防止头文件的重复包含。但相对于头文件守卫，这种方式显得冗长。

    ```c
    #ifndef HEADER_NAME_H
    #define HEADER_NAME_H

    // 头文件内容

    #endif // HEADER_NAME_H
    ```

3. **命名空间（Namespace）：** 在 C++ 中，使用命名空间可以有效地避免全局作用域中的名称冲突，从而实现头文件不重复包含的目的。

4. **前置声明（Forward Declaration）：** 如果只需要使用类的指针或引用，可以使用前置声明来避免包含完整的类定义。这可以减少需要包含的头文件数量。

尽管存在其他方法，但头文件守卫是应用最广泛且最通用的方式，适用于 C 和 C++，且具有较好的可移植性。根据你的需求和编程环境，选择合适的方法来防止头文件的重复包含。



## 动态库的制作及使用

### 1、将 .c 生成 .o 文件(生成与位置无关的代码，参数：-fPIC)

```bash
gcc -c add.c -o add.o -fPIC
```

### 2、使用 gcc -shared 制作动态库

```bash
gcc -shared -o libmymath.so add.o sub.o div.o
```

### 3、编译可执行程序时，指定所使用的动态库

+ -l：指定库名
+ -L：指定库的路径

```bash
gcc test.c -o a.out -l mymath -L ./lib
```

### 4、运行可执行程序会出错

**出错原因：**动态链接器出错

+ 链接器：工作于链接阶段，工作时需要 -l 和 -L
+ 动态链接器：工作于程序运行阶段，工作时需要提供动态库所在目录位置

**解决方式：**

+ **通过环境变量（临时生效，终端重启环境变量就会失效)**

```bash
export LD_LIBRARY_PATH=./lib //赋值动态库路径,建议使用绝对路径
```

+ **写入终端配置文件 .bashrc(永久生效)**

1. vim打开配置文件

```bash
vim ~/.bashrc
```

2. 给环境变量赋值

```bash
export LD_LIBRARY_PATH=./lib //赋值动态库路径,建议使用绝对路径
```

3. 生效脚本文件/重启终端

```bash
. .bashrc
```

+ **将动态库放到/目录下lib(标准C库所在目录)中**

+ **配置文件法**

1. 打开配置文件

```bash
vim /etc/ld.so.conf
```

2. 写入动态库绝对路径
3. 使配置文件生效

```bash
sudo ldconfig -v
```



# gdb



## 调试准备

```bash
gcc -g test.c -o a.out
```

-g：使用改参数编译可执行文件，得到调试表

```bash
gdb a.out
```



## 基础指令

list/l 1：从第一行列出源码

b 20：在20行位置设置断点

run/r：运行程序

next/n：步过

step/s：步入

print/p i：查看变量i的值

continue/c：继续断点后续指令

quit/q：退出



## 其他指令（先略过了）

run：可以直接使用run来查找段错误的出现位置



# makefile

默认只有两个名称可以识别：makefile和Makefile



## 一个规则

### 格式

目标：依赖条件

（tab缩进）命令

```makefile
hello:hello.c
	gcc hello.c -o hello
```

1. 目标的时间必须晚于依赖条件的时间，否则，更新目录
2. 依赖条件如果不存在，寻找规则去产生依赖

**ALL命令：**指定mikefile的终极目标(默认终极目标是第一行的目标)



## 两个函数

```makefile
src = $(wildcard ./*.c) //匹配当前工作目录下的所有.c文件，将文件名组成列表，赋值给变量src
```

```makefile
obj = $(patsubst %.c,%.o,$(src)) //将参数3中包含参数1的部分，替换为参数2
```



## 三个自动变量

$@：在规则的命令(第二行是命令)中，表示规则中的目标

$^： 在规则的命令(第二行是命令)中，表示所有依赖条件

$<： 在规则的命令(第二行是命令)中，表示第一个依赖条件，如果将该变量应用在模式规则中，它可将依赖条件列表中的依赖依次取出，套用模式规则



## 模式规则

```makefile
clean:
	-rm -rf $(obj) a.out
```
























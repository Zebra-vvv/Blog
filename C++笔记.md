



# 2023.4



## 4.16

### 1、常量的学习

```c++
#include<iostream>
using namespace std;

//常量的定义方式
//1、#define 宏常量
//2、const修饰的变量


//1、#define 宏常量 通常定义在文件的最上方
#define Week 7

int main()
{
	//Week = 14;   //Week是常量，不可修改，修改会报错
	cout << "一周有" << Week << "天" << endl;
	
	//2、const修饰的变量   可以定义在main函数里面
	const int month = 12;
	//month = 24;  //const修饰的变量也是常量，不可修改
	cout << "一年有" << month << "个月" << endl;
	
	
	system("pause");
	return 0;
}
```

### 2、标识符的命名

```c++
#include<iostream>
using namespace std;

//标识符的命名规则：
//1、标识符不可以是关键字
//2、标识符由字母、数字和下划线构成
//3、标识符第一个字符只能是字母或下划线
//4、标识符严格区分大小写

int main()
{
    //1、标识符不可以是关键字
    //int int = 10;

    //2、标识符由字母、数字和下划线构成
    int abc = 1;
    int _abc = 2;
    int _123abc = 3;

    //3、标识符第一个字符只能是字母或下划线
    //int 123abc = 40;

    //4、标识符严格区分大小写
    int a = 100;
    //cout << A << endl;

    //建议：给变量起名的时候，最好做到见名知意
    int num1 = 10;
    int num2 = 20;
    int sum = num1 + num2;
    cout << sum << endl;

    system("pause");
    return 0;
}
```

### 3、整型和实型（浮点型）

+  	    **short<int<=long<long long**（long在windows和Linux下所占字节不同）
+  	    sizeof ( 数据类型 / 变量)

+ float类型定义
    + ```c++
        float f1 = 3.14f;  //如果不多加一个f，默认为double类型
        ```

    + 默认情况下，C++输出小数最多保留**6位有效数字**，如果需要修改，需要一些进阶操作

    + 科学计数法

        ```c++
        float f1 = 3e2;      //3 * 10 ^ 2
        float f2 = 3e-2;     //3 * 0.1 ^ 2
        ```

    
    ![image-20230426120008886](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20230426120008886.png)

------



## 4.17

### 1、字符型

+ char所占内存空间1B

+ 只能用单引号创建**字符型**

+ char只能存一个字符

+ ```c++
    char ch = 'a';
    cout << (int)ch << endl;   //强制转为int型号，返回字母a的ASCII码     A-65   a--97
    ```

### 2、转义字符

+ 换行符   \n

+ 反斜杠   \\\

+ 水平制表符   \t

+ ```c++
    #include<iostream>
    using namespace std;
    int main()
    {
        cout << "a\tHelloWorld" << endl;  //前面Hello占5格，后面空格就占3格，反正加起来要占8格
        cout << "aa\tHelloWorld" << endl;  //实现了对齐的效果，整齐地输出后面的字符
        cout << "aaa\tHelloWorld" << endl;
        return 0;
    }
    ```

 ### 3、字符串型

+ C风格字符串：`char 变量名[] = "字符串值"`

  + 只能用双引号创建**字符串**型

  + 需要一个中括号
    ```c++
     char str1[] = "Hello World";
     cout << str1 << endl; 
    ```

+ C++风格字符串：`string 变量名 = “字符串值”`

  + ```c++
      include <string>              //一定要包含头文件
      string str2 = "Hello World";
      cout << str2 << endl; 
      ```

 ### 3、布尔类型

+ 只占1B内存
+ 只要非0就是真

### 4、算数运算符

+ 两个整数相除，结果依然是整数，小数部分直接扔掉
  ```c++
  int a = 10,b = 3;
  cout << a / b << endl;    //结果是3
  ```

+ 两个小数相除，结果可以是小数

    ```c++
    double d1 = 1.5,d2 = 0.2;
    cout << d1 / d2 << endl;  //结果是7.5
    ```

### 5、前置后置 递增递减

+ 前置递增：先让变量+1，然后进行表达式的运算

+ 后置递增：先进行表达式的运算，然后让变量+1

```c++
#include<iostream>
using namespace std;
int main()
{
	int a1 = 10;
	int b1 = ++a1 * 10;  
	cout << b1 << endl;   //输出110

	int a2 = 10;
	int b2 = a2++ * 10;   
	cout << b2 << endl;  //输出100 
    return 0;
}
```

### 6、比较运算符

```c++
#include<iostream>
using namespace std;

int main()
{
	int a = 1, b = 2;
	cout << (a == b) << endl;  //输出0，代表假
	cout << (a != b) << endl;  //输出1，代表真
	return 0;
}
```

### 7、三目运算符

```c++
#include<iostream>
using namespace std;

int main()
{
	int a = 1, b = 2;
	int c = (a > b ? a : b);
	cout << c << endl;         //返回b的值
    
	(a > b ? a : b) = 100;     //三目运算符返回的是变量，可以继续赋值
	cout << a << endl;
	cout << b << endl;         //b被返回且被赋值为100
}
```

### 8、switch语句

+ switch中表达式类型只能是**整型**或**字符型**，不能判断区间

+ 每一个case不要忘记**加break**

+ 与if语句相比，结构清晰，执行**效率高**

  ​    
--------



## 4.19

### 1、生成随机数

```c++
#include <iostream>
#include<ctime>   //包含time系统时间头文件
using namespace std;

int main()
{
	srand((unsigned int)time(NULL));   //添加随机数种子，利用当前系统时间生成
	int num = rand() % 100 + 1;        //生成1~100的随机数
	int val;
	while (1)
	{
		cout << "请输入你猜的数字：" << endl;
		cin >> val;
		if (val > num)
		{
			cout << "你猜的数太大了！" << endl;
		}
		else if (val < num)
		{
			cout << "你猜的数太小了！" << endl;
		}
		else 
		{
			cout << "你猜对了！" << endl;
			break;
		}
	}
}
```

### 2、do while 语句

+ 与while的区别在于do while会先执行一次循环语句，再判断循环条件

```c++
#include <iostream>
using namespace std;

int main()
{
	int num = 0;
	do
	{
		cout << num << endl;
		num++;
	} while (num); //先执行，后判断，会进入死循环输出数字
	return 0;
}
```

+ 水仙花数
```c++
#include <iostream>
using namespace std;

int main()
{
    int n = 100;
    do{
        int a = n % 10;         //取模于10，可以获取到个位
        int b = n / 10 % 10;    //先整除于10，得到一个两位数，再获取这个两位数的个位，也就得到了原三位数的十位
        int c = n / 100;        //直接整除于100，获取百位

        if (a * a * a + b * b * b + c * c * c == n)
        {
            cout << n << endl;
        }
        n++;
    }while(n < 1000);
    return 0;
}
```

### 3、嵌套循环

+ 乘法口诀表

```c++
#include <iostream>
using namespace std;

int main()
{
    for(int i=1;i<=9;i++)
    {
        for(int j=1;j<=i;j++)      //列数小于等于行数
        {
            cout<<j<<"*"<<i<<"="<<j*i<<"\t";
        }
        cout<<endl;
    }
    return 0;
}
```

### 4、continnue语句

+ 执行到本行，就不再执行后面的代码了，而执行**下一次循环**

+ 注意和break区分，break是直接跳出**整个循环**了

    


-------



## 4.20

### 1、数组

+ ```c++
    #include <iostream>
    using namespace std;
    
    int main()
    {
        int arr[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9};
        cout << sizeof(arr) << endl;     //获取整个数组的长度
        cout << sizeof(arr[0]) << endl;  //获取单个元素的长度
        cout << sizeof(arr) / sizeof(arr[0]) << endl;  //两者相除计算出数组中元素的个数
    
        //通过数组名查看数组首地址，即数组中第一个元素的地址
        cout << arr << endl;
        cout << &arr[0] << endl;  //访问具体元素要加取址符
        return 0;
    }
    ```

### 2、冒泡排序

```c++
#include <iostream>
using namespace std;

int main()
{
    int arr[9] = {4, 2, 8, 0, 5, 7, 1, 3, 9};
    for (int i = 0; i < 9 - 1; i++)           //外层循环次数=数组元素个数-1
    {
        for (int j = 0; j < 9 - i - 1; j++)   //内层循环次数=外层循环次数-i(当前外层轮次)
        {
            if (arr[j + 1] > arr[j])      //递减排序
            {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    for (int k = 0; k < 9; k++)
    {
        cout << arr[k] << " ";
    }
    return 0;
}
```



---------



## 4.21

### 1、二维数组

+ 定义二维数组，行数可以省去，会自动计算出来
```c++
int arr[][3]={1,2,3,4,5,6};    //自动会算出这是一个2行3列的矩阵
```

+ 二维数组行数列数计算方法：
```c++
int row = sizeof(arr) / sizeof(arr[0]);    // 行数=整个二维数组所占字节/一行所占字节
int column = sizeof(arr[0]) / sizeof(arr[0][0]);  //列数=一行所占字节/单个元素所占字节
```

### 2、函数调用

```c++
#include <iostream>
using namespace std;

int add(int num1, int num2)  //num1和num2是形参，没有值，在调用函数的时候，实参的值会传递给形参
{
    return num1 + num2;
}

int main()
{
    int a = 1, b = 3;
    int result = add(a, b);  //a和b是实参，有自己的值
    cout << result << endl;
    return 0;
}
```

### 3、值传递

```c++
#include <iostream>
using namespace std;

void swap(int num1, int num2)
{
    int temp = num1;
    num1 = num2;
    num2 = temp;
}

int main()
{
    int a = 1, b = 2;
    swap(a, b);
    cout << a << " " << b << endl;   //输出结果发现，a和b并没有交换，因为值传递时，形参发生任何改变，不会影响实参
    return 0;
}
```

### 4、函数声明

```c++
#include <iostream>
using namespace std;

int compare(int a, int b);//函数声明，因为compare函数定义写在了main函数后面(程序顺序执行，会不知道compare什么意思)，如果compare函数写在main函数前面，可以不用声明

int main()
{
    int a = 1, b = 2;
    cout << compare(a, b) << endl;
    return 0;
}

int compare(int a, int b)
{
    return a > b ? a : b;
}
```

### 4、函数的分文件编写

+ 4个步骤

  1. 创建后缀名为.h的头文件
  2. 创建后缀名为.cpp的源文件
  3. 在头文件中写函数的声明
  4. 在源文件中写函数的定义

```c++
//swap.h头文件
#include <iostream>
using namespace std;

void swap(int a, int b);  //头文件写函数的声明
```

```c++
//swap.cpp源文件
#include "swap.h"

void swap(int a, int b)  //源文件中写函数的定义
{
    int temp = a;
    a = b;
    b = temp;
    cout << a << " " << b << endl;
}
```

```C++
//调用函数的主程序
#include <iostream>
using namespace std;
#include "swap.h"   //主程序调用时，直接包含头文件

int main()
{
    int a = 10, b = 20;
    swap(a, b);
    return 0;
}
```

### 3、指针

+ 定义和使用

```c++
int main()
{
    int a = 10;
    int *p = &a;
    cout << &a << endl;  //输出a的地址
    cout << p << endl;   //指针中存放的就是a的地址，也是输出a的地址
	
    *p = 1000;           //利用解引用，可以修改a的值
    
    cout << a << endl;   //输出a的值
    cout << *p << endl;  //指针前面加*号解引用，也是输出a的值
    return 0;
}
```

+ 指针所占内存空间：不管是什么数据类型，32位系统占4个字节，64位系统占8个字节（因为8bit=1B)

    

-------



## 4.22

### 1、空指针和野指针

+ 空指针：指针变量指向内存中编号为0的空间，空指针用于初始化指针变量，指向的内存不可以访问
+ 野指针：指针变量指向非法的内存空间

### 2、const修饰指针

+ √ 表示可以修改，× 表示不可修改

|          三种形式           | 指针的指向 | 指针指向的值 |
| :-------------------------: | :--------: | :----------: |
|          常量指针           |     √      |      ×       |
|          指针常量           |     ×      |      √       |
| const既修饰指针，又修饰常量 |     ×      |      ×       |

```c++
#include <iostream>
using namespace std;

int main()
{
    int a = 1, b = 2;

    const int *p1 = &a;        //常量指针(const后面修饰的是*p，也就是把指针的值给限定住了)
    p1 = &b;                   //指针的指向可以修改

    int *const p2 = &a;        //指针常量(const后面修饰的是p，也就是把指针的指向给限定住了)
    *p2 = 2;                   //指针的值可以修改

    const int *const p3 = &a;  //const既修饰指针，也修饰常量，两者都被限定住了

    return 0;
}
```

### 3、指针和数组

```c++
#include <iostream>
using namespace std;

int main()
{
    int arr[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int *p = arr;
    for (int i = 0; i < 10; i++)
    {
        cout << *p << endl;  //利用指针来遍历数组
        p++;                 //64位系统下，p++会向后移动8个字节
    }
    return 0;
}
```

### 4、地址传递

```c++
#include <iostream>
using namespace std;

void swap1(int num1, int num2)//值传递
{
    int temp = num1;
    num1 = num2;
    num2 = temp;
}

void swap2(int *p1, int *p2)//地址传递
{
    int temp = *p1;
    *p1 = *p2;
    *p2 = temp;
}

int main()
{
    int a = 1, b = 2;
    swap1(a, b);
    cout << a << " " << b << endl;  //值传递，形参没法改变实参，a和b并没有交换
    swap2(&a, &b);
    cout << a << " " << b << endl;  //地址传递，形参改变，实参也会改变，a和b交换成功
    return 0;
}
```



-------



## 4.23

### 1、结构体的定义和使用

```c++
#include <iostream>
#include <string>
using namespace std;

struct Student //定义结构体时，struct不能省略
{
    string name;
    int age;
    int score;
} s1; //第一种创建方式，顺便创建一个结构体变量

int main()
{
    s1.name = "王五";

    struct Student s2; //第二种创建方式，这里struct可以省略
    s2.name = "张三";
    s2.age = 18;
    s2.score = 100;

    Student s3 = {"李四", 19, 80}; //第三种创建方式

    return 0;
}
```

### 2、结构体指针

```c++
#include <iostream>
#include <string>
using namespace std;

struct Student
{
    string name;
    int age;
    int score;
};

int main()
{
    Student s1 = {"张三", 18, 100};
    Student *p = &s1;
    cout << "姓名：" << p->name
         << "  年龄：" << p->age
         << "  分数：" << p->score << endl; //利用->，可以通过结构体指针来访问结构体中的属性
    return 0;
}
```

### 3、嵌套结构体

```c++
#include <iostream>
#include <string>
using namespace std;

struct Student
{
    string name;
    int age;
    int score;
};

struct Teacher
{
    string name;
    int id;
    int age;
    Student stu;
};

int main()
{
    Teacher t;
    Student s;
    t.stu.score = 100;  //嵌套结构体
    cout << t.stu.score << endl;
    return 0;
}
```

### 4、结构体中的const

```c++
#include <iostream>
#include <string>
using namespace std;

struct Student
{
    string name;
    int age;
    int score;
};

void PrintStudent(const Student *s) //用指针作为函数的形参，不会像值传递那样复制一份新的副本，可以节省内存空间
{
    //s->age = 100;     const可以防止函数中的误操作（不允许修改的数据）
    cout << "姓名：" << s->name
         << "  年龄：" << s->age
         << "  分数：" << s->score << endl;
}

int main()
{
    Student s = {"张三", 18, 100};
    PrintStudent(&s);
    return 0;
}
```



------------



## 4.25

### 1、内存分区模型

**程序运行前**

+ 代码区：存放函数体的二进制代码，由操作系统进行管理

+ 全局区：存放**全局变量**、**静态变量**以及**常量**

**程序运行后**

+ 栈区：由编译器自动分配释放，存放**函数的参数值(形参)**，**局部变量**等

+ 堆区：由程序员分配和释放，若程序员不释放，程序结束时，由操作系统回收



**内存分区的意义：**

不同区域存放的数据，赋予不同的声明周期，编程更加灵活



---



## 4.26

### 1、全局区

```c++
#include <iostream>
using namespace std;

int g_a = 10, g_b = 10;//全局变量
const int c_g_a = 10, c_g_b = 10;//const修饰的全局变量(全局常量)

int main()
{
    int a = 10, b = 10;//局部变量
    static int s_a = 10, s_b = 10;//静态变量
    const int c_l_a = 10, c_l_b = 10;//const修饰的局部变量(局部常量)

    cout << "局部变量a地址：" << (long long) &a << endl;
    cout << "局部变量b地址：" << (long long) &b << endl;

    cout << "全局变量a地址：" << (long long) &g_a << endl;
    cout << "全局变量b地址：" << (long long) &g_b << endl;

    cout << "静态变量a地址：" << (long long) &s_a << endl;
    cout << "静态变量b地址：" << (long long) &s_b << endl;

    cout << "字符串常量的地址：" << (long long) &"Hello world!" << endl;

    cout << "全局常量c_g_a的地址：" << (long long) &c_g_a << endl;
    cout << "全局常量c_g_b的地址：" << (long long) &c_g_b << endl;

    cout << "局部常量c_l_a的地址：" << (long long) &c_l_a << endl;
    cout << "局部常量c_l_b的地址：" << (long long) &c_l_b << endl;

    return 0;
}
```

运行以上代码，发现只有局部变量和局部常量不在全局区，其余都在全局区，总结如下图：

![image-20230426124314753](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20230426124314753.png)

### 2、栈区

+ 栈区的数据由编译器管理开辟和释放
+ 注意事项：不要返回局部变量的地址

```c++
#include <iostream>
using namespace std;

int *func(int b)//形参也会放在栈区
{
    b = 100;
    int a = 10;//局部变量，存放在栈区，栈区的数据在函数执行完后自动释放，那个地址就不属于你了
    return &a;//所以不要返回局部变量的地址！
}


int main()
{
    int *p = func(1);
    cout << *p << endl;
    cout << *p << endl;
    return 0;
}
```

### 3、堆区

+ 由程序员分配和释放，若程序员不释放，程序结束时由操作系统回收
+ 在C++中主要利用new在堆区开辟内存

```c++
#include <iostream>
using namespace std;

int *func()
{
    int *p = new int(10);//利用new关键字，可以将数据开辟到堆区，返回的是该类型的指针
    return p;//这个指针变量还是局部变量，放在栈上，但是指针保存的数据在堆区
}

int main()
{
    int *p = func();
    cout << *p << endl;
    return 0;
}
```

### 4、new操作符

```c++
#include <iostream>
using namespace std;

int *func()
{
    int *p = new int(10);  //在堆区创建整型数据
    return p;
}

void test01()
{
    int *p = func();
    cout << *p << endl;
    delete p;             //可以用delete释放堆区的数据
    cout << *p << endl;
}

void test02()
{
    int *arr = new int[10];  //在堆区创建含有10个整型数据的数组
    for (int i = 0; i < 10; i++)
    {
        arr[i] = i + 100;
    }
    for (int i = 0; i < 10; i++)
    {
        cout << arr[i] << endl;
    }
    delete[]arr;  //释放堆区的数组，delete需要加[]
 
}

int main()
{
    test01();
    test02();
    return 0;
}
```

### 4、引用做函数参数

+ 本质：给变量起别名
+ 注意事项：引用**必须初始化**，且在初始化之后就**不可以发生改变**
```c++
#include <iostream>
using namespace std;

int main()
{
    int a = 10, c = 20;
    int &b = a;  //引用的基本语法
    //int &b; //错误，必须初始化
    //int &b=c;  //错误，引用初始化之后不允许更改
    cout << a << endl;
    cout << b << endl;
    b = c;  //允许赋值操作，并且a和b操作的是同一块内存,值都会改变
    cout << a << endl;
    cout << b << endl;
    return 0;
}
```

+ **引用**可以做函数参数，可以简化指针的方法(地址传递)，也能达到形参修饰实参的方法

```c++
#include <iostream>
using namespace std;

//交换函数
void swap01(int a, int b)  //值传递，形参不能修饰实参
{
    int temp = a;
    a = b;
    b = temp;
    cout << "swap01中的" << "a = " << a << "," << "b = " << b << endl;  //形参改变了
}

void swap02(int *a, int *b)  //地址传递，形参可以修饰实参
{
    int temp = *a;
    *a = *b;
    *b = temp;
    cout << "swap02中的" << "a = " << *a << "," << "b = " << *b << endl;
}

void swap03(int &a, int &b)  //引用传递，相当于给原来的a起了个别名也叫a，所以形参可以修饰实参
{
    int temp = a;
    a = b;
    b = temp;
    cout << "swap03中的" << "a = " << a << "," << "b = " << b << endl;
}

int main()
{
    int a = 10, b = 20;

    //swap01(a, b);

    //swap02(&a, &b);

    swap03(a, b);
    cout << "main中的" << "a = " << a << " " << "b = " << b << endl;
    return 0;
}
```



-----



## 4.27

### 1、引用做函数返回值

注意：

+ 不要返回局部变量的引用
+ 如果函数的返回值是引用，函数的调用可以作为左值

```c++
#include <iostream>
using namespace std;

//int &test01()
//{
//    int a = 10;//这是局部变量，不要返回局部变量的引用！
//    return a;
//}

int &test02()
{
    static int a = 10;//静态变量，存放在全局区，全局区的数据在程序结束后由系统释放
    return a;
}

int main()
{
    int &ref = test02();
    cout << ref << endl;
    test02() = 1000;  //相当于就是对a的内存进行赋值了，ref是a的别名，也指向同一块内存
    cout << ref << endl;
    return 0;
}
```

### 2、引用的本质

+ 引用的内部实现是一个指针常量(可以回顾4.22笔记)，C++推荐使用引用技术，因为语法方便，而且所有的指针操作编译器都帮我们做了

```c++
#include <iostream>
using namespace std;

void func(int &ref)  //引用，编译器会转化为指针常量来实现，即int* const ref = &a;
{
    ref = 100;  //引用，转化为*ref = 100;
}

int main()
{
    int a = 10;
    int &ref = a; //自动转化为 int* const ref = &a; 指针常量指针的指向不可以修改，所以引用不可以更改
    ref = 20;  //引用，转化为*ref = 20;

    cout << "a:" << a << endl;
    func(a);
    cout << "ref:" << ref << endl;
    return 0;
}
```

### 3、常量引用

+ 常量引用主要用来修饰形参，防止误操作
+ 在函数形参列表中，可以加const修饰，防止形参改变实参

```c++
#include <iostream>
using namespace std;

int main()
{

    //int &ref = 10; 会报错，引用必须引一块合法的内存空间
    const int &ref = 10;//加上const不会报错，编译器底层实现两步：int temp = 10; const int &ref = temp;
    //ref = 20; 会报错，因为加上const之后不可修改
    return 0;
}
```

### 4、函数默认参数

注意：

+ 如果某个位置已经有了默认参数，那么从这个位置往后，从左到右都必须有默认值

+ 如果函数声明有默认参数，函数实现就不能有默认参数

```c++
#include <iostream>
using namespace std;

int func01(int a = 1, int b = 2, int c = 3)
{
    return a + b + c;
}

int func02(int a, int b);

int func02(int a = 10, int b = 10) //函数声明和函数实现，只能有一处有默认参数，否则编译器会混淆
{
    return a + b;
}

int main()
{
    int sum01 = func01();
    cout << sum01 << endl;

    int sum02 = func02();
    cout << sum02 << endl;
    return 0;
}
```



-------



## 4.28

### 1、函数占位参数

+ 函数的形参列表里可以有占位参数，用来做占位，调用函数时必须填补该位置

+ 占位参数也可以有默认参数

```c++
#include <iostream>
using namespace std;

void func01(int a, int)  //后面的int用来占位
{
    cout << "this is a func" << endl;
}

void func02(int a, int = 10)  //占位参数也可以直接给默认参数
{
    cout << "this is a func" << endl;
}

int main()
{
    func01(10,10);  //第二个位置也必须传进去一个数
    func02(10);  //第二个位置有默认参数了
    return 0;
}
```

### 2、CLion如何关闭连按两下shift打开搜索

+ 设置里搜索double，在 Disable double modifier key shortcuts 前面打√，然后点击Apply，再点击 OK ，即可生效

### 3、函数重载

+ 作用：可以让函数名相同，提高复用性

+ 条件：

    + 同一作用域下

    + 函数名称相同

    + 函数参数类型不同，或者参数个数不同，或者参数顺序不同

+ 注意：无法重载仅按返回值类型区分的函数( Functions that differ only in their return type cannot be overloaded )

```c++
#include <iostream>
using namespace std;

void func()
{
    cout << "func的调用" << endl;
}

void func(int a)
{
    cout << "func(int a)的调用!" << endl;
}

void func(double a)
{
    cout << "func(double a)的调用!" << endl;
}

void func(int a, double b)
{
    cout << "func(int a,double b)的调用!" << endl;
}

void func(double b, int a)
{
    cout << "func(double b,int a)的调用!" << endl;
}

int main()
{
    func();  //无参数
    func(1);  //有一个参数
    func(3.14);  //参数类型和上一个不同

    //下面两个是参数顺序不同
    func(1, 3.14);
    func(3.14, 1);
    return 0;
}
```

+ 注意事项：
    1. 引用作为重载的条件
    2. 写函数重载尽量避免默认参数，会出现歧义
```c++
#include <iostream>
using namespace std;

//1、引用作为函数重载的条件
void func01(int &a) //int &a = 10; 不合法
{
    cout << "func01(int &a)的调用" << endl;
}

//两个函数参数类型不同，可以重载
void func01(const int &a)  //const int &a = 10; //加上const不会报错，编译器底层实现两步：int temp = 10; const int &a = temp;
{
    cout << "func01(const int &a)的调用" << endl;
}

//2、函数重载碰到默认参数
void func02(int a, int b = 10)
{
    cout << "func02(int a,int b)" << endl;
}

void func02(int a)
{
    cout << "func02(int a)" << endl;
}

int main()
{
    int a = 10;
    func01(a);
    func01(10);

    //func02(10); 报错，此时编译器两个func02都可以调用，不知道该用哪个
    return 0;
}
```

### 4、封装

+ 封装是C++面向对象三大特性之一
+ 意义：
    + 将属性和行为作为一个整体，表现生活中的事物
    + 将属性和行为加以权限控制

```c++
#include <iostream>	
#include <string>
using namespace std;

const double PI = 3.14;

class Circle
{
public:
    //类中的属性和行为，都可以统一称为成员
    //属性也叫成员属性，成员变量
    //行为也叫成员函数，成员方法
    int m_r;//属性,半径
    double calculateZC()//行为，计算周长
    {
        return 2 * PI * m_r;
    }
};

int main()
{
    Circle c1;    //实例化，通过Circle类创建具体的圆(对象)
    c1.m_r = 10;  //给对象的属性赋值
    cout << "圆的周长为：" << c1.calculateZC() << endl;
    return 0;
}
```

类在设计时，可以把属性和行为放在不同的权限下，加以控制

访问权限有三种：

| 权限类型  | 类内 | 类外 | 继承 |      |
| :-------: | :--: | :--: | :--: | ---- |
|  public   |  √   |  √   |      |      |
| protected |  √   |  ×   |  √   |      |
|  private  |  √   |  ×   |  ×   |      |



-------------



# 2023.5



## 5.2

### 1、struct和class的区别

+ struct默认权限是公共 public

+ class  默认权限为私有 private


### 2、成员属性设置为私有
+ 优点：
    + 将所有成员属性设置为私有，可以自己控制读写权限(在public里写访问函数)
    + 对于”写“权限，我们可以检测数据的有效性

```c++
#include <iostream>
#include <string>
using namespace std;

class Person
{
public:

    void setName(string name)  //设置姓名
    {
        m_Name = name;
    }

    string getName()  //获取姓名
    {
        return m_Name;
    }

    int getAge()  //获取年龄
    {
        return m_Age;
    }

    void setAge(int age)  //设置年龄
    {
        if (age >= 0 && age <= 150)
        {
            m_Age = age;
        } else m_Age = 0;
    }

    string setLover(string lover)  //设置情人
    {
        m_Lover = lover;
    }

private:
    string m_Name;  //可读可写
    int m_Age;  //可读可写，年龄范围0~150
    string m_Lover;  //只写
};


int main()
{
    Person p;
    p.setName("张三");
    cout << "姓名：" << p.getName() << endl;
    p.setAge(151);
    cout << "年龄：" << p.getAge() << endl;
    p.setLover("桃乃木香奈");
    return 0;
}
```

### 3、点和圆的关系-案例

```c++
#include <iostream>
using namespace std;

class Point  // 点类
{
public:
    void setX(int x)  //设置x坐标
    {
        m_X = x;
    }

    int getX()  //获取x坐标
    {
        return m_X;
    }

    void setY(int y)  //设置y坐标
    {
        m_Y = y;
    }

    int getY()  //获取y坐标
    {
        return m_Y;
    }

private:
    int m_X;
    int m_Y;
};

class Circle //圆类
{
public:
    void setR(int r)  //设置半径
    {
        m_R = r;
    }

    int getR()  //获取半径
    {
        return m_R;
    }

    void setCenter(Point center)  //设置圆心，圆心是点类型
    {
        m_Center = center;
    }

    Point getCenter()  //获取圆心
    {
        return m_Center;
    }

private:
    int m_R;
    Point m_Center;
};

void isInCircle(Circle &c, Point &p)
{
    int Distance = (p.getX() - c.getCenter().getX()) * (p.getX() - c.getCenter().getX()) +
                   (p.getX() - c.getCenter().getX()) * (p.getX() - c.getCenter().getX());
    int rDistance = c.getR() * c.getR();
    if (Distance = rDistance) cout << "点在圆上" << endl;
    if (Distance > rDistance) cout << "点在圆外" << endl;
    if (Distance < rDistance) cout << "点在圆内" << endl;
}

int main()
{
    Circle c;
    c.setR(10);
    Point center;
    center.setX(10);
    center.setY(0);
    c.setCenter(center);
    Point p;
    p.setX(10);
    p.setY(10);
    isInCircle(c, p);
    return 0;
}
```



--------

## 5.7

### 1、构造函数和析构函数

+ 构造函数：主要用于在创建对象时，为对象的成员属性赋值，构造函数由编译器自动调用，无需手动调用
+ 析构函数，主要用于在销毁对象前，也由系统自动调用，执行一些清理工作

**构造函数语法:**

1. 构造函数，没有返回值也不用写void

2. 函数名称与类名相同

3. 构造函数可以有参数，因此可以发生重载

4. 程序在调用对象时候会自动调用构造，无需手动调用，而且只会调用一次

**析构函数：**

1. 析构函数，没有返回值也不用写void
2. 函数名称与类名相同，在名称前加上符号~
3. 析构函数不可以有参数，因此不可以发生重载
4. 程序在对象销毁前会自动调用析构，无需手动调用，而且只会调用一次

```c++
#include <iostream>
using namespace std;

class Person
{
public:

    //构造和析构都是必须有的实现，如果自己不提供，编译器会提供一个空实现的构造和析构
    Person()  //构造函数
    {
        cout << "Person构造函数的调用" << endl;
    }

    ~Person()  //析构函数
    {
        cout << "Person析构函数的调用" << endl;
    }
};

void test01()
{
    Person p1;  //局部变量，test01函数执行完毕后，会释放这个对象，自动调用析构函数
}

int main()
{
    test01();  //构造和析构都调用了
    Person p2;  //只调用了构造，析构需要等main函数结束才会调用
    system("pause");
    return 0;
}
```



## 5.8

### 1、构造函数的分类及调用

两种分类方式：

+ 按参数划分：有参构造和无参构造
+ 按类型划分：普通构造和拷贝构造

三种调用方式：

+ 括号法
+ 显示法
+ 隐式转换法

```c++
#include <iostream>
using namespace std;

class Person
{
public:
    Person()  //无参构造
    {
        cout << "Person无参构造函数的调用" << endl;
    }

    Person(int a)  //有参构造
    {
        age = a;
        cout << "Person有参构造函数的调用" << endl;
    }

    Person(const Person &p)  //拷贝构造
    {
        age = p.age;  //将传入的人身上的所有属性，拷贝到我身上
        cout << "Person拷贝构造函数的调用" << endl;
    }

    ~Person()
    {
        cout << "Person析构函数的调用" << endl;
    }

    int age;
};

void test01()
{
    //1、括号法
    Person p1;  //默认构造函数的调用,注意这里不能加括号，编译器会以为是函数的声明
    Person p2(10);  //有参构造函数的调用
    Person p3(p2);  //拷贝构造函数

    //2、显示法
    Person p4;  //默认无参构造函数
    Person p5 = Person(10);  //有参构造
    Person p6 = Person(p5);  //拷贝构造
    //Person(10)；单独拿出来是匿名对象  特点：当前行执行结束后，系统会立即回收掉匿名对象
    //注意：不要利用拷贝构造来初始化一个匿名对象，编译器会认为Person(p3)相当于Person p3，会造成重定义

    //3、隐式转换法
    Person p7 = 10;  //有参构造，相当于Person p7 = Person(10);
    Person p8 = p7;  //拷贝构造，相当于Person p8 = Person(p7);
}

int main()
{
    test01();
    return 0;
}
```

### 2、拷贝构造函数的调用时机

C++中拷贝构造函数调用时机通常有三种情况：

+ 使用一个已经创建完毕的对象来初始化一个新对象
+ 值传递的方式给函数参数传值
+ 以值方式返回局部对象

```c++
#include <iostream>
using namespace std;

class Person
{
public:
    Person()
    {
        cout << "Person默认构造函数的调用" << endl;
    }

    Person(int age)
    {
        cout << "Person有参构造函数的调用" << endl;
        m_Age = age;
    }

    Person(const Person &p)
    {
        cout << "Person拷贝构造函数的调用" << endl;
        m_Age = p.m_Age;
    }

    ~Person()
    {
        cout << "Person析构函数的调用" << endl;
    }

    int m_Age;
};

void test01()  //1、使用一个已经创建完毕的对象来初始化一个新对象
{
    Person p1(20);
    Person p2(p1);
}

//2、值传递的方式给函数参数传值
void doWork(Person p)
{

}

void test02()
{
    Person p;
    doWork(p);
}

//3、值方式返回局部对象
Person doWork2()
{
    Person p1;
    cout << (long long) &p1 << endl;
    return p1;
}

void test03()
{
    Person p = doWork2();
    cout << (long long) &p << endl;
}

int main()
{
    test03();
    return 0;
}
```



---------

## 5.16

### 1、构造函数的调用规则

默认情况下，C++编译器至少给一个类添加3个函数

+ 默认构造函数(无参，函数体为空)

+ 默认析构函数(无参，函数体为空)

+ 默认拷贝构造函数，对属性进行值拷贝

构造函数的调用规则如下：

+ 如果用户定义有参构造函数，C++不再提供默认无参构造，但是会提供默认拷贝构造

+ 如果用户定义拷贝构造函数，C++不会再提供其他构造函数

    

### 2、深拷贝与浅拷贝

+ **浅拷贝**：

    - 浅拷贝是一种简单的复制操作，只复制对象的引用或指针，而不是复制对象内部的数据。

    - 复制后的对象与原始对象共享相同的数据，任何一个对象的改变都会影响到另一个对象。

    - 浅拷贝适用于简单的数据类型或只包含指针的对象，可以提高性能和节省内存。

    - 当对象包含动态分配的内存或资源时，浅拷贝可能导致浅层复制的对象和原始对象共享同一块内存或资源，可能引发潜在的问题，如多次释放同一块内存或资源。

        

+ **深拷贝：**

    - 深拷贝是一种复制对象及其内部数据的操作，创建了一个完全独立的对象和数据副本。

    - 复制后的对象与原始对象相互独立，对一个对象的修改不会影响到另一个对象。

    - 深拷贝适用于对象包含动态分配的内存、资源或其他对象的情况，确保每个对象都有自己的独立拷贝。

    - 深拷贝的实现通常需要递归遍历对象的内部数据结构，进行数据的逐个复制。

        

```c++
#include <iostream>
using namespace std;

class Person
{
public:
    Person()
    {
        cout << "Person默认构造函数的调用" << endl;
    }

    Person(int age, int height)
    {
        m_Age = age;
        m_Height = new int(height);
        cout << "Person有参构造函数的调用" << endl;
    }

    Person(const Person &p) //自己实现拷贝构造函数 解决浅拷贝带来的问题
    {
        m_Age = p.m_Age;
        // m_Height = p.m_Height; 浅拷贝(编译器默认实现)
        m_Height = new int(*p.m_Height);  //深拷贝操作
        cout << "Person拷贝构造函数的调用" << endl;
    }

    ~Person()
    {
        cout << "Person析构函数的调用" << endl;
        if (m_Height != nullptr)  //在析构函数中将堆区开辟的数据释放
        {
            delete m_Height;
            m_Height = nullptr;
        }
    }

    int m_Age;
    int *m_Height;
};

void test01()
{
    Person p1(18, 185);
    cout << "p1的年龄为: " << p1.m_Age << "  " << "身高为：" << *p1.m_Height << endl;
    Person p2(p1);
    cout << "p2的年龄为: " << p2.m_Age << "  " << "身高为：" << *p2.m_Height << endl;
}

int main()
{
    test01();
    return 0;
}
```



------------

## 5.17

### 1、初始化列表

+ C++提供了初始化列表语法，用来初始化属性

```c++
#include <iostream>
using namespace std;

class Person
{
public:

//    Person(int a, int b, int c)  //传统初始化操作
//    {
//        m_A = a;
//        m_B = b;
//        m_C = c;
//    }

    Person(int a, int b, int c) : m_A(a), m_B(b), m_C(c)  //利用初始化列表来初始化数据
    {

    }

    int m_A;
    int m_B;
    int m_C;
};

void test01()
{
    //Person p(10, 20, 30);
    Person p(30, 20, 10);
    cout << p.m_A << " " << p.m_B << " " << p.m_C << endl;
}

int main()
{
    test01();
    return 0;
}
```

### 2、类对象作为类成员

+ 当其他类对象作为本类成员，构造时候先构造类对象，再构造自身，而析构的顺序与构造相反

```c++
#include <iostream>
using namespace std;

class A
{
public:
    A()
    {
        cout << "A构造函数的调用" << endl;
    }

    ~A()
    {
        cout << "A析构函数的调用" << endl;
    }

};

class B
{
public:
    B()
    {
        cout << "B构造函数的调用" << endl;
    }

    ~B()
    {
        cout << "B析构函数的调用" << endl;
    }

    A a;
};

int main()
{
    B b;
    return 0;
}
```

### 3、静态成员

静态成员就是在成员变量和成员函数前加上关键字static，称为静态成员

+ 静态成员变量
    + 所有对象共享同一份数据
    + 在编译阶段分配内存
    + 类内声明，类外初始化

```c++
#include <iostream>
using namespace std;

class Person
{
public:
    static int m_A;  //类内声明
private:
    static int m_B;  //静态成员变量也是有访问权限的，类外无法访问private
};

//类外初始化
int Person::m_A = 100;
int Person::m_B = 200;

void test01()
{
    Person p;
    cout << p.m_A << endl;

    Person p2;
    p2.m_A = 200;
    cout << p.m_A << endl;  //输出200，因为修改的是同一份数据
}


void test02()
{
    //静态成员变量，不属于某个对象上，所有对象都共享同一份数据
    //因此静态成员变量有两种访问方式

    //1、通过对象进行访问
    Person p;
    cout << p.m_A << endl;
    //2、通过类名进行访问
    cout << Person::m_A << endl;
    //cout << Person::m_B << endl;

}

int main()
{
    //test01();
    test02();
    return 0;
}
```

+ 静态成员函数
    + 所有对象共享同一个函数
    + 静态成员函数只能访问静态成员变量

```c++
#include <iostream>
using namespace std;

class Person
{
public:
    static void func()
    {
        m_A = 100;  //静态成员函数可以访问静态成员变量
        //m_B = 100;  //静态成员函数 不可以访问 非静态成员变量
        cout << " static void func的调用" << endl;
    }

    static int m_A;  //静态成员变量
    int m_B;  //非静态成员变量
};

int Person::m_A = 0;

void test01()
{
    //1、通过对象访问
    Person p;
    p.func();

    //2、通过类名访问
    Person::func();
}

int main()
{
    test01();
    return 0;
}
```

### 4、C++对象模型和this指针

+ 成员变量和成员函数分开存储

    在C++中，类内的成员变量和成员函数分开存储，只有非静态成员变量才属于类的对象

```c++
#include <iostream>
using namespace std;

class Person
{
    //只有非静态成员属于类的对象上
    int m_A;         //非静态成员变量    属于类的对象上
    static int m_B;  //静态成员变量      不属于类的对象
    void func()      //非静态成员函数    不属于类对象上
    {

    }

    static void func2()  //非静态成员函数    不属于类对象上
    {

    }
};

int Person::m_B = 0;  //一定要记得静态成员变量类外要初始化

void test01()
{
    Person p;
    //空对象占用内存空间为：1
    //C++编译器会给每个空对象也分配一个字节空间，是为了区分空对象占内存的位置
    //每个空对象也应该有一个独一无二的内存地址
    cout << sizeof(p) << endl;
}

void test02()
{
    Person p;
    cout << sizeof(p) << endl;
}

int main()
{
    //test01();
    test02();
    return 0;
}
```



--------------



## 5.18

### 1、this指针概念

每个非静态成员函数只会诞生一份函数实例，也就是说多个同类型的对象会公用一块代码

那么问题是：这一块代码是如何区分是哪个对象调用自己的呢？



C++通过提供特殊的对象指针，this指针，解决上述问题。**this指针指向被调用的成员函数所属的对象**



this指针是隐含每一个非静态成员函数内的一种指针

this不需要定义，直接使用即可



this指针的用途：

+ 当形参和成员变量同名时，可用this指针来区分
+ 在类的非静态成员函数中返回对象本身，可使用return *this

```c++
#include <iostream>
using namespace std;

class Person
{
public:
    Person(int age)
    {
        this->age = age;  //this指针解决形参和成员变量同名的问题
    }

    int age;

    Person &PersonAddAge(Person &p)
    {
        this->age += p.age;
        return *this;  //this是指向p2的指针，而*this指向的就是p2这个对象本体
    }
};

void test01()
{
    Person p1(18);
    cout << "p1的年龄为：" << p1.age << endl;
}

void test02()
{
    Person p1(10);
    Person p2(10);

    p2.PersonAddAge(p1).PersonAddAge(p1).PersonAddAge(p1);  //链式编程思想
    cout << "p2的年龄为：" << p2.age << endl;
}

int main()
{
    //test01();
    test02();
    return 0;
}
```

### 2、空指针访问成员函数

C++中空指针也是可以调用成员函数的，但是爷爷要注意有没有用到this指针

如果用到this指针，需要加以判断保证代码的健壮性

```c++
#include <iostream>
using namespace std;

class Person
{
public:

    void showClassName()
    {
        cout << "this is Person class" << endl;
    }

    void showPersonAge()
    {
        if (this == NULL)  //提高健壮性
        {
            return;
        }

        cout << "age = " << m_Age << endl;
    }

    int m_Age;
};

void test01()
{
    Person *p = NULL;
    p->showClassName();
    p->showPersonAge();
}

int main()
{
    test01();
    return 0;
}
```

### 3、const修饰成员函数

**常函数：**

+ 成员函数后加const后称为常函数
+ 常函数内不可以修改成员属性
+ 成员属性声明时加关键字mutable后，在常函数中就可以修改了

**常对象：**

+ 声明对象前加const称该对象为常对象
+ 常对象只能调用常函数

```c++
#include <iostream>
using namespace std;

class Person
{
public:
    Person()
    {

    }

    //this指针的本质是指针常量，指针的指向是不可以修改的，相当于Person * const this;
    //如果在成员函数后面再加一个const，那么指针指向的值也不可以修改了，相当于const Person * const this;
    void showPerson() const //常函数
    {
        //m_A = 100;
        m_B = 100;
    }

    void func()
    {

    }

    int m_A;
    mutable int m_B;  //mutable实现特殊变量，使得常函数和常对象也可以修改这个值
};

//void test01()
//{
//    Person p;
//    p.showPerson();
//}

void test02()
{
    const Person p;  //在对象前加const，变为常对象
    //p.m_A = 100;
    p.m_B = 100;
    //常对象只能调用常函数
    p.showPerson();
    //p.func();  常对象不可以调用普通成员函数，因为普通成员函数可以修改属性，而常对象不允许修改属性
}

int main()
{
    test02();
    return 0;
}
```

### 4、全局函数做友元

```c++
#include <iostream>
using namespace std;

#include <string>

class Building
{
    friend void goodGay(Building *building); //全局函数做友元

public:
    Building()
    {
        m_LivingRoom = "客厅";
        m_BedRoom = "卧室";
    }

public:
    string m_LivingRoom;
private:
    string m_BedRoom;
};

void goodGay(Building *building)
{
    cout << "好基友的全局函数正在访问：" << building->m_LivingRoom << endl;
    //类中写了friend 可以访问private的属性了
    cout << "好基友的全局函数正在访问：" << building->m_BedRoom << endl;
}

void test01()
{
    Building building;
    goodGay(&building);
}

int main()
{
    test01();
    return 0;
}
```

### 5、类做友元

```c++
#include <iostream>
using namespace std;

#include <string>

class Building
{
    friend class GoodGay; //GoodGay是本类的friend，可以访问private

public:
    Building();

public:
    string m_LivingRoom;
private:
    string m_BedRoom;
};

//类外写成员函数
Building::Building()
{
    m_LivingRoom = "客厅";
    m_BedRoom = "卧室";
}

class GoodGay
{
public:

    GoodGay();

    void visit();

    Building *building;
};

GoodGay::GoodGay()
{
    building = new Building;
}

void GoodGay::visit()
{
    cout << "好基友类正在访问：" << building->m_LivingRoom << endl;
    cout << "好基友类正在访问：" << building->m_BedRoom << endl;
}


void test01()
{
    GoodGay gg;
    gg.visit();
}

int main()
{
    test01();
    return 0;
}
```

### 6、成员函数做友元

```c++
#include <iostream>
using namespace std;

#include <string>

class Building;

class GoodGay
{
public:
    GoodGay();

    void visit01();  //让visit01函数可以访问Building中的私有成员
    void visit02();  //让visit02函数不可以访问Building中的私有成员

    Building *building;

};

class Building
{
    friend void GoodGay::visit01();  //visit01成员函数作为friend，可以访问私有成员了

public:
    Building();

public:
    string m_LivingRoom;
private:
    string m_BedRoom;
};

//类外实现成员函数
Building::Building()
{
    m_LivingRoom = "客厅";
    m_BedRoom = "卧室";
}

GoodGay::GoodGay()
{
    building = new Building;
}

void GoodGay::visit01()
{
    cout << "visit01函数正在访问：" << building->m_LivingRoom << endl;
    cout << "visit01函数正在访问：" << building->m_BedRoom << endl;
}

void GoodGay::visit02()
{
    cout << "visit02函数正在访问：" << building->m_LivingRoom << endl;
    //cout << "visit02函数正在访问：" << building->m_BedRoom << endl;
}

void test01()
{
    GoodGay gg;
    gg.visit01();
    gg.visit02();
}

int main()
{
    test01();
    return 0;
}
```



---------

## 5.19

### 1、运算符重载

+ 运算符重载的概念：对已有的运算符重新进行定义，赋予其另一种功能，以适应不同的数据类型



#### 加号运算符重载

+ 作用：实现两个自定义数据类型相加的运算

+ 注意：
    + 对于内置的数据类型的表达式的运算符是不可能改变的
    + 不要滥用运算符重载(比如不要把＋号重载成相减的功能，别人看不懂)

```c++
#include <iostream>
using namespace std;

class Person
{
public:
    int m_A;
    int m_B;

    //1、成员函数重载+号
    Person operator+(Person &p)
    {
        Person temp;
        temp.m_A = this->m_A + p.m_A;
        temp.m_B = this->m_B + p.m_B;
        return temp;
    }

};

//2、全局函数重载+号
//Person operator+(Person &p1, Person &p2)
//{
//    Person temp;
//    temp.m_A = p1.m_A + p2.m_A;
//    temp.m_B = p1.m_B + p2.m_B;
//    return temp;
//}

//运算符重载+函数重载(实现Person+int)
Person operator+(Person &p1, int num)
{
    Person temp;
    temp.m_A = p1.m_A + num;
    temp.m_B = p1.m_B + num;
    return temp;
}

void test01()
{
    Person p1;
    p1.m_A = 10;
    p1.m_B = 20;

    Person p2;
    p2.m_A = 10;
    p2.m_B = 20;

    //Person p3 = p1.operator+(p2);  //成员函数重载+号的本质调用
    //Person p3 = operator+(p1, p2);  //全局函数重载+号的本质调用
    Person p3 = p1 + p2;  //重载+号后的简便调用
    Person p4 = p1 + 100;  //调用Person+int函数重载

    cout << p3.m_A << " " << p3.m_B << endl;
    cout << p4.m_A << " " << p4.m_B << endl;
}

int main()
{
    test01();
    return 0;
}
```

#### 左移运算符重载

作用：可以输出自定义数据类型

```c++
#include <iostream>
using namespace std;

class Person
{
public:

    //通常不会利用成员函数重载左移运算符，因为无法实现cout在p的左侧

    int m_A;
    int m_B;
};

//全局函数实现左移运算符的重载
ostream &operator<<(ostream &cout, Person &p)  //返回值仍然是ostream类，可以继续链式编程输出
{
    cout << "m_A=" << p.m_A << "  m_B=" << p.m_B;
    return cout;
}

void test01()
{
    Person p;
    p.m_A = 10;
    p.m_B = 20;
    //operator<<(cout, p);  //重载<<运算符的本质实现
    cout << p << endl;  //简化实现
}

int main()
{
    test01();
    return 0;
}
```



--------------

## 5.21

### 1、递增运算符重载

作用：通过重载递增运算符，实现自己的整型数据

注意：前置递增返回的是引用，后置递增返回的是值

```c++
#include <iostream>
using namespace std;

class MyInteger
{
    friend ostream &operator<<(ostream &cout, MyInteger myint);

public:
    MyInteger()
    {
        m_Num = 0;
    }

    //重载前置++运算符，返回引用是为了一直对同一个数据进行递增操作
    MyInteger &operator++()
    {
        m_Num++;
        return *this;
    }

    //重载后置++运算符,后置递增只能返回值，因为不能返回局部变量的引用
    MyInteger operator++(int) //int是占位参数，可以用于区分前置和后置递增
    {
        MyInteger temp = *this;
        m_Num++;
        return temp;
    }

private:
    int m_Num;
};

//重载<<运算符
ostream &operator<<(ostream &cout, MyInteger myint)
{
    cout << myint.m_Num;
    return cout;
}

void test01()
{
    MyInteger myint;
    cout << ++myint << endl;
    cout << myint << endl;
}

void test02()
{
    MyInteger myint;
    cout << myint++ << endl;
    cout << myint << endl;
}

int main()
{
    //test01();
    test02();
    return 0;
}
```

### 2、赋值运算符重载

作用：如果类中有属性指向堆区，重载赋值运算符采用深拷贝可以解决堆区内存重复释放的问题

```c++
#include <iostream>
using namespace std;

class Person
{
public:
    Person(int age)
    {
        m_Age = new int(age);
    }

    ~Person()
    {
        if (m_Age != NULL)
        {
            delete m_Age;
            m_Age = NULL;
        }
    }

    //重载赋值运算符,解决默认浅拷贝带来堆区内存重复释放的问题
    Person &operator=(Person &p)
    {
        //编译器是提供浅拷贝
        //m_Age = p.m_Age;

        //应该先判断是否有属性在堆区，如果有先释放干净，然后再深拷贝
        if (m_Age != NULL)
        {
            delete m_Age;
            m_Age = NULL;
        }
        m_Age = new int(*p.m_Age);  //深拷贝
        return *this;  //返回对象本身
    }

    int *m_Age;
};

void test01()
{
    Person p1(18);
    Person p2(20);
    Person p3(22);
    p3 = p2 = p1;
    cout << "p1的年龄为：" << *p1.m_Age << endl;
    cout << "p2的年龄为：" << *p2.m_Age << endl;
    cout << "p3的年龄为：" << *p2.m_Age << endl;
}

int main()
{
    test01();
    return 0;
}
```

### 3、关系运算符重载

作用：可以让来两个自定义类型对象进行对比操作

```c++
#include <iostream>
using namespace std;

#include <string>

class Person
{
public:
    Person(string name, int age)
    {
        m_Name = name;
        m_Age = age;
    }

    //重载关系运算符
    bool operator==(Person &p)
    {
        if (this->m_Name == p.m_Name && this->m_Age == p.m_Age)
        {
            return true;
        }
        return false;
    }


    string m_Name;
    int m_Age;
};

void test01()
{
    Person p1("Tom", 18);
    Person p2("Tom", 18);
    if (p1 == p2)
    {
        cout << "p1和p2是相等的！" << endl;
    } else
    {
        cout << "p1和p2是不相等的！" << endl;
    }
}

int main()
{
    test01();
    return 0;
}
```

### 4、函数调用运算符重载

+ 函数调用运算符()也可以重载 
+ 由于重载后使用的方式非常像函数的调用，因此称为仿函数
+ 仿函数没有固定写法，非常灵活

```c++
#include <iostream>
using namespace std;

#include <string>

class MyPrint
{
public:
    //重载函数调用运算符
    void operator()(string test)
    {
        cout << test << endl;
    }
};

void MyPrint02(string test)
{
    cout << test << endl;
}

void test01()
{
    MyPrint myPrint;
    myPrint("Hello World!");  //重载函数调用运算符，由于使用起来非常类似于函数调用，因此称为仿函数
    MyPrint02("Hello World!");  //真正的函数调用
}

class MyAdd
{
public:
    int operator()(int num1, int num2)
    {
        return num1 + num2;
    }
};

void test02()
{
    MyAdd myadd;
    //int res = myadd.operator()(100, 100);  //本质实现
    int res = myadd(100, 100);  //重载后的简化实现
    cout << res << endl;

    cout << MyAdd()(100, 100) << endl;  //匿名函数对象
}

int main()
{
    test01();
    test02();
    return 0;
}
```



-------------------

## 5.22

### 1、继承的基本语法

+ 继承的好处：减少重复代码

+ 子类也称为派生类

+ 父类也称为基类

**派生类中的成员，包含两大部分：**

一类是从基类继承过来的，一类是自己增加的成员。

从基类继承过来的表现其共性，而新增的成员提现了其个性。

```c++
#include <iostream>
using namespace std;

class Basepage
{
public:
    void header()
    {
        cout << "首页、公开课、登录、注册（公共头部）" << endl;
    }

    void footer()
    {
        cout << "帮助中心、交流合作、站内地图（公共底部）" << endl;
    }

    void left()
    {
        cout << "Java、Python、C++（公共分类列表）" << endl;
    }
};

//Java页面
class Java : public Basepage
{
public:
    void content()
    {
        cout << "Java学科视频" << endl;
    }
};

//Python页面
class Python : public Basepage
{
public:
    void content()
    {
        cout << "Python学科视频" << endl;
    }
};

//C++页面
class CPP : public Basepage
{
public:
    void content()
    {
        cout << "C++学科视频" << endl;
    }
};

void test01()
{
    cout << "Java视频下载页面" << endl;
    Java ja;
    ja.header();
    ja.footer();
    ja.left();
    ja.content();

    cout << "------------------" << endl;

    cout << "Python视频下载页面" << endl;
    Python py;
    py.header();
    py.footer();
    py.left();
    py.content();

    cout << "------------------" << endl;

    cout << "C++视频下载页面" << endl;
    CPP cpp;
    cpp.header();
    cpp.footer();
    cpp.left();
    cpp.content();
}

int main()
{
    test01();
    return 0;
}
```

### 2、继承方式

**继承方式一共有三种：**

+ 公共继承：父类中除了private之外，其他保持不变
+ 保护继承：父类中除了private之外，其他均变成protected权限
+ 私有继承：父类中除了private之外，其他均变成private权限

![image-20230522143503157](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20230522143503157.png)

```c++
#include <iostream>
using namespace std;

class Base1
{
public:
    int m_A;
protected:
    int m_B;
private:
    int m_C;
};

class Son1 : public Base1 //公共继承
{
public:
    void func()
    {
        m_A = 10; //父类中的公共权限成员，到子类中依然是公共权限
        m_B = 20; //父类中的保护权限成员，到子类中依然是保护权限
        //m_C = 30; //父类中的私有权限成员，子类访问不到
    }
};

void test01()
{
    Son1 s1;
    s1.m_A = 100; //公共权限 类内类外都可以访问
    //s1.m_B = 100; //保护权限 类外不可以访问
}


class Son2 : protected Base1 //保护继承
{
public:
    void func()
    {
        m_A = 10; //父类中的公共权限成员，到子类中变为保护权限
        m_B = 20; //父类中的保护权限成员，到子类中依然是保护权限
        //m_C = 30; //父类中的私有权限成员，子类访问不到
    }
};

void test02()
{
    Son2 s2;
    //s2.m_A = 10; //保护权限 类外不可以访问
}


class Son3 : private Base1 //私有继承
{
public:
    void func()
    {
        m_A = 10; //父类中的公共权限成员，到子类中变为私有权限
        m_B = 10; //父类中的保护权限成员，到子类中变为私有权限
        //m_C = 10; //父类中的私有权限成员，子类访问不到
    }
};

void test03()
{
    Son3 s3;
    //s3.m_A = 10; //到Son3中变为了私有成员 类外访问不到
}

class GrandSon3 : public Son3
{
public:
    void func()
    {
        //m_A = 10; //到Son3中，m_A是私有，即使是儿子也继承不了
    }
};

int main()
{

    return 0;
}
```

### 3、继承中的对象模型

利用开发人员命令提示工具查看对象模型：

+ 跳转盘符
+ 跳转文件路径 cd 具体路径
+ 查看此文件夹
+ cl /d1 reportSingleClassLayout类名 文件名

![image-20230522180841955](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20230522180841955.png)

```c++
#include <iostream>
using namespace std;

class Base
{
public:
    int m_A;
protected:
    int m_B;
private:
    int m_C;
};

class Son : public Base
{
public:
    int m_D;
};

void test01()
{   //父类中所有非静态成员属性都会被子类继承下去
    //父类中的私有成员属性，是被编译器给隐藏了，因此访问不到，但是确实被继承下去了
    cout << sizeof(Son) << endl;
}

int main()
{
    test01();
    return 0;
}
```

### 4、继承中构造和析构的顺序

```c++
#include <iostream>
using namespace std;

class Base
{
public:
    Base()
    {
        cout << "Base的构造函数调用！" << endl;
    }

    ~Base()
    {
        cout << "Base的析构函数调用！" << endl;
    }
};

class Son : public Base
{
public:
    Son()
    {
        cout << "Son的构造函数调用！" << endl;
    }

    ~Son()
    {
        cout << "Son的析构函数调用！" << endl;
    }
};

void test01()
{
    //先构造父类，再构造子类
    //先析构子类，再析构父类
    Son s;
}

int main()
{
    test01();
    return 0;
}
```



------------



## 5.23

### 1、继承同名成员处理方式

问题：当子类和父类出现同名的成员，如何通过子类对象，访问到子类或父类中同名的数据呢？

+ 访问子类同名成员：直接访问即可
+ 访问父类同名成员：需要加作用域

```c++
#include <iostream>
using namespace std;

class Base
{
public:
    Base()
    {
        m_A = 100;
    }

    void func()
    {
        cout << "Base-func的调用" << endl;
    }

    void func(int a)
    {
        cout << "Son-func(int a)的调用" << endl;
    }

    int m_A;
};

class Son : public Base
{
public:
    Son()
    {
        m_A = 200;
    }

    void func()
    {
        cout << "Son-func()的调用" << endl;
    }


    int m_A;
};

void test01()
{
    Son s;
    cout << s.m_A << endl;
    cout << s.Base::m_A << endl; //如果通过子类对象访问父类中同名成员，需要加作用域
}

void test02()
{
    Son s;
    s.func();
    s.Base::func();
    //s.func(10); //如果子类中出现和父类同名的成员函数，子类的同名成员会隐藏掉父类中所有同名成员函数
    s.Base::func(10);  //需要加作用域
}

int main()
{
    test02();
    return 0;
}
```



### 2、继承中的同名静态成员处理

```c++
#include <iostream>
using namespace std;

class Base
{
public:
    static int m_A; //类内声明

    static void func()
    {
        cout << "Base - static void func()" << endl;
    }
};

int Base::m_A = 100; //类外初始化

class Son : public Base
{
public:
    static int m_A;

    static void func()
    {
        cout << "Son - static void func()" << endl;
    }
};

int Son::m_A = 200;

//同名静态成员属性
void test01()
{
    //1、通过对象访问
    Son s;
    cout << s.m_A << endl;
    cout << s.Base::m_A << endl;

    //2、通过类名访问
    cout << Son::m_A << endl;
    cout << Son::Base::m_A << endl;//第一个::代表通过类名方式访问，第二个::代表是父类作用域下
}


//同名静态成员函数
void test02()
{
    Son s;
    //1、通过对象访问
    s.func();
    s.Base::func();
    
    //2、通过类名访问
    Son::func();
    Son::Base::func();
}

int main()
{
    //test01();
    test02();
    return 0;
}
```



### 3、多继承语法

C++允许一个类继承多个类

多继承可能会引发父类中有同名成员出现，需要加作用域区分

**C++实际开发中不建议使用多继承**

```c++
#include <iostream>
using namespace std;

class Base1
{
public:
    Base1()
    {
        m_A = 100;
    }

    int m_A;
};

class Base2
{
public:
    Base2()
    {
        m_A = 200;
    }

    int m_A;
};

class Son : public Base1, public Base2 //多继承语法
{
public:
    Son()
    {
        m_C = 300;
        m_D = 400;
    }

    int m_C;
    int m_D;
};

void test01()
{
    Son s;
    cout << sizeof(s) << endl;
    //当父类中出现同名成员，需要加作用域区分
    cout << s.Base1::m_A << endl;
    cout << s.Base2::m_A << endl;
}

int main()
{
    test01();
    return 0;
}
```



### 4、菱形继承(钻石继承)

+ 菱形继承带来的主要问题是继承两份相同的数据，导致资源浪费，毫无意义
+ 利用虚继承可以解决菱形继承问题
```c++
#include <iostream>
using namespace std;

class Animal //动物类
{
public:
    int m_Age;
};

//利用虚继承可以解决菱形继承问题
//继承之前 加上关键字virtual 变为虚继承
//Animal类称为虚基类
class Sheep : virtual public Animal//羊类
{

};

class Camel : virtual public Animal //驼类
{

};

class Alpaca : public Sheep, public Camel //羊驼类
{

};

void test01()
{
    Alpaca a;
    a.Sheep::m_Age = 18;
    a.Camel::m_Age = 250;
    //使用虚继承之后，相当于m_Age的数据就只有一份了，是共享的
    cout << a.Sheep::m_Age << endl;
    cout << a.Camel::m_Age << endl;
    cout << a.m_Age << endl;
}

int main()
{
    test01();
    return 0;
}
```



--------------------------

## 5.24

### 1、多态的基本概念



**多态是C++面向对象三大特性之一**



**多态分为两类：**

+ 静态多态：函数重载 和 运算符重载都属于今天多态，服用函数名
+ 动态多态：派生类和虚函数实现运行时多态



**静态多态和动态多态的区别：**

+ 静态多态的函数地址早绑定 - 编译阶段确定函数地址
+ 动态多态的函数地址晚绑定 - 运行阶段确定函数地址

```c++
#include <iostream>
using namespace std;

class Animal
{
public:
    virtual void speak() //虚函数
    {
        cout << "动物在说话" << endl;
    }
};

class Cat : public Animal
{
public:
    //函数重写：函数返回值类型，函数名称，参数列表完全相同
    void speak() //子类重写函数的virtual可写可不写
    {
        cout << "小猫在说话" << endl;
    }
};

class Dog : public Animal
{
public:
    void speak()
    {
        cout << "小狗在说话" << endl;
    }
};

//地址早绑定，在编译器阶段确定函数地址
//如果想执行让猫说话，那么这个函数地址就不能提前绑定，需要在运行阶段进行绑定(地址晚绑定)

//动态多态满足条件：
//1、有继承关系
//2、子类要重写父类的虚函数

//动态多态的使用：父类的指针或者引用指向子类对象
void doSpeak(Animal &animal)
{
    animal.speak();
}

void test01()
{
    Cat cat;
    doSpeak(cat);

    Dog dog;
    doSpeak(dog);
}

int main()
{
    test01();
    return 0;
}
```



### 2、多态案例——计算器类

**案例描述：**

分别利用普通写法和多态技术，实现设计两个操作数进行运算的计算器类

**多态的优点：**

+ 代码组织结构清晰
+ 可读性强
+ 利于前期和后期的扩展以及维护

```c++
#include <iostream>
using namespace std;

#include <string>

//普通写法实现计算器
class Calculator
{
public:
    float getResult(string oper)
    {
        if (oper == "+")
        {
            return m_Num1 + m_Num2;
        }
        else if (oper == "-")
        {
            return m_Num1 - m_Num2;
        }
        else if (oper == "*")
        {
            return m_Num1 * m_Num2;
        }
        else if (oper == "/")
        {
            return m_Num1 / m_Num2;
        }
        //如果想扩展新的功能，需要修改源码
        //在真实开发中，提倡开闭原则：对扩展进行开放，对修改进行关闭
    }

    float m_Num1;
    float m_Num2;
};

//利用多态实现计算器
class AbstractCalcalator
{
public:
    virtual int getResult()
    {
        return 0;
    }

    float m_Num1;
    float m_Num2;
};

//加法计算器类
class AddCalculator : public AbstractCalcalator
{
public:
    int getResult()
    {
        return m_Num1 + m_Num2;
    }
};

//减法计算器类
class SubCalculator : public AbstractCalcalator
{
public:
    int getResult()
    {
        return m_Num1 - m_Num2;
    }
};

//乘法计算器类
class MulCalculator : public AbstractCalcalator
{
public:
    int getResult()
    {
        return m_Num1 * m_Num2;
    }
};

void test01()
{
    Calculator c;
    c.m_Num1 = 20;
    c.m_Num2 = 10;
    cout << c.getResult("+") << endl;
    cout << c.getResult("-") << endl;
    cout << c.getResult("*") << endl;
    cout << c.getResult("/") << endl;
}

void test02()
{
    //加法运算
    AbstractCalcalator *abc = new AddCalculator; //new开辟在堆区
    abc->m_Num1 = 10; //类对象时指针对象，需要用->指向类中成员
    abc->m_Num2 = 20;
    cout << abc->getResult() << endl;
    delete abc; //堆区数据手动开辟，手动释放

    //减法运算
    abc = new SubCalculator;
    abc->m_Num1 = 20; //类对象时指针对象，需要用->指向类中成员
    abc->m_Num2 = 10;
    cout << abc->getResult() << endl;
    delete abc; //堆区手动开辟，手动释放

    //乘法运算
    abc = new MulCalculator;
    abc->m_Num1 = 20; //类对象时指针对象，需要用->指向类中成员
    abc->m_Num2 = 10;
    cout << abc->getResult() << endl;
    delete abc; //堆区手动开辟，手动释放

}

int main()
{
    //test01();
    test02();
    return 0;
}
```



### 3、纯虚函数和抽象类

在多态中，通常父类中虚函数的实现是毫无意义的，主要都是调用子类重写的内容

因此可以将虚函数改为**纯虚函数**

当类中有了纯虚函数，这个类也称为**抽象类**



**抽象类的特点：**

+ 无法实例化对象
+ 子类必须重写抽象类中的纯虚函数，否则也属于抽象类

```c++
#include <iostream>
using namespace std;

class Base
{
public:
    virtual void func() = 0; //纯虚函数
};

class Son : public Base
{
public:
    virtual void func()
    {
        cout << "func函数的调用" << endl;
    }
};

void test01()
{
    //抽象类无法实例化对象，无论是在栈区还是堆区
    //Base b;
    //new Base;
    Son s; //子类必须重写父类中的纯虚函数，否则无法实例化对象
    Base *b = new Son;
    b->func();
}

int main()
{
    test01();
    return 0;
}
```

### 4、多态案例——制作饮品

```c++
#include <iostream>
using namespace std;

class AbstractDrinking
{
public:
    virtual void Boil() = 0; //煮水

    virtual void Brew() = 0; //冲泡

    virtual void PourInCup() = 0; //倒入杯中

    virtual void PutSomething() = 0; //加入辅料

    void MakeDrink() //整体制作流程
    {
        Boil();
        Brew();
        PourInCup();
        PutSomething();
    }
};

class Coffee : public AbstractDrinking
{
    //煮水
    virtual void Boil()
    {
        cout << "煮农夫山泉" << endl;
    }

    //冲泡
    virtual void Brew()
    {
        cout << "冲泡咖啡" << endl;
    }

    //倒入杯中
    virtual void PourInCup()
    {
        cout << "倒入咖啡杯中" << endl;
    }

    //加入辅料
    virtual void PutSomething()
    {
        cout << "加入糖和牛奶" << endl;
    }
};

//制作红茶

class Tea : public AbstractDrinking
{
    //煮水
    virtual void Boil()
    {
        cout << "煮矿泉水" << endl;
    }

    //冲泡
    virtual void Brew()
    {
        cout << "冲泡茶叶" << endl;
    }

    //倒入杯中
    virtual void PourInCup()
    {
        cout << "倒入玻璃杯中" << endl;
    }

    //加入辅料
    virtual void PutSomething()
    {
        cout << "加入枸杞" << endl;
    }
};

void doWork(AbstractDrinking *abs)
{
    abs->MakeDrink();
}

void test01()
{
    doWork(new Coffee);
    cout << "----------------" << endl;
    doWork(new Tea);

}

int main()
{
    test01();
    return 0;
}
```



## 5.25

### 1、虚析构和纯虚析构



**问题：**多态使用时，如果子类中有属性开辟到堆区，那么父类指针在释放时无法调用到子类的析构代码，堆区数据会造成内存泄露



**解决方式：**将父类中的析构函数改为虚析构或者纯虚析构



**虚析构和纯虚析构共性：**

+ 可以解决父类指针释放子类对象
+ 都需要有具体的函数实现

**虚析构和纯虚析构区别：**

+ 如果是纯虚析构，该类属于抽象类，无法实例化对象

```c++
#include <iostream>
using namespace std;

#include <string>

class Animal
{
public:
    Animal()
    {
        cout << "Animal构造函数的调用" << endl;
    }

    //利用虚析构可以解决，父类指针释放子类对象时，内存泄露的问题
//    virtual ~Animal()
//    {
//        cout << "Animal虚析构函数的调用" << endl;
//    }

    //纯虚析构，需要声明，也需要实现
    //有了纯虚析构之后，这个类就属于抽象类，无法实例化对象
    virtual ~Animal() = 0;

    //纯虚函数
    virtual void speak() = 0;
};

//纯虚析构的实现
Animal::~Animal()
{
    cout << "Animal纯虚析构函数的调用" << endl;
}

class Cat : public Animal
{
public:
    Cat(string name)
    {
        cout << "Cat构造函数的调用" << endl;
        m_Name = new string(name);
    }

    ~Cat()
    {
        if (m_Name != NULL)
        {
            cout << "Cat析构函数调用" << endl;
            delete m_Name;
            m_Name = NULL;
        }
    }

    void speak()
    {
        cout << *m_Name << "小猫在说话" << endl;
    }

    string *m_Name;
};

void test01()
{
    Animal *animal = new Cat("Tom");
    animal->speak();
    //父类指针在析构的时候，不会调用子类的析构函数，导致子类中如果有开辟在堆区的属性，会出现内存泄露
    delete animal;
}

int main()
{
    test01();
    return 0;
}
```

总结：

1. 虚析构或纯虚析构就是用来解决父类指针释放子类对象
2. 如果子类中没有堆区数据，可以不写虚析构或纯虚析构
3. 拥有纯虚析构函数的类也属于抽象类



## 5.26

### 1、多态案例三——电脑组装

```c++
#include <iostream>
using namespace std;

//抽象CPU类
class CPU
{
public:
    virtual void calculate() = 0;
};

//抽象GPU类
class VideoCard
{
public:
    virtual void display() = 0;
};

//抽象内存条类
class Memory
{
public:
    virtual void storage() = 0;
};

//电脑类
class Computer
{
public:
    Computer(CPU *cpu, VideoCard *vc, Memory *mem)
    {
        m_cpu = cpu;
        m_vc = vc;
        m_mem = mem;
    }

    //利用Computer的析构函数来释放堆区的电脑零件
    ~Computer()
    {
        if (m_cpu != NULL)
        {
            delete m_cpu;
            m_cpu = NULL;
        }

        if (m_vc != NULL)
        {
            delete m_vc;
            m_vc = NULL;
        }

        if (m_mem != NULL)
        {
            delete m_mem;
            m_mem = NULL;
        }
    }

    void work()
    {
        m_cpu->calculate();
        m_vc->display();
        m_mem->storage();
    }

    CPU *m_cpu;
    VideoCard *m_vc;
    Memory *m_mem;
};

//配件厂商

//Intel
class IntelCPU : public CPU
{
public:
    void calculate()
    {
        cout << "Intel的CPU正在计算！" << endl;
    }
};

class IntelVideoCard : public VideoCard
{
public:
    void display()
    {
        cout << "Intel的显卡正在显示！" << endl;
    }
};

class IntelMemory : public Memory
{
public:
    void storage()
    {
        cout << "Intel的内存条正在存储！" << endl;
    }
};

//AMD
class AMDCPU : public CPU
{
public:
    void calculate()
    {
        cout << "AMD的CPU正在计算！" << endl;
    }
};

class AMDVideoCard : public VideoCard
{
public:
    void display()
    {
        cout << "AMD的显卡正在显示！" << endl;
    }
};

class AMDMemory : public Memory
{
public:
    void storage()
    {
        cout << "AMD的内存条正在存储！" << endl;
    }
};

void test01()
{
    //第一台电脑零件
    CPU *intelCpu = new IntelCPU;
    VideoCard *intelCard = new IntelVideoCard;
    Memory *interMemory = new IntelMemory;

    cout << "第一台电脑开始工作：" << endl;
    //创建第一台电脑
    Computer *computer1 = new Computer(intelCpu, intelCard, interMemory);
    computer1->work();
    delete computer1;

    cout << "-------------------------------" << endl;

    cout << "第二台电脑开始工作：" << endl;
    //创建第二台电脑
    Computer *computer2 = new Computer(new AMDCPU, new AMDVideoCard, new AMDMemory);
    computer2->work();
    delete computer2;
}

int main()
{
    test01();
    return 0;
}
```

### 2、文件操作

程序运行时产生的数据都属于临时数据，程序一旦运行结束都会被释放

通过**文件可以将数据持久化**

C++中对文件操作需要包含头文件<fstream>



文件类型分为两种：

1. **文本文件**      - 文件以文本的ASCII码形式存储在计算机中
2. **二进制文件**  - 文件以文本的**二进制形式**存储在计算机中



操作文件的三大类：

1. ofstream:写操作
2. ifstream：读操作
3. fstream：读写操作

#### 文本文件

##### 写文件

写文件步骤如下：

1. 包含头文件

    #include<fstream>

2. 创建流对象

    ofstream ofs;

3. 打开文件

    of.open("文件路径"，打开方式);

4. 写数据

    ofs<<"写入的数据"

5. 关闭文件

    ofs.close();

    | 打开方式    | 解释                       |
    | ----------- | -------------------------- |
    | ios::in     | 为读文件而打开文件         |
    | ios::out    | 为写文件而打开文件         |
    | ios::ate    | 初试位置：文件尾           |
    | ios::app    | 追加方式写文件             |
    | ios::trunc  | 如果文件存在先删除，在创建 |
    | ios::binary | 二进制方式                 |

```c++
#include <iostream>
using namespace std;
//1、包含头文件
#include <fstream>

void test01()
{   //2、创建流对象
    ofstream ofs;
    //3、制定打开方式
    ofs.open("test.txt", ios::out);
    //4、写内容
    ofs << "姓名：张三" << endl;
    ofs << "性别：男" << endl;
    ofs << "年龄：18" << endl;
    //5、关闭文件
    ofs.close();
}

int main()
{
    test01();
    return 0;
}
```

总结：

+ 文件操作必须包含头文件fstream

+ 读文件可以利用ofstream,或者fstream类

+ 打开文件时候需要制定操作文件的路径，以及打开方式

+ 利用<<可以想文件中写数据

+ 操作完毕，要关闭文件

    

##### 读文件

读文件与写文件步骤相似，但是读取方式相对比较多



读文件步骤如下：

1. 包含头文件

    #include<fstream>

2. 创建流对象

    ifstream ifs;

3. 打开文件并判断文件是否打开成功

    ifs.open("文件路径",打开方式)

4. 读数据

    四种方式读取

5. 关闭文件

    ifs.close();

```c++
#include <iostream>
using namespace std;
//1、包含头文件
#include <fstream>
#include <string>

void test01()
{
    //2、创建流对象
    ifstream ifs;
    //3、打开文件并判断文件是否打开成功
    ifs.open("test.txt", ios::in);
    if (!ifs.is_open())
    {
        cout << "文件打开失败！" << endl;
        return;
    }
    //4、读数据(四种方式)

    //第一种
//    char buf[1024] = {0};
//    while (ifs >> buf)
//    {
//        cout << buf << endl;
//    }

    //第二种
//    char buf[1024] = {0};
//    while (ifs.getline(buf, sizeof(buf)))
//    {
//        cout << buf << endl;
//    }

    //第三种
//    string buf;
//    while (getline(ifs, buf))
//    {
//        cout << buf << endl;
//    }

    //第四种
    char c;
    while ((c = ifs.get()) != EOF) //EOF end of file
    {
        cout << c;
    }

    //5、关闭文件
    ifs.close();
}

int main()
{
    test01();
    return 0;
}
```

总结：

+ 读文件可以利用ifstream，或者fstream类
+ 利用is_open函数可以判断文件是否打开成功
+ close关闭文件



#### 二进制文件

以二进制的方式对文件进行读写操作

打开方式要制定为ios::binary



##### 写文件

二进制方式写文件主要利用流对象调用成员函数write

函数原型：

```c++
ostream& write(const char* buffer,int len);
```

参数解释：字符指针buffer指向内存中的一段存储空间，len是读写的字节数



##### 读文件

二进制方式读文件主要利用流对象调用成员函数read

函数原型：

```c++
istream& read(char *buffer,int len);
```

参数解释：字符指针buffer指向内存中的一段存储空间，len是读写的字符数

```c++
#include <iostream>
using namespace std;

#include <fstream>

class Person
{
public:
    char m_Name;
    int m_Age;
};

void test01()
{
    ifstream ifs;
    ifs.open("Person.txt", ios::in | ios::binary);
    if (!ifs.is_open())
    {
        cout << "打开文件失败" << endl;
        return;
    }
    Person p;
    ifs.read((char *) &p, sizeof(Person));
    cout << p.m_Name << ' ' << p.m_Age << endl;
    ifs.close();
}

int main()
{
    test01();
    return 0;
}
```



------------------

## 5.27

### 1、CMake的基本使用

+ 项目不要使用中文名！

+ project（）括号里面放目标名称，最后的可执行文件(exe)也叫这个名称
+ add_executable（）括号里面第一个参数要填和project（）括号里一样的目标名称，后面再把.h和.cpp文件全部加进去，从而构建项目



---

## 5.31

### 1、函数模板

+ C++的另一种编程思想——泛型编程，主要利用的技术就是模板
+ C++提供两种模板机制：**函数模板**和**类模板**

#### 函数模板语法

函数模板作用：

建立一个通用函数，其函数返回值类型和形参类型可以不具体制定，用一个虚拟的类型来代表。



语法：

```c++
temeplate<typename T>
函数声明或定义
```

解释：

template --- 声明创建模板

typename --- 表明其后面的符号是一种数据类型，可以用class代替

T --- 通用的数据类型，名称可以替换，通常为大写字母

```c++
#include <iostream>
using namespace std;

//交换两个整型的函数
void Swapint(int &a, int &b)
{
  int temp = a;
  a = b;
  b = temp;
}

//交换两个浮点型函数
void Swapdouble(double &a, double &b)
{
  double temp = a;
  a = b;
  b = temp;
}

template<typename T>

void Swap(T &a, T &b)
{
  T temp = a;
  a = b;
  b = temp;
}

void test01()
{
  int a = 10;
  int b = 20;
  //Swapint(a, b);

  //利用函数模板
  //两种方式

  //1、自动类型推导
  //Swap(a, b);

  //1、显示指定类型
  Swap<int>(a, b);

  cout << a << " " << b << endl;

//  double c = 1.1;
//  double d = 2.2;
//  Swapdouble(c, d);
//  cout << c << " " << d << endl;
}

int main()
{
  test01();
  return 0;
}
```

####  函数模板注意事项

+ 自动类型推导，必须推导出一致的数据类型T，才可以使用
+ 模板必须要确定出T的数据类型，才可以使用

```c++
#include <iostream>
using namespace std;

//交换函数模板
template<class T>
void Swap(T &a, T &b)
{
    T temp = a;
    a = b;
    b = temp;
}

//简单选择排序模板
template<class T>
void Sort(T arr[], int len)
{
    for (int i = 0; i < len; i++)
    {
        int max = i;
        for (int j = i + 1; j < len; j++)
        {
            if (arr[max] < arr[j])
            {
                max = j;
            }
        }
        if (max != i)
        {
            Swap(arr[max], arr[i]);
        }
    }
}

//打印数组函数模板
template<class T>
void PrintArray(T arr[], int len)
{
    for (int i = 0; i < len; i++)
    {
        cout << arr[i] << " ";
    }
    cout << endl;
}

void test01()
{
    char charArr[] = "badcfe";
    int num = sizeof(charArr) / sizeof(char);
    Sort(charArr, num);
    PrintArray(charArr, num);
}

void test02()
{
    int intArr[] = {7, 5, 1, 3, 9, 2, 4, 6, 8};
    int num = sizeof(intArr) / sizeof(int);
    Sort(intArr, num);
    PrintArray(intArr, num);
}
int main()
{
    test01();
    test02();
    return 0;
}
```



--------------



# 2023.6



## 6.1

### 1、普通函数和函数模板的区别

+ 普通函数调用时可以发生自动类型转换（隐式类型转换）
+ 函数模板调用时，如果利用自动类型推导，不会发生隐式类型转换；如果利用显式指定类型的方式，可以发生隐式类型转换

```c++
#include <iostream>
using namespace std;

//普通函数
int myAdd01(int a, int b)
{
    return a + b;
}

//函数模板
template<class T>
T myAdd02(T a, T b)
{
    return a + b;
}

void test01()
{
    int a = 10;
    int b = 20;
    char c = 'c'; //ASCII码 a-97 c-99
    cout << myAdd01(a, c) << endl;

    //自动类型推导，不可以发生隐式类型转换
    //cout << myAdd02(a, c) << endl;

    //显式指定类型,可以发生隐式类型转换
    cout << myAdd02<int>(a, c) << endl;
}

int main()
{
    test01();
    return 0;
}
```



### 2、普通函数和函数模板的调用规则



调用规则如下：

1. 如果函数模板和普通函数都可以调用，优先调用普通函数
2. 可以通过空模板参数列表来强制实现调用函数模板
3. 函数模板也可以发生重载
4. 如果函数模板可以产生更好的匹配，优先调用函数模板

```c++
#include <iostream>
using namespace std;

void myPrint(int a, int b)
{
    cout << "调用的普通函数" << endl;
}

template<class T>
void myPrint(T a, T b)
{
    cout << "调用的模板" << endl;
}

template<class T>
void myPrint(T a, T b, T c) //函数模板也可以发生函数重载
{
    cout << "调用重载的模板" << endl;
}

void test01()
{
    int a = 10;
    int b = 20;

    //如果函数模板和普通函数都可以调用，优先调用普通函数
    myPrint(a, b);

    //通过空模板参数列表，强制调用函数模板
    myPrint<>(a, b);

    //如果函数模板可以产生更好的匹配，优先调用函数模板
    char c1 = 'a';
    char c2 = 'b';
    myPrint(c1, c2);
}

int main()
{
    test01();
    return 0;
}
```



### 3、模板的局限性

+ 利用具体化的模板，可以解决自定义数据类型的通用化
+ 学习模板并不是为了写模板，而是为了在STL中能够运用系统提供的模板

```c++
#include <iostream>
using namespace std;
#include <string>

class Person
{
 public:
  Person(string name, int age)
  {
      this->m_Name = name;
      this->m_Age = age;
  }
  string m_Name;
  int m_Age;
};

template<class T>
bool myCompare(T &a, T &b)
{
    if (a == b)
    {
        return true;
    } else
    {
        return false;
    }
}

//利用具体化Person的版本实现代码，会优先调用
template<>
bool myCompare(Person &p1, Person &p2)
{
    if (p1.m_Name == p2.m_Name && p1.m_Age == p2.m_Age)
    {
        return true;
    } else
    {
        return false;
    }
}

void test01()
{
    int a = 10;
    int b = 20;
    bool ret = myCompare(a, b);
    if (ret)
    {
        cout << "a==b" << endl;
    } else
    {
        cout << "a!=b" << endl;
    }
}
void test02()
{
    Person p1("Tom", 10);
    Person p2("Tom", 10);

    bool ret = myCompare(p1, p2);
    if (ret)
    {
        cout << "p1==p2" << endl;
    } else
    {
        cout << "p2!=p2" << endl;
    }
}
int main()
{
    //test01();
    test02();
    return 0;
}
```



### 4、类模板的语法

类模板和函数模板语法相似，在声明模板template后面加类，此类称为类模板

```c++
#include <iostream>
using namespace std;
#include <string>

template<class NameType, class AgeType>
class Person
{
public:
    Person(NameType name, AgeType age)
    {
        this->m_Name = name;
        this->m_Age = age;
    }
    void ShowPerson()
    {
        cout << this->m_Name << endl;
        cout << this->m_Age << endl;
    }
    NameType m_Name;
    AgeType m_Age;
};

void test01()
{
    Person<string, int> p1("孙悟空", 99);
    p1.ShowPerson();
}

int main()
{
    test01();
    return 0;
}
```



### 4、类模板和函数模板区别

 

类模板和函数模板区别主要有两点：

1. 类模板没有自动类型推导的使用方式
2. 类模板在模板参数列表中可以有默认参数(C++17标准已经支持)

```c++
//
// Created by Here on 2023/6/1.
//

#include <iostream>
using namespace std;
#include <string>

template<class NameType, class AgeType=int> //类模板在模板参数列表中可以有默认参数
class Person
{
public:
    Person(NameType name, AgeType age)
    {
        this->m_Name = name;
        this->m_Age = age;
    }
    void ShowPerson()
    {
        cout << this->m_Name << endl;
        cout << this->m_Age << endl;
    }
    NameType m_Name;
    AgeType m_Age;
};

//类模板没有自动类型推导使用方式（其实C++17标准已经支持了)
void test01()
{
    Person<string, int> p1("孙悟空", 1000);
    Person p2("孙悟空", 1000);
    p2.ShowPerson();
}

void test02()
{
    Person<string> p("猪八戒", 999); //只传入第一个string,第二个int采用默认参数
    p.ShowPerson();
}

int main()
{
    test01();
    test02();
    return 0;
}
```



### 5、类模板中成员函数创建时机

类模板中成员函数和普通类中成员函数创建时机是有区别的：

+ 普通类中的成员函数一开始就可以创建
+ 类模板中的成员函数在调用时才创建

```c++
#include <iostream>
using namespace std;

class Person1
{
public:
    void showPerson1()
    {
        cout << "Person1 show" << endl;
    }
};

class Person2
{
public:
    void showPerson2()
    {
        cout << "Person2 show" << endl;
    }
};

template<class T>
class Myclass
{
public:
    T obj;

    //类模板中的成员函数
    void func1()
    {
        obj.showPerson1();
    }

    void func2()
    {
        obj.showPerson2();
    }

};

void test01()
{
    Myclass<Person1> m;
    m.func1();
    //m.func2();
}

int main()
{
    test01();
    return 0;
}
```



### 6、类模板对象做函数参数

一共有三种传入方式：

+ 指定传入的类型  --- 直接显示对象的数据类型（使用比较广泛）
+ 参数模板化          --- 将对象中的参数变为模板进行传递
+ 整个类模板化      --- 将这个对象类型 模板化进行传递

```c++
#include <iostream>
using namespace std;
#include <string>
#include <typeinfo>

template<class T1, class T2>
class Person
{
public:
    Person(T1 name, T2 age)
    {
        this->m_Name = name;
        this->m_Age = age;
    }

    void showPerson()
    {
        cout << this->m_Name << endl;
        cout << this->m_Age << endl;
    }

    T1 m_Name;
    T2 m_Age;
};

//1、指定传入类型
void printPerson1(Person<string, int> &p)
{
    p.showPerson();
}

void test01()
{
    Person<string, int> p("孙悟空", 500);
    printPerson1(p);
}

//2、参数模板化
template<class T1, class T2>
void printPerson2(Person<T1, T2> &p)
{
    p.showPerson();
}

void test02()
{
    Person<string, int> p("猪八戒", 99);
    printPerson2(p);
}

//3、整个类模板化
template<class T1>
void printPerson3(T1 &p)
{
    p.showPerson();
    cout << typeid(T1).name() << endl;
}

void test03()
{
    Person<string, int> p("唐僧", 100);
    printPerson3(p);
}

int main()
{
    test01();
    test02();
    test03();
    return 0;
}
```



-----------



## 6.2

### 1、类模板与继承

当类模板碰到继承时，需要注意以下几点：

+ 当子类继承的父类是一个类模板时，子类在声明的时候，要指定出父类中T的类型
+ 如果不指定，编译器无法给子类分配内存
+ 如果想灵活指定出父类中T的类型，子类也需变为类模板

```c++
#include <iostream>
using namespace std;
#include <typeinfo>

template<class T>
class Base
{
    T m;
};

class Son1 : public Base<int> //必须要知道父类中T的类型，才能继承给子类
{

};

template<class T1, class T2>
class Son2 : public Base<T2> //如果想灵活指定父类中T类型，子类也需要变为类模板
{
public:
    Son2()
    {
        cout << typeid(T1).name() << endl;
        cout << typeid(T2).name() << endl;
    }
    T1 obj;
};

void test01()
{
    Son1 s1;
    Son2<int, char> s2;
}

int main()
{
    test01();
    return 0;
}
```



### 2、类模板成员函数的类外实现

```c++
//
// Created by Here on 2023/6/2.
//

#include <iostream>
using namespace std;

template<class T1, class T2>
class Person
{
public:
    Person(T1 name, T2 age);
//    {
//        this->m_Name = name;
//        this->m_Age = age;
//    }

    void showPerson();
//    {
//        cout << this->m_Name << endl;
//        cout << this->m_Age << endl;
//    }
    T1 m_Name;
    T2 m_Age;
};

//构造函数的类外实现
template<class T1, class T2>
Person<T1, T2>::Person(T1 name, T2 age)
{
    this->m_Name = name;
    this->m_Age = age;
}

//成员函数的类外实现
template<class T1, class T2>
void Person<T1, T2>::showPerson()
{
    cout << this->m_Name << endl;
    cout << this->m_Age << endl;
}

void test01()
{
    Person<string, int> p("Tom", 20);
    p.showPerson();
}
int main()
{
    test01();
    return 0;
}
```



### 3、类模板分文件编写



问题：

+ 类模板中成员函数创建时机是在调用阶段，导致分文件编写时链接不到

解决方式：

+ 1、直接包含.cpp源文件
+ 2、将声明和实现写到同一个文件中，并更改后缀名为.hpp，hpp是约定俗成的名称（主流解决方法）



**类模板分文件编写.cpp**

```c++
#include <iostream>
using namespace std;
//1、直接包含源文件
#include "Person.cpp"

//2、将.h和.cpp中的内容写到一起，将后缀名改为.hpp文件
#include "Person.hpp"
```



**Person.hpp**

```c++
#pragma once

#include <iostream>
using namespace std;
#include <string>

template<class T1, class T2>
class Person
{
public:

    Person(T1 name, T2 age);

    void showPerson();

    T1 m_Name;
    T2 m_Age;
};

//构造函数的类外实现
#include "Person.hpp"

template<class T1, class T2>
Person<T1, T2>::Person(T1 name, T2 age)
{
    this->m_Name = name;
    this->m_Age = age;
}

//成员函数的类外实现
template<class T1, class T2>
void Person<T1, T2>::showPerson()
{
    cout << this->m_Name << endl;
    cout << this->m_Age << endl;
}
```



### 4、类模板与友元

+ 全局函数类内实现 ：直接在类内声明友元即可
+ 全局函数类外实现：需要提前让编译器知道全局函数的存在





## 6.4

### 1、STL的诞生

+ 长久以来，软件界一直希望建立一种**可重复利用**的东西
+ C++的**面向对象**和**泛型编程**思想，目的就是提高复用性
+ 大多是情况下，数据结构和算法都未能有一套标准，导致被迫从事大量重复工作
+ 为了建立**数据结构**和**算法**的一套标准，诞生了STL



### 2、STL基本概念

+ STL(Standard Template Library,标准模板库)
+ STL从广义上分为：**容器(container)**，算法(algorithm)，**迭代器(iterator)**
+ **容器**和**算法**之间通过**迭代器**进行无缝连接
+ STL几乎所有代码都采用了**类模板**或者**函数模板**



### 3、STL六大组件

STL大体分为六大组件：**容器、算法、迭代器、仿函数、适配器(配接器)、空间配置器**



1. 容器：各种数据结构，如vector、list、deque、set、map等，用来存放数据
2. 算法：各种常用的算法，如sort、find、copy、for_each等
3. 迭代器：扮演了容器与算法之间的胶合剂
4. 仿函数：行为类似函数，可作为算法的某种策略
5. 适配器：一种用来修饰容器、仿函数或者迭代器接口的东西
6. 空间配置器：负责空间的配置与管理



### 4、STL中容器、算法、迭代器



**容器：**

STL容器就是将运用**最广泛的一些数据结构**实现出来

常用的数据结构：数组、链表、树、栈、队列、集合、映射表等

这些容器分为**序列式容器**和**关联式容器**两种：

+ **序列式容器：**强调值的排序，序列式容器中的每个元素均有固定的位置

+ **关联式容器：**二叉树结构，各元素之间没有严格的物理上的顺序关系



**算法：**

有限的步骤，解决逻辑或数学上的问题

算法分为：质变算法和**非质变算法**

+ **质变算法：**运算过程中会更改区间内元素的内容，例如拷贝、替换、删除等

+ **非质变算法：**运算过程中不会更改区间内的元素内容，例如查找、计数、遍历、寻找极值等



**迭代器：**

提供一种方法，使之能够依序寻访某个容器所含的各个元素，而又无需暴露该容器的内部表示方式。

每个容器都有自己专属的迭代器。

迭代器的使用非常类似于指针，初学阶段可以先理解迭代器为指针



迭代器种类：

![image-20230604151655881](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20230604151655881.png)



------------

## 6.11

### 1、vector存放内置数据类型

```c++
#include <iostream>
using namespace std;
#include <vector>
#include <algorithm>

void myPrint(int val)
{
    cout << val << endl;
}

void test01()
{
    //创建了一个vector容器，类似数组
    vector<int> v;

    //向容器中插入数据
    v.push_back(1);
    v.push_back(2);
    v.push_back(3);
    v.push_back(4);
    v.push_back(5);

    //通过迭代器访问容器中的数据
    vector<int>::iterator itBegin = v.begin(); //起始迭代器，指向容器中第一个元素
    vector<int>::iterator itEnd = v.end(); //结束迭代器，指向容器中最后一个元素的下一个位置

    //第一种遍历方式
    while (itBegin != itEnd)
    {
        cout << *itBegin << endl;
        itBegin++;
    }

    cout << endl;
    
    //第二种遍历方式
    for (vector<int>::iterator it = v.begin(); it != v.end(); it++)
    {
        cout << *it << endl;
    }

    cout << endl;

    //第三种遍历方式，利用STL提供的遍历算法
    for_each(v.begin(), v.end(), myPrint);

}
int main()
{
    test01();
    return 0;
}
```



### 2、vector存放自定义数据类型

```c++
#include <iostream>
using namespace std;
#include <vector>
#include <algorithm>

class Person
{
public:
    Person(string name, int age)
    {
        this->m_Name = name;
        this->m_Age = age;
    }
    string m_Name;
    int m_Age;
};

//存放自定义的数据类型
void test01()
{
    vector<Person> v;
    Person p1("aaa", 10);
    Person p2("bbb", 20);
    Person p3("ccc", 30);
    Person p4("ddd", 40);
    Person p5("eee", 50);

    //向容器中添加数据
    v.push_back(p1);
    v.push_back(p2);
    v.push_back(p3);
    v.push_back(p4);
    v.push_back(p5);

    //遍历容器中的数据
    for (vector<Person>::iterator it = v.begin(); it != v.end(); it++)
    {
        //cout << (*it).m_Name << " " << (*it).m_Age << endl; //解引用
        cout << it->m_Name << " " << it->m_Age << endl; //直接利用指针
    }

}

//存放自定义数据类型的指针
void test02()
{
    vector<Person *> v;
    Person p1("aaa", 10);
    Person p2("bbb", 20);
    Person p3("ccc", 30);
    Person p4("ddd", 40);
    Person p5("eee", 50);

    //向容器中添加数据
    v.push_back(&p1);
    v.push_back(&p2);
    v.push_back(&p3);
    v.push_back(&p4);
    v.push_back(&p5);

    //遍历容器
    for (vector<Person *>::iterator it = v.begin(); it != v.end(); it++)
    {
        cout << (*it)->m_Name << " " << (*it)->m_Age << endl;
    }
}

int main()
{
    //test01();
    test02();
    return 0;
}
```



### 3、vector容器嵌套容器

```c++
#include <iostream>
using namespace std;
#include <vector>

void test01()
{
    vector<vector<int>> v;

    //创建小容器
    vector<int> v1;
    vector<int> v2;
    vector<int> v3;
    vector<int> v4;

    //向小容器中添加数据
    for (int i = 0; i < 4; i++)
    {
        v1.push_back(i + 1);
        v2.push_back(i + 2);
        v3.push_back(i + 3);
        v4.push_back(i + 4);
    }

    //将小容器插入到大容器中
    v.push_back(v1);
    v.push_back(v2);
    v.push_back(v3);
    v.push_back(v4);

    //通过大容器遍历所有数据
    for (vector<vector<int>>::iterator it = v.begin(); it != v.end(); it++)
    {
        for (vector<int>::iterator vit = (*it).begin(); vit != (*it).end(); vit++)
        {
            cout << *vit << " ";
        }
        cout << endl;
    }
}

int main()
{
    test01();
    return 0;
}
```



### 4、string基本概念

**本质：**

+ string是C++风格的字符串，本质上是一个类

    

**string和char*的区别：**

+ char*是一个指针

+ string是一个类，类内部封装了char\*，管理这个字符串，是一个char\*型的容器

    

**特点：**

+ string类内部封装了很多成员方法，例如查找find，拷贝copy，删除delete，替换replace，插入insert
+ string管理char*所分配的内存，不用担心复制越界和取值越界等问题，由类内部负责解决



### 5、string的构造函数

```c++
#include <iostream>
using namespace std;

void test01()
{
    string s1; //默认构造，创建一个空的字符串

    const char *str = "Hello World";
    string s2(str); //使用字符串初始化
    cout << s2 << endl;

    string s3(s2); //拷贝构造
    cout << s3 << endl;

    string s4(10, 'a'); //创建10个a
    cout << s4 << endl;
}

int main()
{
    test01();
    return 0;
}
```



### 6、string赋值操作

```c++
#include <iostream>
using namespace std;

void test01()
{
    string str1;
    str1 = "Hello World"; //直接等号+字符串
    cout << str1 << endl;

    string str2;
    str2 = str1; //用别的字符串等号赋值
    cout << str2 << endl;

    string str3;
    str3 = 'a'; //单个字符等号赋值
    cout << str3 << endl;

    string str4;
    str4.assign("Hello C++"); //利用assign将另一个字符串赋值给当前字符串
    cout << str4 << endl;

    string str5;
    str5.assign("Hello C++", 5); //利用assign将另一个字符串的前n个字符赋值给当前字符串
    cout << str5 << endl;

    string str6;
    str6.assign(str5); //利用assign来复制另一个字符串
    cout << str6 << endl;

    string str7;
    str7.assign(10, 'b'); //利用assign赋值n个字符
    cout << str7 << endl;
}

int main()
{
    test01();
    return 0;
}
```



### 7、string字符串拼接

```c++
#include <iostream>
using namespace std;

void test01()
{
    string str1 = "我";
    str1 += "爱玩游戏";
    cout << str1 << endl;\

    string str2 = "I";
    str2.append(" love you");
    cout << str2 << endl;
}

int main()
{
    test01();
    return 0;
}
```



------------



## 6.12

### 1、string查找和替换

```c++
#include <iostream>
using namespace std;

//查找
void test01()
{
    string str1 = "abcdefgde";

    //find是从左往右查找
    int pos = str1.find("de");
    if (pos == -1)
    {
        cout << "未找到该字符串！" << endl;
    }
    else
    {
        cout << "找到该字符串，下标为：" << pos << endl;
    }

    //rfind是从右往左查找(但是下标依然是从左往右的)
    pos = str1.rfind("de");
    cout << pos << endl;
}

//替换
void test02()
{
    string str1 = "abcdefgde";

    //从下标1位置开始的3个字符替换为"1111"
    str1.replace(1, 3, "1111");
    cout << str1 << endl;
}

int main()
{
    //test01();
    test02();
    return 0;
}
```



### 2、string字符串比较

```c++
#include <iostream>
using namespace std;

void test01()
{
    string str1 = "hello";
    string str2 = "hello";

    if (str1.compare(str2) == 0)
    {
        cout << "str1等于str2！" << endl;
    }
    else
    {
        cout << "str1不等于str2！" << endl;
    }

}

int main()
{
    test01();
    return 0;
}
```



### 3、string字符存取

```c++
#include <iostream>
using namespace std;

void test01()
{
    string str = "hello";
    cout << str << endl;

    //1、通过[]访问单个字符
    for (int i = 0; i < str.size(); i++)
    {
        cout << str[i] << " ";
    }
    cout << endl;
    //2、通过at方式访问单个字符
    for (int i = 0; i < str.size(); i++)
    {
        cout << str.at(i) << " ";
    }
    cout << endl;

    //修改单个字符
    str[0] = 'x';
    cout << str << endl;
    str.at(1) = 'x';
    cout << str << endl;

}

int main()
{
    test01();
    return 0;
}
```



### 4、string插入和删除

```c++
#include <iostream>
using namespace std;

void test01()
{
    string str = "hello";

    //插入
    str.insert(1, "111");
    cout << str << endl;

    //删除
    str.erase(1, 3);
    cout << str << endl;
}

int main()
{
    test01();
    return 0;
}
```



### 5、string子串

```c++
#include <iostream>
using namespace std;

void test01()
{
    string email = "zhangsan@qq.com";

    int pos = email.find("@");
    string userName = email.substr(0, pos);
    cout << userName << endl;
}

int main()
{
    test01();

    return 0;
}
```



### 6、vector基本概念

**功能：**

+ vector和数组非常相似，也称为单端数组



**vector和普通数组的区别：**

+ 数组是静态空间，而vector可以动态扩展



**动态扩展：**

+ 并不是在原空间之后续接新空间，而是找到更大的内存空间，然后将原数据拷贝到新空间，再释放原空间



### 7、vector构造函数

```c++
#include <iostream>
using namespace std;
#include <vector>

void printVector(vector<int> &v)
{
    for (vector<int>::iterator it = v.begin(); it < v.end(); it++)
    {
        cout << *it << " ";
    }
    cout << endl;
}

void test01()
{
    //默认构造，无参
    vector<int> v1;
    for (int i = 0; i < 10; i++)
    {
        v1.push_back(i);
    }
    printVector(v1);

    //通过区间方式进行构造，传两个迭代器到参数中
    vector<int> v2(v1.begin(), v1.end());
    printVector(v2);

    //n个elem方式构造(10个100)
    vector<int> v3(10, 100);
    printVector(v3);

    //拷贝构造
    vector<int> v4(v3);
    printVector(v4);
}

int main()
{
    test01();
    return 0;
}
```



## 6.20

### 1、vector容量和大小

```c++
#include <iostream>
using namespace std;
#include <vector>

void printVector(vector<int> &v)
{
    for (vector<int>::iterator it = v.begin(); it != v.end(); it++)
    {
        cout << *it << " ";
    }
    cout << endl;
}

void test01()
{
    vector<int> v1;
    for (int i = 0; i < 10; i++)
    {
        v1.push_back(i);
    }
    printVector(v1);

    if (v1.empty())
    {
        cout << "v1为空！" << endl;
    }
    else
    {
        cout << "v1不为空！" << endl;
        cout << "v1的容量为：" << v1.capacity() << endl;
        cout << "v1的大小为：" << v1.size() << endl;
    }

    //重新指定大小
    v1.resize(15, 100); //如果resize比原本的长，默认用0填充新的位置(重载版本可以实现用100填充空余位置)
    printVector(v1);

    v1.resize(5); //如果resize比原本短，会截断多余部分
    printVector(v1);
}

int main()
{
    test01();
    return 0;
}

```



### 2、vector插入和删除

```c++
#include <iostream>;
using namespace std;
#include <vector>

void printVector(vector<int> &v)
{
    for (vector<int>::iterator it = v.begin(); it != v.end(); it++)
    {
        cout << *it << " ";
    }
    cout << endl;
}
void test01()
{
    vector<int> v1;

    //尾插法
    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);
    v1.push_back(40);
    v1.push_back(50);

    //遍历
    printVector(v1);

    //尾删
    v1.pop_back();
    printVector(v1);

    //插入
    v1.insert(v1.begin(), 100); //在头部插入100
    printVector(v1);
    v1.insert(v1.begin(), 2, 1000); //在头部插入2个1000
    printVector(v1);

    //删除
    v1.erase(v1.begin()); //删除头部第一个数
    printVector(v1);

    //v1.erase(v1.begin(), v1.end()); //从头到尾删除
    v1.clear(); //清空
    printVector(v1);

}

int main()
{
    test01();
    return 0;
}
```



### 3、vector数据存取

```c++
#include <iostream>
using namespace std;
#include <vector>

void test01()
{
    vector<int> v1;
    for (int i = 0; i < 10; i++)
    {
        v1.push_back(i);
    }

    //利用[]方式访问元素中数组
    for (int i = 0; i < v1.size(); i++)
    {
        cout << v1[i] << " ";
    }
    cout << endl;

    //利用at方式访问元素
    for (int i = 0; i < v1.size(); i++)
    {
        cout << v1.at(i) << " ";
    }
    cout << endl;

    //获取第一个元素
    cout << "第一个元素为：" << v1.front() << endl;

    //获取最后一个元素
    cout << "最后一个元素为：" << v1.back() << endl;
}

int main()
{
    test01();
    return 0;
}
```



### 4、vector互换

```c++
#include <iostream>
using namespace std;
#include <vector>

void printVector(vector<int> &v)
{
    for (vector<int>::iterator it = v.begin(); it != v.end(); it++)
    {
        cout << *it << " ";
    }
    cout << endl;
}

//基本使用
void test01()
{
    vector<int> v1;
    for (int i = 0; i < 10; i++)
    {
        v1.push_back(i);
    }

    cout << "交换前：" << endl;
    printVector(v1);

    vector<int> v2;
    for (int i = 10; i > 0; i--)
    {
        v2.push_back(i);
    }
    printVector(v2);

    cout << "交换后：" << endl;
    v1.swap(v2);
    printVector(v1);
    printVector(v2);
}

//巧用swap可以收缩内存空间
void test02()
{
    vector<int> v;
    for (int i = 0; i < 100000; i++)
    {
        v.push_back(i);
    }

    cout << "v的容量为：" << v.capacity() << endl;
    cout << "v的大小为：" << v.size() << endl;

    v.resize(3); //resize容量不会变，就会导致浪费出现

    cout << "v的容量为：" << v.capacity() << endl;
    cout << "v的大小为：" << v.size() << endl;

    //巧用swap收缩内存
    vector<int>(v).swap(v); //创建一个匿名对象，然后交换，匿名对象会被自动回收

    cout << "v的容量为：" << v.capacity() << endl;
    cout << "v的大小为：" << v.size() << endl;

}

int main()
{
    //test01();
    test02();
    return 0;
}
```



### 5、预留空间

```c++
#include <iostream>
using namespace std;
#include <vector>

void test01()
{
    vector<int> v;
    v.reserve(100000);
    int num = 0;
    int *p = NULL;
    for (int i = 0; i < 100000; i++)
    {
        v.push_back(i);
        if (p != &v[0])
        {
            p = &v[0];
            num++;
        }
    }
    cout << num << endl;
}

int main()
{
    test01();
    return 0;
}
```














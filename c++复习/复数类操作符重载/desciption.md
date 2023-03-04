# 复数类操作符重载

## Description

实现复数的操作符重载，你需要做的是，将complex.h文件的函数声明，全部在complex.cpp中实现
 函数的声明如下：

```cpp
class COMPLEX
{
public:
    COMPLEX(double r = 0, double i = 0); // 构造函数
    COMPLEX(const COMPLEX &other);       // 拷贝构造函数
    void print();                        // 打印复数
                                         // 重载加法运算符（二元）
    COMPLEX operator+(const COMPLEX &other);
    // 重载减法运算符（二元）
    COMPLEX operator-(const COMPLEX &other);
    COMPLEX operator-(); // 重载求负运算符（一元）
                         // 重载赋值运算符（二元）
    COMPLEX & operator=(const COMPLEX &other);
    COMPLEX & operator++();     //重载前置++
    COMPLEX operator++(int);     //重载后置++
    COMPLEX & operator--();        //重载前置--
    COMPLEX operator--(int);        //重载后置--
protected:
    double real, image; // 复数的实部与虚部
};
输出格式为：
1+2i
-5-6i
-5-6i
-4-5i
-4-5i
-5-6i
-6-7i
-6-7i
-5-6i
-5-6i
```

main.cpp

```cpp
#include <vector>
#include <numeric>
#include <iostream>
#include<cstdlib>
#include "COMPLEX.h"
using namespace std;

int main()
{
    COMPLEX c1(1, 2); 
    COMPLEX c2(2);  
    COMPLEX c3(c1);   

    c3.print();  
    c1 = c1 + c2 + c3; 
    c2 = -c3;    
    c3 = c2 - c1;  
    c3.print();  

    COMPLEX temp= c3++;
    temp.print();
    c3.print();

    temp=c3--;
    temp.print();
    c3.print();

    temp=--c3;
    temp.print();
    c3.print();

    temp=++c3;
    temp.print();
    c3.print();   
   


    return 0;
}
```

COMPLEX.h

```cpp
#ifndef COMPLEX_H
#define COMPLEX_H

class COMPLEX
{
public:
	COMPLEX(double r = 0, double i = 0); 
	COMPLEX(const COMPLEX &other);		 
	void print();						 
										 
	COMPLEX operator+(const COMPLEX &other);

	COMPLEX operator-(const COMPLEX &other);
	COMPLEX operator-(); 
	COMPLEX operator=(const COMPLEX &other);
  
	COMPLEX &operator++();  
	COMPLEX operator++(int); 
	COMPLEX &operator--();   
	COMPLEX operator--(int); 
protected:
	double real, image; 
};
#endif
```
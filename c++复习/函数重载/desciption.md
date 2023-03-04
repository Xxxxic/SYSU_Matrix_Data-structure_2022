# 函数重载

## Description

写出3组Plus函数的声明与实现，类型分别为int，double，string，并在函数中分别输出"It's from int!"，"It's from double!"，"It's from string!"

## Sample Input

```
2 3
2.4 3.5
birth day
```

## Sample Output

```
It's from int!
5
It's from double!
5.9
It's from string!
birthday
```

main.cpp：

```cpp
#include<iostream>
#include"fun.h"
using namespace std;
int main(){
	int i1,i2;
	cin>>i1>>i2;
	cout<<Plus(i1,i2)<<endl;
	double d1,d2;
	cin>>d1>>d2;
	cout<<Plus(d1,d2)<<endl;
	string s1,s2;
	cin>>s1>>s2;
	cout<<Plus(s1,s2)<<endl;
	return 0;
}
```
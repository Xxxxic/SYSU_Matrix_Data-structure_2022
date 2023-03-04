# 实现一个简单point类

## Description

实现一个point类，它具有以下特征：

- point有一个静态数据成员，count，记录了一共创建了多少个point对象
- point有两个基本属性x，y分别记录了x和y轴的坐标，x，y的初始值为0；
- point有一个方法，judge可以判断三个点是否在一条直线上
- point可以打印出点的坐标(x,y)

## Sample Input

```
1 1
2 2
3 3
```

## Sample Output

```
(1,1)
1
True
3
```

main.cpp：

```cpp
#include <iostream>
#include "point.h"
using namespace std;

int main ( )
{
    double x,y;
    cin>>x>>y;
    point p1(x,y);
    p1.print();
    cout<<point::count<<endl;
    cin>>x>>y;
    point p2(x,y);
    cin>>x>>y;
    point p3(x,y);
    if(p1.judge(p2,p3)){
    	cout<<"True"<<endl;
	}
	else{
		cout<<"False"<<endl;
	}
	cout<<point::count<<endl;
    return 0;
}
```
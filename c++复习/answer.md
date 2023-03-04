---
title: answer
date: 2023-01-10T20:47:08Z
lastmod: 2023-01-10T21:04:23Z
---



# 实现一个简单point类

```cpp
class point{
	public:
		point(double x=0,double y=0){
			this->x=x;
			this->y=y;
			count++;
		}
		static int count;
		void print(){
			std::cout<<'('<<x<<','<<y<<')'<<std::endl;
		}
		bool judge(const point &p1,const point &p2){
			double dx1=p1.x-x;
			double dx2=p2.x-x;
			double dy1=p1.y-y;
			double dy2=p2.y-y;
			if(dx1==0&&dx2==0){
				return true;
			}
			else if(dx1==0||dx2==0){
				return false;
			}
			else if(dy1/dx1==dy2/dx2){
				return true;
			}
			else{
				return false;
			}
		}
	private:
		double x;
		double y;
};
int point::count=0;

```

## my answer

```cpp
#include <iostream>
using namespace std;

class point{
public:
    static int count;
    double x=0;
    double y=0;
    point(double x_,double y_):x(x_),y(y_){
        count++;
    }
    ~point(){
        count--;
    }
    void print(){
        cout<<'('<<x<<','<<y<<')'<<endl;
    }
    bool judge(point& p1,point& p2){
        return (p1.y-y)/(p1.x-x)==(p2.y-y)/(p2.x-x);
    }
};
int point::count=0;
```

‍

# 函数重载

```cpp
#include<iostream>
using namespace std;
int Plus(int a,int b){
	cout<<"It's from int!"<<endl;
	return a+b;
}
double Plus(double a,double b){
	cout<<"It's from double!"<<endl;
	return a+b;
}
string Plus(string a,string b){
	cout<<"It's from string!"<<endl;
	return a+b;
}
```

## my answer

```cpp
#include<iostream>
#include<string>
#include<iomanip>
using namespace std;


string Plus(int a,int b){
    string c="It's from int!\n";
    string d=to_string(a+b);
    return c+d;
}
string Plus(double a,double b){
    string c="It's from double!\n";
    string d=to_string(a+b);
    d = d.substr(0, d.find_last_not_of('0') + 1);
    return c+d;
}
string Plus(string a,string b){
    string c="It's from string!\n";
    string d=a+b;
    return c+d;
}
```

‍

# 复数类操作符重载

```cpp
#include"COMPLEX.h"
#include<iostream>
using namespace std;
COMPLEX::COMPLEX(double r,double i){
  real=r;
  image=i;
}
COMPLEX::COMPLEX(const COMPLEX &other){
  real=other.real;
  image=other.image;
}
void COMPLEX::print(){
  if(real==0&&image==0)
    cout<<'0'<<endl;
  else if(real==0){
    if(image==1)
    cout<<"i"<<endl;
    else
    cout<<image<<"i"<<endl;
  }
  else if(image==0)
    cout<<real<<endl;
  else{
    if(image==1)
     cout<<real<<"+"<<"i"<<endl;
    else
     cout<<real<<showpos<<image<<"i"<<endl;
  }
}
COMPLEX COMPLEX::operator+(const COMPLEX &other){
  COMPLEX tem;
  tem.real=real+other.real;
  tem.image=image+other.image;
  return tem;
}
COMPLEX COMPLEX::operator-(const COMPLEX &other){
  COMPLEX tem;
  tem.real=real-other.real;
  tem.image=image-other.image;
  return tem;
}
COMPLEX COMPLEX::operator-(){
  COMPLEX tem;
  tem.real=-real;
  tem.image=-image;
  return tem;
}
COMPLEX COMPLEX::operator=(const COMPLEX &other){
  real=other.real;
  image=other.image;
  return *this;
}
COMPLEX &COMPLEX::operator++(){
  real++;
  image++;
  return *this;
}
COMPLEX COMPLEX::operator++(int ){
  COMPLEX tem=*this;
  real++;
  image++;
  return tem;
}
COMPLEX &COMPLEX::operator--(){
  real--;
  image--;
  return *this;
}
COMPLEX COMPLEX::operator--(int){
  COMPLEX tem=*this;
  real--;
  image--;
  return tem;
}  

```

## my answer

```cpp
#include <vector>
#include <numeric>
#include <iostream>
#include<cstdlib>
#include "COMPLEX.h"
using namespace std;\


COMPLEX::COMPLEX(double r, double i):real(r),image(i) {}
COMPLEX::COMPLEX(const COMPLEX &o):real(o.real),image(o.image) {}
void COMPLEX::print(){
    if(real){
        if(image>=0)
            cout<<real<<"+"<<image<<"i"<<endl;
        else
            cout<<real<<image<<"i"<<endl;
    }
    else{
        if(image>=0)
            cout<<image<<"i"<<endl;
        else
            cout<<image<<"i"<<endl;
    }
}	 
                                      
COMPLEX COMPLEX::operator+(const COMPLEX &other){
    return COMPLEX(real+other.real,image+other.image);
}

COMPLEX COMPLEX::operator-(const COMPLEX &other){
    return COMPLEX(real-other.real,image-other.image);
}
COMPLEX COMPLEX::operator-(){
    return COMPLEX(-real,-image);
}
COMPLEX COMPLEX::operator=(const COMPLEX &other){
    real=other.real;
    image=other.image;
    return *this;
}

COMPLEX& COMPLEX::operator++(){
    real++;
    image++;
    return *this;
}
COMPLEX COMPLEX::operator++(int){
    COMPLEX temp=*this;
    real++;
    image++;
    return temp;
}
COMPLEX& COMPLEX::operator--(){
    real--;
    image--;
    return *this;
}   
COMPLEX COMPLEX::operator--(int){
    COMPLEX temp=*this;
    real--;
    image--;
    return temp;
}

```

‍

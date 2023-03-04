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
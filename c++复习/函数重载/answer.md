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
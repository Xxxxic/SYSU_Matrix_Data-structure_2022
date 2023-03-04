---
title: answer
date: 2023-01-10T20:46:42Z
lastmod: 2023-01-10T21:00:22Z
---

# answer

# Bracket Matching括号匹配

```cpp
//Bracket Matching

#include<iostream>
#include<stack>
using namespace std;
bool IsMatching(string &s){
    int sz=s.size();
    stack<char> cstack; 
    for(int i=0;i<sz;i++){
        if(s[i]=='{'||s[i]=='('||s[i]=='[')
            cstack.push(s[i]);
        else if(s[i]=='}'){
            if(cstack.empty())
                return false;
            if(cstack.top()=='{')
                cstack.pop();
            else
                return false;
        }
        else if(s[i]==')'){
            if(cstack.empty())
                return false;
            if(cstack.top()=='(')
                cstack.pop();
            else
                return false;
        }
        else if(s[i]==']'){
            if(cstack.empty())
                return false;
            if(cstack.top()=='[')
                cstack.pop();
            else
                return false;
        }
    }
    if(cstack.empty())
        return true;
    return false;
}
int main(){
    string s;
    cin>>s;
    if(IsMatching(s))
     cout<<"Yes";
    else
        cout<<"No";
  
    return 0;
}
```

## my answer

```cpp
#include<iostream>
#include<stack>
using namespace std;

int main(){
    string str;
    cin>>str;
    stack<char> s;
    if(str=="}"){
        cout<<"No";
        return 0;
    }
    for(int i=0;i<str.length();++i){
        if(str[i]=='('||str[i]=='['||str[i]=='{'){
            s.push(str[i]);
        }
        else if(str[i]==')'||str[i]==']'||str[i]=='}'){
            if((str[i]==')'&&s.top()!='(')||(str[i]==']'&&s.top()!='[')||(str[i]=='}'&&s.top()!='{')){
                break;
            }
            else{
                s.pop();
            }
        }
    }
    if(s.empty())
        cout<<"Yes";
    else  
        cout<<"No";
    return 0;
}
```

‍

# 中缀表达式转后缀表达

```cpp
#include<iostream>
#include<cstring>
#include<cstdio>
#include<stack>
using namespace std;

stack<char> zhan;
char s[1000];
int cd,ls1,ls2;



int main()
{
while(scanf("%[^\n]",&s)!=EOF)
{
	getchar();
	cd=strlen(s);
	for (int i=0;i<=cd-1;i++)
	if ((s[i]>=65&&s[i]<=90)||(s[i]>=97&&s[i]<=122)) printf("%c",s[i]);
	else{
		if (s[i]=='(') zhan.push(s[i]);
		else if (s[i]==')'){
			while (zhan.top()!='('){
				printf("%c",zhan.top());
				zhan.pop();
			}
			zhan.pop();
		}
		else if (s[i]=='*'||s[i]=='/'){
			while (zhan.empty()!=1&&zhan.top()!='('&&(zhan.top()=='*'||zhan.top()=='/')){
				printf("%c",zhan.top());
				zhan.pop();
			}
			zhan.push(s[i]);
		}
		else{
			while (zhan.empty()!=1&&zhan.top()!='('){
				printf("%c",zhan.top());
				zhan.pop();
			}
			zhan.push(s[i]);
		}
	}

	while (zhan.empty()!=1){
		printf("%c",zhan.top());
		zhan.pop();
	}

	printf("\n");
}
}
```

## my answer

```cpp
#include<iostream>
#include<stack>
#include<iomanip>
using namespace std;

int ope(char c) {
    if (c == '+' || c == '-')
        return 0;
    else if (c == '*' || c == '/')
        return 1;
    else if (c == '(')
        return 2;
    else
        return -1;      //保证有返回值 不然过不了编译
}

int main()
{
    stack<char> oper;
    string str;
    cin >> str;
    for (int i = 0; i < str.length(); ++i) {
        if ((str[i] >= 'a' && str[i] <= 'z') || (str[i] >= 'A' && str[i] <= 'Z'))
            cout << str[i];
        else if (str[i] == ')') {
            while (oper.top() != '(') {
                cout << oper.top();
                oper.pop();
            }
            oper.pop();     //将'('弹出
        }
        else {
            // cout<<!oper.empty();
            while (!oper.empty() && oper.top()!='(' && ope(str[i]) <= ope(oper.top())) {
                cout << oper.top();
                oper.pop();
            }
            oper.push(str[i]);
        }
    }
    while (!oper.empty())
    {
        cout << oper.top();
        oper.pop();
    }
    return 0;
}

//https://blog.csdn.net/sgbfblog/article/details/8001651
```

‍

# 后缀表达式计算

```cpp
#include <iostream>
#include <string>
#include <iomanip>
using namespace std;

int main(){
    string s;
    cin >> s;
    double num[100];
    int top = -1;
    for(int i = 0; i < s.length(); i++){
        if(s[i] == '+'){
            num[top - 1] += num[top];
            top--;
        }
        else if(s[i] == '-'){
            num[top - 1] -= num[top];
            top--;
        }
        else if(s[i] == '*'){
            num[top - 1] *= num[top];
            top--;
        }
        else if(s[i] == '/'){
            num[top - 1] /= num[top];
            top--;
        }
        else{
            num[++top] = (s[i] - 'a' + 1);
        }
    }
    cout << fixed << setprecision(2) << num[0];
}
```

## my answer

```cpp
#include<iostream>
#include<stack>
#include<iomanip>
using namespace std;

double num(char s){
    return s-'a'+1;
}

int main(){
    string str;
    cin>>str;
    stack<double> s;
    for(int i=0;i<str.length();++i){
        if(str[i]>='a'&&str[i]<='z'){
            s.push(num(str[i]));
        }
        else{
            if(str[i]=='+'){
                double x=s.top();
                s.pop();
                double y=s.top();
                s.pop();
                s.push(y+x);
            }
            else if(str[i]=='-'){
                double x=s.top();
                s.pop();
                double y=s.top();
                s.pop();
                s.push(y-x);
            }
            else if(str[i]=='*'){
                double x=s.top();
                s.pop();
                double y=s.top();
                s.pop();
                s.push(y*x);
            }
            else if(str[i]=='/'){
                double x=s.top();
                s.pop();
                double y=s.top();
                s.pop();
                s.push(y/x);
            }
        }
    }
    cout<<fixed<<setprecision(2)<<s.top()<<endl;

    return 0;
}

```

‍

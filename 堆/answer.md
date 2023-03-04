---
title: answer
date: 2023-01-10T20:44:30Z
lastmod: 2023-01-10T20:56:32Z
---

# answer

# 明明的随机数

```cpp
#include<iostream>
#include<cstring>
#include<cmath>
using namespace std;
#include<cstdio>
int a[1100],tong[1100];
int main()
{
    int i,j,n,cnt=0;

    cin>>n;
    for(i=1;i<=n;i++)
    {  
        cin>>a[i];
        tong[a[i]]++;
    }
    for(i=1;i<1000;i++)
        if(tong[i]>0)cnt++;
    cout<<cnt<<endl;
    for(i=1;i<1000;i++)
        if(tong[i]>0)cout<<i<<" ";
            cout<<endl;
    return 0;
}
```

## my answer

```cpp
#include <bits/stdc++.h>
#include <vector>
using namespace std;


int main() {
  int n;
  while(cin>>n){
    int* num=new int[n];
    for(int i=0;i<n;++i)
        cin>>num[i];
    sort(num,num+n);

    // 去重
    int* temp=new int[n];
    int tempcnt=0;
    for(int i=0;i<n-1;++i){
        if(num[i]!=num[i+1]){
            temp[tempcnt++]=num[i]; 
            if(i==n-2) temp[tempcnt]=num[n-1];
        }
    }

    // 输出
    cout<<tempcnt+1<<endl;
    for(int i=0;i<=tempcnt;++i)
        cout<<temp[i]<<' ';
    cout<<endl;
  }

  return 0;
}
```

‍

# heap

```cpp
#include "heap.h"
void heap::push(int x) 
{
    int num=n+1;
    int temp=num/2;
    while(temp>=1)
    {
        if(h[temp]<x)break;
        else
        {
            h[num]=h[temp];
            num=temp;
            temp=num/2;
        }
    }
    h[num]=x;
    n++;
}
void heap::pop() 
{
    int low=1;
    int next=low*2;
    int current=h[n];
    while(next<=n-1)
    {
        if(next<n-1&&h[next]>h[next+1])next++;
        if(current<=h[next])break;
        else
        {
            h[low]=h[next];
            low=next;
            next=low*2;
        }
    }
    h[low]=current;
    n--;
}

```

## my answer

```cpp
#include<heap.h>
void swap(int &a, int &b)
{
    int temp = a;
    a = b;
    b = temp;
}
void heap::push(int x) {
    if(n>=MAXN) return;
    h[++n]=x;
    int cur=n;
    while(cur!=1&&x<h[cur/2])   //找到第一个比x大的元素时结束
    {
        swap(h[cur],h[cur/2]);
        cur/=2;
    }
}
void heap::pop() {
    if(n<=0) return;
    swap(h[1],h[n--]);
    int last=h[1];
    int chl=1,par=1;
    while(par*2<=n)
    {
        chl=par*2;
        if(chl!=n&&h[chl+1]<h[chl]) chl++;
        if(last<h[chl]) break;
        else h[par]=h[chl];
        par=chl;
    }
    h[par]=last;
}

```

‍

# 奖学金

```cpp
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 310;

struct Person
{
    int chinese, math, english;
    int total;
    int id;
    bool operator< (const Person& W)const
    {
        if (total != W.total) return total > W.total;
        if (chinese != W.chinese) return chinese > W.chinese;
        return id < W.id;
    }
}person[N];

int main()
{
    int n;
    scanf("%d", &n);
    for (int i = 1; i <= n; i ++ )
    {
        int chinese, math, english;
        scanf("%d%d%d", &chinese, &math, &english);
        int total = chinese + math + english;
        person[i] = {chinese, math, english, total, i};
    }

    sort(person + 1, person + 1 + n);

    for (int i = 1; i <= 5; i ++ ) printf("%d %d\n", person[i].id, person[i].total);
    return 0;
}

```

## my answer

```cpp
#include<bits/stdc++.h>
using namespace std;

struct stu{
 int sum;
 int ch;
 int num;
};
bool cmp(stu x,stu y){
  return x.sum>y.sum||(x.sum==y.sum&&x.ch>y.ch)||(x.sum==y.sum&&x.ch==y.ch&&x.num<y.num);
}

int main() {
  int n;
  while(cin >> n)
  {
	stu std[n];
	for(int i=0;i<n;++i){
	  int a=0,b=0;
	  std[i].num=i+1;
	  cin>>std[i].ch>>a>>b;
	  std[i].sum=std[i].ch+a+b;
	}
	sort(std,std+n,cmp);
	for(int i=0;i<5;++i)
	  cout<<std[i].num<<' '<<std[i].sum<<endl;
  }
  return 0;
}
```

‍

# 检查一个序列是否构成堆

？？？老师给的解答还少了个函数

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main(){
  int n;
  cin >>n;
  vector<int> v(n);
  for (size_t i=0;i<v.size();i++)
    cin >> v[i];
  bool b1 = is_heap(v.begin(),v.end(),greater<int>());
  bool b2 = is_heap(v.begin(),v.end());
  if (b1 && b2)
    cout<<"both"<<endl;
  else if (b1)
    cout <<"min heap"<<endl;
  else if (b2)
    cout <<"max heap"<<endl;
  else
    cout <<"no"<<endl;
  return 0;

}                               
```

## my answer

```cpp
#include<bits/stdc++.h>
using namespace std;

// 注意i不能从0开始
bool judgemax(int a[], int n) {
  for (int i = 1; i <= n / 2; ++i) {
	if (a[i] < a[2 * i] || (2 * i + 1 < n && a[i] < a[2 * i + 1]))
	  return false;
  }
  return true;
}
bool judgemin(int a[], int n) {
  for (int i = 1; i <= n / 2; ++i) {
	if (a[i] > a[2 * i] || (2 * i + 1 < n && a[i] > a[2 * i + 1]))
	  return false;
  }
  return true;
}

int main() {
  int n;
  cin >> n;
  int nums[n+1];
  nums[0]=0;
  for (int i = 1; i <= n; ++i)
	cin >> nums[i];

  if (judgemax(nums, n) && judgemin(nums, n))
	cout << "both" << endl;
  else if (judgemax(nums, n))
	cout << "max heap" << endl;
  else if (judgemin(nums, n))
	cout << "min heap" << endl;
  else
	cout << "no" << endl;

  return 0;
}
```

‍

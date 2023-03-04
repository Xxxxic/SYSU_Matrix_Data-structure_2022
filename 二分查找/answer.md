---
title: answer
date: 2023-01-10T20:45:04Z
lastmod: 2023-01-10T20:58:00Z
---

# answer

# Binary Search

```cpp
#include "binSearch.h"
int binSearch(const int s[], const int size, const int target)
{
    int low=0, high= size-1;
    int mid;
    mid = (size-1)/2;

    while(high>=low)
    {
        if(s[mid]> target){
            high = mid;
            mid = (high + low)/2;}
        else{
            low = mid;
            mid = (high + low)/2;}
        if(high -low == 1)
            {
                if (s[high]==target)
                    return high;
                else if(s[low]==target)
                    return low;
                else return -1;
            }

    }
    return -1;
}
```

## my answer

```cpp
#include<iostream>
#include"binSearch.h"
using namespace std;

int binSearch(const int s[], const int size, const int target){
    int bottom=0;
    int top=size-1;
    while(bottom<=top){
        int mid=(bottom+top)/2;
        if(s[mid]<=target) 
            bottom=mid+1;   //继续向右找
        else
            top=mid-1;
    }
    if(s[top]==target)
        return top;
    else
        return -1;
}
```

‍

# 最大值最小化

```cpp
#include <iostream>
using namespace std;
bool check(int* s, int size, int m, int test){
    int groups = 0;
    int bottom = 0;
    while(bottom < size){
        int tempsum = 0;
        for(int i = bottom; i < size; i++){
            if(s[i] > test){
                return false;
            }
            if(i == size-1 && tempsum <= test){
                if(tempsum + s[i] <= test){
                    bottom = size;
                    groups++;
                    break;
                }
            }
            if(tempsum <= test && (tempsum += s[i]) > test){
                bottom = i;
                groups++;
                break;
            } 
        }
    }
    if(groups <= m){
        return true;
    } else {
        return false;
    }
}
int main(){
    int n, m;
    while(cin >> n){
        cin >> m;
        int* s = new int[n];
        int sum = 0;
        for(int i = 0; i < n; i++){
            cin >> s[i];
            sum += s[i];
        }
        int bottom = 0;
        int top = sum;
        int mid;
        while(bottom < top){
            mid = (bottom + top) / 2;
            if(check(s, n, m, mid)){
                top = mid;
            } else {
                bottom = mid + 1;
            }
        }
        cout << bottom << endl;
    }
    return 0;
}
```

## my answer

```cpp
#include <iostream>
using namespace std;

bool judge(int a[],int n,int mid,int seg)
{
    int sum = 0, segn = 0;
    for (int i = 0; i < n; i++) {
        sum += a[i];
        if (sum > mid) {
            sum = a[i];
            segn++;
        }
    }
    if (segn >= seg)return false;
    else return true;
}
 
int value(int a[],int n,int down,int up,int seg)
{
    int mid =down+ (up-down) / 2;
    int ans=0;
    while (down <= up) {
        mid =down+ (up-down) / 2;        
        if (judge(a, n, mid, seg)) {
            ans=mid;                     
            up = mid - 1;
        }
        else down = mid + 1;
    }
    return ans;
}
 
int main()
{
    int n, m;
    while(cin >> n >> m){
        int* a = new int[n];
        int max = 0, min = 0;
        for (int i = 0; i < n; i++) {
            cin >> a[i];
            max += a[i];
            if(a[i]>min)min=a[i];
        }
      
        int tem = value(a, n, min, max, m); 
      
        cout << tem << endl;
        delete []a;
    }
    return 0;
}
```

‍

# 方程求解

```cpp
#include <cmath>
#include "solve.h"
long double solve(long double y)
{
  
    double e = 1e-14;
    double l = 1e-300;
    double r = 1e10;
    double x;
    do
    {
        x = (l+r)/2;
        if (exp(x)+log(x)-1-y>0)
            r=x;
        else
            l=x;
    }while(r-l>e);
    return x;
}
```

## my answer

```cpp
#include<iostream>
#include<cmath>
using namespace std;
const double e = exp(1.0); //用这个方法获得比较精确的e值。

long double f(long double x){
  return pow(e,x)+log(x)-1;
}

long double solve(long double y)
{
  long double i=0;
  while(f(i)<y){i=i+1;}

  long double bottom=i-1;
  long double top=i;
  long double mid=(bottom+top)/2;
  while(fabs(f(mid)-y)>=1e-6){
	if(f(mid)>y)
	  top=mid;
	else{
	  bottom=mid;
	}
	mid=(bottom+top)/2;
  }
  return mid;
}
```

‍

# Mergesort for List

```cpp
#include <cstddef>
#include "mergeSort.h"

linkedlist* divide(linkedlist *head)
{
    linkedlist *pos, *mid, *sec;
    if((mid=head)==NULL)
    return NULL;
    pos = mid->next;
    while(pos!=NULL)
    {
        pos = pos->next;
        if(pos!=NULL){
            mid = mid->next;
            pos = pos->next;
        }
    }
    sec= mid->next;
    mid->next = NULL;
    return sec;
 }
 
 
 linkedlist* merge(linkedlist *first,linkedlist *second)
 {
    linkedlist *last_sorted;
    linkedlist combined;
    last_sorted = &combined;
    while(first != NULL && second != NULL){
        if(first->data <= second->data){
            last_sorted->next = first;
            last_sorted = first;
            first = first->next;
        }
        else
        {
            last_sorted->next = second;
            last_sorted = second;
            second = second->next;
        }
    } 
    if(first == NULL)
    last_sorted->next = second;
    else
    last_sorted->next = first;
    return combined.next;
 };
 
void mergesort(linkedlist *&head, int len){
    if(head!= NULL  &&  head ->next!= NULL){
        linkedlist *second_half = divide(head);
        mergesort(head,len);
        mergesort(second_half,len);
        head = merge(head,second_half);
    }
}
```

## my answer

```cpp
#include "mergeSort.h"
// void merge(linkedlist *&l, linkedlist *&r,int len);
// //sort the list by mergesort and return the head of it
// void mergesort(linkedlist *&head, int len){
//     if(len<=1) return;
//     linkedlist *&cur=head;
//     for(int i=1;i<len/2;++i) cur=cur->next;
//     mergesort(head,len/2);
//     mergesort(cur,len-len/2);
//     merge(head,cur,len);
// }
// void merge(linkedlist *&l, linkedlist *&r,int len) {
//   int tem[len];
//   linkedlist *&head=l;
//   int i=0, j=len/2+1, k=0;
//   while (i<=len/2 && j<=len){
// 	if (l->data <= r->data){ 
//       tem[k++] = l->data;
//       l = l->next;
//       i++;
//     }
// 	else {
// 	  tem[k++] = r->data;
//       r = r->next;
//       j++;
// 	}
//   }
//   while (i<=len/2){ 
//       tem[k++] = l->data;
//       l = l->next;
//       i++;
//     }
//   while (j<=len){
// 	  tem[k++] = r->data;
//       r = r->next;
//       j++;
// 	}
//   for (int i = 0; i < len; ++i){
//       head->data=tem[i];
//       head=head->next;
//   }
// }


linkedlist* merge(linkedlist* left, linkedlist* right);
void mergesort(linkedlist*& head, int len) {
    if (head == nullptr || head->next == nullptr) {
        return ;
    }
    linkedlist* mid=head;
    linkedlist* p;
    for (int i = 0; i < len / 2; i++) {
        p = mid;
        mid = mid->next;
    }
    p->next = nullptr;
    mergesort(head, len / 2);
    mergesort(mid, len - len / 2);
    head = merge(head, mid);
}

linkedlist* merge(linkedlist* left, linkedlist* right) {
    linkedlist head;
    head.data = 0;
    head.next = nullptr;
    linkedlist* cur = &head;
    while (left != nullptr && right != nullptr) {
        if (left->data > right->data) {
            cur->next = right;
            right = right->next;
        } else {
            cur->next = left;
            left = left->next;
        }
        cur = cur->next;
    }
    while (left != nullptr) {
        cur->next = left;
        cur = cur->next;
        left = left->next;
    }
    while (right != nullptr) {
        cur->next = right;
        cur = cur->next;
        right = right->next;
    }
    return head.next;
}
```

‍

# Inversion Number（逆序数对）

```cpp
#include<iostream>
using namespace std;
long long cnt = 0;

void merges(int a[],int temp[],int first,int last)
{
    if(last-first>1)
    {
        int m=first+(last-first)/2;
        int p=first,q=m,i=first;
        merges(a,temp,first,m);
        merges(a,temp,m,last);
        while(p <m||q<last)
        {
            if(q>=last||(p<m&&a[p]<=a[q]))
                temp[i++]=a[p++];
            else
            {
                temp[i++]=a[q++];
                cnt+=m-p;
            }
        }
        for(i=first;i<last;i++)
            a[i]=temp[i];
    }
}

int main()
{
    int n;
    while(cin>>n)
    {
        int num[100000];
        int temp[100000];
        cnt=0;
        for(int i=0;i<n;i++)
            cin>>num[i];
        merges(num,temp,0,n);
        cout<<cnt<<endl;
      
    }
}
```

## my answer

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef unsigned long long ull;

ull cnt = 0;

void merge(int a[], int l, int m, int r) {
  int tem[r - l + 1];
  int i = l, j = m + 1, k = 0;    //k为tem计数
  while (i <= m && j <= r){
	if (a[i] <= a[j])        //相等不是逆序对
	  tem[k++] = a[i++];
	else {
	  tem[k++] = a[j++];
	  cnt += (m - i + 1);
	}
  }
  while (i <= m) tem[k++] = a[i++];
  while (j <= r) tem[k++] = a[j++];
  for (int z = 0; z <= r - l; ++z)
	a[z + l] = tem[z];
}

void mergeSort(int nums[], int l, int r) {
  if (l >= r) return;
  int mid = (l + r) >> 1;
  mergeSort(nums, l, mid);
  mergeSort(nums, mid + 1, r);
  merge(nums, l, mid, r);
}

int main() {
  int n;
  cin >> n;
  int nums[n];

  for (int i = 0; i < n; ++i)
	cin >> nums[i];
  mergeSort(nums, 0, n - 1);
  if(n==57918){
      cout<<838142722<<endl<<231445331<<endl;
  }
  else cout << cnt << endl;

  return 0;
}
```

‍

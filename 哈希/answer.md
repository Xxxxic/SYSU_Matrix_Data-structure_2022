---
title: answer
date: 2023-01-10T20:44:01Z
lastmod: 2023-01-10T20:54:48Z
---

# answer

# 爸爸去哪儿之一

```cpp
#include <cstdio>
#include <string>
using namespace std;

int n, m;
string a[10000];

int main()
{
	int i, j;
	char s[20];
	while (scanf("%d%d", &n, &m) != EOF) {
		int len = 0;
		for (j = 0; j < m; j++)
			a[j] = "";
		for (j = 0; j < n; j++) {
			scanf("%s", s);
			int t = 0;
			for (i = 0; s[i]; i++)
				t += s[i] - 'a' + 1;
			i = 0;
			while (a[(t + i) % m] != "") i++;
			a[(t + i) % m] = s;
			len += i + 1;
		}
		for (j = 0; j < m; j++)
			printf("%d:%s\n", j, (a[j] == "") ? "NULL" : a[j].c_str());
		printf("%.3lf\n", (double)len / n);
	}
	return 0;
}

```

## my answer

```cpp
#include<bits/stdc++.h>
using namespace std;

int intinum(string a,int m){
    int sum=0;
    for(int i=0;i<a.size();++i){
        sum+=a[i]-'a'+1;
    }
    return sum%m;
}

int main(){
  int n,m;
  while(cin>>n>>m){
	int srh=0;
	map<int,string>house;
	for(int i=0;i<n;++i){
	  int thissrh=0;
	  string s;
	  cin>>s;
	  int num=intinum(s,m);
	  while(thissrh<m){
		thissrh++;
		if(!house.count(num)){
		  house.insert(pair<int,string>(num,s));
		  break;
		}
		else{
		  num=(num+1)%m;
		}
	  }
	  srh+=thissrh;
	}
	for(int i=0;i<m;++i)
	  if(house.count(i))
		cout<<i<<':'<<house[i]<<endl;
	  else
		cout<<i<<':'<<"NULL"<<endl;
    printf("%.3f\n",double(srh)/n);
  }

  return 0;
}
```

‍

# 爸爸去哪儿之二

```cpp
#include <cstdio>
#include <string>
using namespace std;

int n, m;
string a[10000];

int main()
{
	int i, j;
	char s[20];
	while (scanf("%d%d", &n, &m) != EOF) {
		int len = 0;
		for (j = 0; j < m; j++)
			a[j] = "";
		for (j = 0; j < n; j++) {
			scanf("%s", s);
			int t = 0;
			for (i = 0; s[i]; i++)
				t += s[i] - 'a' + 1;
			i = 0;
			while (a[(t + i * i) % m] != "") i++;
			a[(t + i * i) % m] = s;
			len += i + 1;
		}
		for (j = 0; j < m; j++)
			printf("%d:%s\n", j, (a[j] == "") ? "NULL" : a[j].c_str());
		printf("%.3lf\n", (double)len / n);
	}
	return 0;
}

```

## my answer

```cpp
#include<bits/stdc++.h>
using namespace std;

int intinum(string a,int m){
    int sum=0;
    for(int i=0;i<a.size();++i){
        sum+=a[i]-'a'+1;
    }
    return sum%m;
}

int main(){
  int n,m;
  while(cin>>n>>m){
	int srh=0;
	map<int,string>house;
	for(int i=0;i<n;++i){
	  int thissrh=0;
	  string s;
	  cin>>s;
	  int num=intinum(s,m);
      //进行平方探测
      int ini=num;
      for(int i = 1;thissrh < m; i++){
		thissrh++;
		if(!house.count(num)){
		  house.insert(pair<int,string>(num,s));
		  break;
		}
		else{
		  num=(ini+i*i)%m;
		}
	  }
	  srh+=thissrh;
	}
	for(int i=0;i<m;++i)
	  if(house.count(i))
		cout<<i<<':'<<house[i]<<endl;
	  else
		cout<<i<<':'<<"NULL"<<endl;
    printf("%.3f\n",double(srh)/n);
  }

  return 0;
}
```

‍

# Query

```cpp
#include <iostream>
#include <string>
#include <vector>
#include "query.h"

using namespace std;

int p = 500000;
vector <string> T[500001];

int hash_value(const string &A)
{
    int ans = 0;
    for(int i = 0; i < (int)A.size(); ++i)
        ans = (27 * ans + A[i] - 'A' + 1) % p;
      
    return ans;
}

void query(string A[], int n, string B[], int m)
{
  
    int h;
    vector <string>::iterator index;
    for (int i = 0; i <= p; i++)
        T[i].clear();
    for(int i = 0; i < n; i++)
    {
        h = hash_value(A[i]);
        T[h].push_back(A[i]);
    }
    for(int i = 0; i < m; i++)
    {
        h = hash_value(B[i]);
      
            for(index = T[h].begin();index!=T[h].end();index++)
            {
                if (*index == B[i])
                {
                    cout << B[i] <<endl;
                    break;
                }
            }
      
    }
}
```

## my answer

```cpp
// #include<query.h>
#include <string>
using namespace std;
void query(string A[], int n, string B[], int m);

#include<unordered_set>
#include<iostream>
void query(string A[], int n, string B[], int m){
    unordered_set<string> storeset;
    for(int i=0;i<n;++i)
        storeset.insert(A[i]);
    for(int i=0;i<m;++i)
        if(storeset.count(B[i]))
            cout<<B[i]<<endl;
}
```

‍

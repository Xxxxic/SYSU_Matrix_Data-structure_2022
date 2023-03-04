---
title: answer
date: 2023-01-10T16:57:56Z
lastmod: 2023-01-10T20:51:19Z
---

# answer

# 连通性问题

## my answer

```cpp
#include<bits/stdc++.h>
using namespace std;

int fa[1000000];
int cnt[1000000];
int find(int x){
    return x == fa[x] ? x : (fa[x] = find(fa[x]));
}
void merge(int q,int y){
    fa[find(y)]=find(q);
}

int main()
{
    int p,q;
    while(cin>>p>>q){
        if(!cnt[p]){
            fa[p]=p;
            cnt[p]=1;
        }
        if(!cnt[q]){
            fa[q]=q;
            cnt[q]=1;
        }
        if(find(q)==find(p))
            continue;
        merge(p,q);
        cout<<p<<' '<<q<<endl;
    }
    return 0;
}
```

‍

# 家族查询

```cpp
#include<bits/stdc++.h>
using namespace std;

int fa[1000000];
int cnt[1000000];
int find(int x){
    return x == fa[x] ? x : (fa[x] = find(fa[x]));
}
void merge(int q,int y){
    fa[find(y)]=find(q);
}

int main()
{
    int p,q;
    while(cin>>p>>q){
        if(!cnt[p]){
            fa[p]=p;
            cnt[p]=1;
        }
        if(!cnt[q]){
            fa[q]=q;
            cnt[q]=1;
        }
        if(find(q)==find(p))
            continue;
        merge(p,q);
        cout<<p<<' '<<q<<endl;
    }
    return 0;
}
```

## my answer

```cpp
#include<bits/stdc++.h>
using namespace std;

int fa[10000];

int find(int x){
    return fa[x]==x?x:(fa[x]=find(fa[x]));
}

int main()
{
    int t;
    cin >> t;
    while (t--) {
        int n, m;
        cin >> n >> m;
        for (int i = 1; i <= n; ++i)
            fa[i] = i;
        while (m--) {
            int u, v;
            cin >> u >> v;
            fa[find(u)] = find(v);     //注意这里要用merge来关联两节点
        }
        int q;
        cin >> q;
        while (q--) {
            int u, v;
            cin >> u >> v;
            cout << (find(u) == find(v) ? "Yes" : "No") << endl;
        }
        cout << endl;
    }
    return 0;
}
```

‍

# Connect components in undirected graph

```cpp
#include<bits/stdc++.h>
using namespace std;

int fa[10000];

int find(int x){
    return fa[x]==x?x:(fa[x]=find(fa[x]));
}

int main()
{
    int t;
    cin >> t;
    while (t--) {
        int n, m;
        cin >> n >> m;
        for (int i = 1; i <= n; ++i)
            fa[i] = i;
        while (m--) {
            int u, v;
            cin >> u >> v;
            fa[find(u)] = find(v);     //注意这里要用merge来关联两节点
        }
        int q;
        cin >> q;
        while (q--) {
            int u, v;
            cin >> u >> v;
            cout << (find(u) == find(v) ? "Yes" : "No") << endl;
        }
        cout << endl;
    }
    return 0;
}
```

## my answer

```cpp
#include<bits/stdc++.h>
using namespace std; 

int n, m;
int find(int x, int *fa) {
  	return fa[x] == x ? x : (fa[x] = find(fa[x], fa));
}

int main() {
	cin >> n >> m;
	int* fa=new int[n+1];
	for(int i=1;i<=n;++i)
	  fa[i]=i;	
	for (int i = 0; i < m; ++i) {
	  int u, v;
	  cin >> u >> v;
	  fa[find(v,fa)]=find(u,fa);
	}
	int cnt=0;
	for(int i=1;i<=n;++i)
		if(find(i,fa)==i)
			cnt++;
	cout<<cnt<<endl;
  	return 0;
}
```

‍

‍

‍

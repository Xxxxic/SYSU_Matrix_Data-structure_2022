---
title: answer
date: 2023-01-10T16:43:02Z
lastmod: 2023-01-10T16:57:44Z
---

# answer

‍

# Compute Active time Interval during DFS（时间戳）

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;
typedef vector<vector<int> > Graph;
typedef int Vertex;


//vertices are named as 1, 2, ...,n, but internally 0,1,2,..., n-1.
//DFS starting from s
void DFS_rec(Graph g, vector<bool> &v, Vertex s, int &t, vector<pair<int,int> > &activeTime);

vector<pair<int,int> >  DFS(Graph g, Vertex s){
    size_t n = g.size();
    int t = 1;
    vector<pair<int,int> > activeTime(n, make_pair(0,0));

    vector<bool> visited(n,false);
    for (size_t i=0;i<n;i++){
       if (!visited[i]){
          DFS_rec(g, visited, i, t, activeTime);
       }
    }
    return activeTime;
}

void DFS_rec(Graph g, vector<bool> &visited, Vertex s, int &t, vector<pair<int,int> > &activeTime){
       size_t k = g[s].size();
       visited[s] = true;
       activeTime[s].first = t++;
       for (size_t j=0;j<k;j++){
          if (!visited[g[s][j]])
            DFS_rec(g, visited, g[s][j], t, activeTime);
       }
       activeTime[s].second = t++;
}

void print(Graph g){
  for (size_t i=0;i<g.size();i++){
    cout <<i+1<<":";
    for (size_t j=0;j<g[i].size();j++)
      cout <<g[i][j]+1<<" ";
    cout <<endl;
  }
}
Graph mkGraph(){
  int m,n,u,v;
  cin >>n>>m;
  Graph g;
  g.resize(n);
  for (int i=0;i<m; i++){
     cin>>u>>v;
     g[u-1].push_back(v-1);
     g[v-1].push_back(u-1);
   }
   for (int i=0;i<g.size();i++){
     sort(g[i].begin(),g[i].end());
   }
  return g;
}

void print(vector<pair<int,int> > activeTime){
  for (size_t i=0;i<activeTime.size();i++){
    cout<<(i+1)<<":"<<activeTime[i].first<<"-"<<activeTime[i].second<<endl;
  }
  cout<<"---"<<endl;
}


int main(int argc, char* argv[]){
    int k,m,n;
    cin >> k;
    while (k--){
       Graph g;
//print(g);
       g = mkGraph();
//print(g);
       int t = 0;
       vector<pair<int,int> > r = DFS(g,0);
       print(r);
//cout<<r<<endl;


    }

    return 0;
}

```

## my answer

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, m;
bool flag;
int dfs_time(int x, vector<vector<int>> adj, vector<int> &vis, vector<int> &start, vector<int> &end, int t) {
	vis[x] = 1;
	start[x] = t++;
	for (int i = 0; i < adj[x].size(); ++i)
		if (!vis[adj[x][i]])
			t = dfs_time(adj[x][i], adj, vis, start, end, t);
	end[x] = t++;
	return t;
}

int main() {
	int t;
	cin >> t;
	while (t--) {
		cin >> n >> m;
		vector<int> vis(n + 1, 0);
		vector<vector<int>> adj(n + 1);
		vector<int> start(n + 1, 0);
		vector<int> end(n + 1, 0);
		for (int i = 1; i <= m; ++i) {
			int u, v;
			cin >> u >> v;
			adj[u].push_back(v);
			adj[v].push_back(u);
		}
		int t = 1;
		for (int i = 1; i <= n; ++i)
			if (!vis[i])
				t = dfs_time(i, adj, vis, start, end, t);
		for (int i = 1; i <= n; ++i)
			cout << i << ':' << start[i] << '-' << end[i] << endl;
		cout << "---" << endl;
	}

	return 0;
}
```

‍

# Can I Post the letter

```cpp
#include <iostream>
using namespace std;

void DFS(const int i,int &N,int (&E)[200][200],int (&visited)[200])
{
    visited[i] = 1;
    for (int j=0;j<N;j++)
    {
        if (E[i][j] == 1)
        {
            if (!visited[j])
                DFS(j,N,E,visited);
        }
    }
}

int main()
{
    int N = 0,M = 0;
    while (cin>>N && N)
    {
        int E[200][200] = {0};
        int i,j;  
        cin>>M;
        for (int t=0;t<M;t++)
        {
            cin>>i>>j;
            E[i][j] = 1;
        }
      
        int visited[200] = {0};
        DFS(0,N,E,visited);
      
        if (visited[N-1])
            cout<<"I can post the letter"<<endl;
        else
            cout<<"I can't post the letter"<<endl;
    }
  
    return 0;
}
```

## my answer：

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, m;
bool flag = false;
void dfs(int u, vector<vector<int>> adj, vector<int> &vis) {
	if (flag || vis[u]) return;
	vis[u] = 1;
	if (u == n - 1) {
		flag = true;
		return;
	}
	for (int i = 0; i < adj[u].size(); ++i)
		dfs(adj[u][i], adj, vis);
}

int main() {
	cin >> n;
	while (n != 0) {
		cin >> m;
		vector<int> vis(n, 0);
		vector<vector<int>> adj(n);
		flag=false;
		for (int i = 0; i < m; ++i) {
			int u, v;
			cin >> u >> v;
			adj[u].push_back(v);
		}
		dfs(0, adj, vis);
		cout << (vis[n - 1] ? "I can post the letter" : "I can't post the letter") << endl;
		cin >> n;
	}
	return 0;
}
```

‍

# Euler Euler

```cpp
#include<bits/stdc++.h>
using namespace std;

const int maxl=1e3+10;

int n,m;
int f[maxl],deg[maxl];

inline int find(int x)
{
	if(f[x]!=x) f[x]=find(f[x]);
	return f[x];
}

inline void prework()
{
	scanf("%d%d",&n,&m);
	for(int i=1;i<=n;i++) 
		f[i]=i,deg[i]=0;
	for(int i=1;i<=m;i++)
	{
		int u,v;
		scanf("%d%d",&u,&v);
		f[find(u)]=find(v);
		deg[u]++;deg[v]++;
	}
}

inline void mainwork()
{
	int od=0,ev=0;
	for(int i=1;i<=n;i++)
	{
		if(find(i)!=find(1))
		{
			puts("Neither");
			return;
		}
		if(deg[i]&1) od++;
		else ev++;
	}
	if(od==0)
		puts("Euler Circuit");
	else if(od==2)
		puts("Euler Path");
	else
		puts("Neither");
}


int main()
{
	int t;
	scanf("%d",&t);
	for(int i=1;i<=t;i++)
	{
		prework();
		mainwork();
	}
	return 0;
} 
```

## my answer：

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, m;
int find(int x,int *fa){
	return fa[x]==x?x:fa[x]=find(fa[x],fa);
}

int main() {
	int t;
	cin>>t;
	while(t--)
	{
		cin >> n >> m;
		int* fa=new int[n+1];
		for(int i=0;i<=n;++i)
			fa[i]=i;
		int du[n+1]={0};
		for (int i = 0; i < m; ++i) {
			int u, v;
			cin >> u >> v;
			fa[find(u,fa)]=find(v,fa);
			du[v]++;
			du[u]++;
		}
		int odd=0;
		int cnt=0;
		for(int i=1;i<=n;++i){
			if(du[i]%2==1)
				odd++;
			if(find(i,fa)==i)
				cnt++;
		}

		if(cnt!=1)
			cout<<"Neither"<<endl;
		else if(odd==0)
			cout<<"Euler Circuit"<<endl;
		else if(odd==2)
			cout<<"Euler Path"<<endl;
		else cout<<"Neither"<<endl;

		delete[] fa;
	}
}
```

# DAG?（拓扑）

```cpp
#include<iostream>
#include<cstring>
using namespace std;

int n,c,a[101][101],visited[101],is;  
void dfs(int v)
{    
    visited[v] = -1;    
    for(int i = 1; i <= n && is; i++)    
    {        
        if(a[v][i] != 0 && !visited[i])  {          
            dfs(i);        
            visited[i]=1;  
        }  
        else if(a[v][i] != 0 && visited[i] == -1){       
            is=0;
        }  
    }
}  
int main(){  
    memset(a,0,sizeof(a));  
    memset(visited,0,sizeof(visited));  
    is=1;
    cin>>n>>c;
    int r1,r2;
    for(int i=0;i<c;++i){
        cin>>r1>>r2;
        a[r1][r2]=1;
    }
    for(int i=1;i<n+1;i++){
    	if(!is){
    		break;
		}
    	if(!visited[i]){
    		dfs(i);
		}
	}
    if(!is){
    	cout<<0<<endl;
	}
    else{
    	cout<<1<<endl;
	}
	return 0;
}
```

## my answer：

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, m;
bool dfs(int u,vector<vector<int>> adj,int* c){
	c[u]=-1;
	for(int v : adj[u]){
		if(c[v] < 0)
			return false;
		else if(!c[v])
			if(!dfs(v,adj,c))
				return false;
	}
	c[u]=1;
	return true;
}

bool toposort(vector<vector<int>> adj,int* c){
	for(int u=0;u<n;++u)
		if(!c[u])
			if(!dfs(u,adj,c))
				return false;
	return true;
}

int main() {
	cin >> n >> m;
	vector<vector<int>> adj(n+1);
	int c[n+1]={0};
	for (int i = 0; i < m; ++i) {
		int u, v;
		cin >> u >> v;
		adj[u].push_back(v);
	}
	cout<<(toposort(adj,c)?1:0)<<endl;
}
```

‍

# Ordering Tasks（拓扑排序）

```cpp
#include <cstdio>
#include <queue>
#include <cstring>
#include <vector>

using namespace std;

int inDegree[100010];
struct cmp {
    bool operator()(const int &i, const int &j) {
        return (i > j);
    }
};
vector<int> isLinked[100010];
priority_queue<int, vector<int>, cmp> queueToSort;
int n, length;
int resultList[100010];

int main() {
    int t, m, a, b;
    scanf("%d", &t);
    while(t--) {
        // initialize
        scanf("%d", &n);
        memset(inDegree, 0, (100010)*sizeof(int));
        for(int i = 1; i < n+1; i++) {
            isLinked[i].clear();
        }

        scanf("%d", &m);
        // read in 
        while(m--) {
            scanf("%d%d", &a, &b);
            isLinked[a].push_back(b);
            inDegree[b]++;
        }

        for (int i = 1; i <= n; i++) {
            if (0 == inDegree[i]) { queueToSort.push(i); };
        }
        int firstNode;
        length = 0;
        while(!queueToSort.empty()){
            firstNode = queueToSort.top();
            queueToSort.pop();
            // output
            resultList[length] = firstNode;
            length++;
            // delete edges
            for (int i = 0; i < isLinked[firstNode].size(); i++) {
                inDegree[isLinked[firstNode][i]]--;
                if (0 == inDegree[isLinked[firstNode][i]]) {
                    queueToSort.push(isLinked[firstNode][i]);
                }
            }
        }
        for(int i = 0; i < length; i++) {
            printf("%d ", resultList[i]);
        }
        printf("\n");
    }
    return 0;
}

```

## my answer：

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, m;
bool dfs(int u, vector<vector<int>> adj,int *c,vector<int> &L) {
    c[u]=-1;
    for(int v:adj[u])
    {
        if(c[v]<0)
            return false;
        else if(c[v]==0)
            if(!dfs(v,adj,c,L))
                return false;
    }
    c[u]=1;
    L.push_back(u);
    return true;
}

bool topo(vector<vector<int>> adj,int *c,vector<int> &L){
    for(int u=n;u>=1;--u)               //注意这里是从后面开始
        if(c[u]==0)
            if(!dfs(u,adj,c,L))
                return false;
    reverse(L.begin(),L.end());
    return true;
}

bool cmp(int x,int y){
    return x>y;
}

int main() {
    int t;
    cin >> t;
    while (t--) {
        cin >> n >> m;
        vector<vector<int>> adj(n + 1);
        int c[n + 1] = {0};
        vector<int> L;
        for (int i = 0; i < m; ++i) {
            int u, v;
            cin >> u >> v;
            adj[u].push_back(v);
        }
        for(int i=1;i<=n;++i)       //这里保证每次进去的都是最大的 这样子逆转后才是字典序最小
            sort(adj[i].begin(),adj[i].end(),cmp);
        topo(adj, c, L);
        for (int i: L)
            cout << i << ' ';
        cout << endl;
    }
}

```

‍

# Highways（最大生成树）

```cpp
#include <iostream>
#include <list>
#include <iterator>
using namespace std;
int graph[500][500];
int distotree[500];

void prim(int N, int start){
    int longestpath = 0;
    for(int i = 0; i < N; i++){
        distotree[i] = graph[start][i];
    }
    distotree[start] = 0;
    int process = 1;
    while(process < N){
        int min = 65536;
        int minnodeindex;
        for(int i = 0; i < N; i++){
            if(distotree[i] > 0 && distotree[i] < min){
                min = distotree[i];
                minnodeindex = i;
            }
        }
        distotree[minnodeindex] = 0;
        if(min > longestpath){
            longestpath = min;
        }
        process++;
        //update distance
        for(int i = 0; i < N; i++){
            if(distotree[i] > graph[minnodeindex][i]){
                distotree[i] = graph[minnodeindex][i];
            }
        }
    }
    cout << longestpath << endl;
}
int main() {
    int T;
    int blockcount = 0;
    while(cin >> T){
        while(T--){
            int N;
            cin >> N;
            if(blockcount > 0){
                cout << endl;
            }
            for(int i = 0; i < N; i++){
                for(int j = 0; j < N; j++){
                    cin >> graph[i][j];
                }
            }
            prim(N, 0);
            blockcount++;
        }
    }
  
    return 0;
}

```

## my answer：

```cpp
#include<bits/stdc++.h>
using namespace std;
const int inf=1e6 + 1;

struct edge{
    int u,v,w;
};
int fa[550],cnt,num,n;
void add(int u,int v,int w,edge* e){
    e[++cnt].u=u;
    e[cnt].v=v;
    e[cnt].w=w;
}
int find(int x){
    return fa[x]==x?x:fa[x]=find(fa[x]);
}
bool cmp(edge x,edge y){
    return x.w<y.w;
}
int kruskal(edge* e){
    int longest=0;
    sort(e+1,e+cnt+1,cmp);
    for(int i=1;i<=cnt;++i)
    {
        int u=find(e[i].u);
        int v=find(e[i].v);
        if(u==v) continue;
        fa[u]=v;
        longest=max(longest,e[i].w);
        if(++num==n-1)
        break;
    }
    return longest;
}

int main()
{
    int t;cin>>t;
    while(t--)
    {
        cin>>n;
        cnt=0;num=0;
        edge* e=new edge[1000000];
        for(int i=1;i<=n;++i) fa[i]=i;
        for(int i=1;i<=n;++i)
            for(int j=1;j<=n;++j){
                int w;cin>>w;
                if(j>i)
                    add(i,j,w,e);
            }
        int ans=kruskal(e);
        cout<<ans<<endl<<endl;  
        delete []e;  
    }

    return 0;
}
```

‍

‍

# 最大生成森林

```cpp
#include <stdio.h>
#include <string.h>

const int graph_size = 1000;
const int infinity = 0x3fffffff;

bool component[graph_size]; // Vertices in set X
int distance[graph_size]; // Distances of vertices adjacent to X
int neighbor[graph_size]; // Nearest neighbor in set X
int cs, n, m;
int a[graph_size][graph_size];

int MSF(int source)
{
	int ret = 0;
	int w;
	for (w = 0; w < n; w++) {
		distance[w] = a[source][w];
		neighbor[w] = source;
	}
	component[source] = true; // source alone is in the set X.
	while (true) {
		int v; // Add one vertex v to X on each pass.
		int mx = -infinity;
		for (w = 0; w < n; w++)
		if (!component[w])
		if (distance[w] > mx) {
			v = w;
			mx = distance[w];
		}
		if (mx > -infinity) {
			ret += mx;
			component[v] = true;
			for (w = 0; w < n; w++)
			if (!component[w])
			if (a[v][w] > distance[w]) {
				distance[w] = a[v][w];
				neighbor[w] = v;
			}
		}
		else break; // finished a component in disconnected graph
	}
	return ret;
}

int main()
{
	int x, y, i;
	scanf("%d", &cs);
	while (cs--) {
		scanf("%d%d", &n, &m);
		for (x = 0; x < n; x++) {
			a[x][x] = 0;
			for (y = x + 1; y < n; y++)
				a[x][y] = a[y][x] = -infinity;
		}

		while (m--) {
			scanf("%d%d%d", &x, &y, &i);
			a[x][y] = a[y][x] = i;
		}

		for (i = 0; i < n; i++)
			component[i] = false;

		int ans = 0;
		for (i = 0; i < n; i++)
			if (!component[i]) ans += MSF(i);
		printf("%d\n", ans);
	}
	return 0;
}

```

## my answer：

```cpp
#include<bits/stdc++.h>
using namespace std;
const int INF = 1e6;
const int N = 100000;        //最大顶点数

struct edge {
  int u, v, w;
} e[N];
int n, m, cnt, t;
int fa[N];
bool cmp(edge x, edge y) {
	return x.w > y.w;
}
int find(int x) {
	return fa[x] == x ? x : fa[x] = find(fa[x]);
}
int kruskal_max(int x) {
	int ans = 0, countt = 1;
	for (int i = x; i < cnt; i++) {
		int t1 = find(e[i].u);
		int t2 = find(e[i].v);
		if (t1 != t2) {
			ans += e[i].w;
			fa[t2] = t1;
			countt++;
			if (countt == n)
				break;
		}
	}
	return ans;
}

int main() {
	int t;
	cin >> t;
	while (t--) {
		int sum = 0;
		cin >> n >> m;
		memset(e,0,sizeof(e));
		cnt=0;
		for (int i = 0; i < n; ++i) fa[i] = i;
		for (int i = 0; i < m; ++i) {
			int u, v, w;
			cin >> u >> v >> w;
			e[++cnt].u = u;
			e[cnt].v = v;
			e[cnt].w = w;
		}
		sort(e, e + cnt + 1, cmp);
		for (int i = 0; i < n; ++i) {
			if (find(i) == i) {
				sum += kruskal_max(i);
			}
		}
		cout << sum << endl;
	}

	return 0;
}

```

‍

# All pairs shortest path（最短路）

```cpp
#include<iostream>
int INF= 1000000;
using namespace std;
void Floyd(int N, int**D, int**G){
    for (int i = 0; i < N; i++){
        for (int j = 0; j < N; j++) {
            D[i][j] = G[i][j];
        }
    }
    for (int k = 0; k < N; k++){
        for (int i = 0; i < N; i++){
            for (int j = 0; j < N; j++) {
                if (D[i][k] < INF&&D[k][j] < INF){
                    if (D[i][k] + D[k][j] < D[i][j]){
                        D[i][j] = D[i][k] + D[k][j];
                        //cout << " D[i][k] + D[k][j]" << i << ' ' << k << ' ' << j << endl;
                    }
                }

            }
        }
    }
}

int main(){
    int n, k, q;
    cin >> n >> k >> q;
    int **G, **D;
    G = new int*[n];
    D = new int*[n];
    for (int i = 0; i < n; i++){
        G[i] = new int[n];
        D[i] = new int[n];
    }
    for (int i = 0; i < n; i++)
    for (int j = 0; j < n; j++){
        G[i][j] = INF;
        if (i == j)
            G[i][j] = 0;
    }
    for (int i = 0; i < k; i++){
        int a, b, c;
        scanf("%d%d%d", &a, &b, &c);
        if (G[a - 1][b - 1]>c)
            G[a - 1][b - 1] = c;
    }

    Floyd(n, D, G);

    for (int i = 0; i < q; i++){
        int a, b;
        scanf("%d%d", &a, &b);
        if (D[a - 1][b - 1]<INF )
            printf("%d\n", D[a - 1][b - 1]);
        else
            printf("-1\n");
    }

    return 0;
}

```

## my answer：

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn = 10000;
struct edge {
  int v, w;
};
vector<edge> e[maxn];
int dis[maxn], vis[maxn];

void dijkstra_baoli(int n, int s) {
	// n个点 出发点是s
	memset(vis,0,sizeof(vis));
	memset(dis, 63, sizeof(dis));
	dis[s] = 0;
	for (int i = 1; i <= n; i++) {
		int u = 0, mind = 0x3f3f3f3f;
		// 从全部未找过的点中找 最短路长度最小的u
		for (int j = 1; j <= n; j++)
			if (!vis[j] && dis[j] < mind)
				u = j, mind = dis[j];
		vis[u] = true;
		// 对加入的u的所有出边 松弛
		for (auto ed : e[u]) {
			int v = ed.v, w = ed.w;
			if (dis[v] > dis[u] + w)
				dis[v] = dis[u] + w;
		}
	}
}

int main() {
	int n,k,qu;
	cin>>n>>k>>qu;
	for(int i=0;i<k;++i){
		int u,v,w;cin>>u>>v>>w;
		edge temp={v,w};
		e[u].push_back(temp);
	}
	for(int i=0;i<qu;++i){
		int u,v;cin>>u>>v;
		dijkstra_baoli(n,u);
		if(dis[v]<0x3f3f3f3f)
			cout<<dis[v]<<endl;
		else
			cout<<-1<<endl;
	}

	return 0;
}
```

‍

# Robot（最短路）

‍二维的走迷宫问题

技巧是：某个点的移动是利用向量dx，dy来移动

##### bfs广搜

用了优先队列 还可以在结束条件设为“遍历到了目标节点” 剪枝

```
const int N = 110;
int n, m;
int s1, s2, t1, t2;
int g[N][N];     //  地图权重数组
int d[N][N];     //  距离数组 初始化为-1 也可以用来标记有没有遍历过
struct node {
	int x;
	int y;
	int w;
	node(int a, int b, int c) : x(a), y(b), w(c) {}
	friend bool operator>(const node &a, const node &b){
		return a.w > b.w;
	}
};
int dx[4] = {-1, 0, 1, 0}, dy[4] = {0, 1, 0, -1};

int bfs(int sx, int sy, int tx, int ty) {
	priority_queue<node, vector<node>, greater<node>> q;
	q.push(node(sx, sy, g[sx][sy]));

	memset(d, -1, sizeof(d));
	d[sx][sy] = g[sx][sy];

	auto t = q.top();
        // 剪枝
	while (d[tx][ty]==-1) {
		q.pop();

		for (int i = 0; i < 4; i++) {
			int x = t.x + dx[i], y = t.y + dy[i];
			if (x >= 1 && x <= n && y >= 1 && y <= m && d[x][y] == -1) {
				d[x][y] = d[t.x][t.y] + g[x][y];
				q.push(node(x, y, g[x][y]));
			}
		}
		t=q.top();
	}
	return d[tx][ty];
}

int main() {
	int t;
	cin >> t;
	while (t--) {
		cin >> n >> m;
		::memset(g, 0, sizeof(g));
		for (int i = 1; i <= n; i++)
			for (int j = 1; j <= m; j++)
				cin >> g[i][j];
		cin >> s1 >> s2 >> t1 >> t2;
		cout << bfs(s1, s2, t1, t2) << endl;
	}

	return 0;
}
```

##### dijkstra

```
#define INF 0x3f3f3f3f
int fuels[105][105];

void dijkstra(vector<vector<pair<int, int>>> &graph, vector<int> &dist, int n, int source) {
  vector<bool> visited(n + 2, false);
  priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
  // 初始顶点
  pq.push(make_pair(0, source));
  dist[source] = 0;

  while (!pq.empty()) {
	int min_w = pq.top().first, v = pq.top().second;
	pq.pop();
	if (visited[v])
	  continue;
	visited[v] = true;
	for (size_t i = 0; i < graph[v].size(); i++) {
	  if (dist[graph[v][i].second] > min_w + graph[v][i].first) {
		dist[graph[v][i].second] = min_w + graph[v][i].first;
		pq.push(make_pair(dist[graph[v][i].second], graph[v][i].second));
	  }
	}
  }
}

int main(void) {
  int t;
  cin >> t;
  int dir_x[4] = {1, 0, -1, 0};
  int dir_y[4] = {0, 1, 0, -1};
  while (t--) {
	int r, c, x1, y1, x2, y2;
	cin >> r >> c;
	int k = 1;
	vector<vector<int>> id(r + 1, vector<int>(c + 1, 0));
	for (int i = 1; i <= r; i++) {
	  for (int j = 1; j <= c; j++) {
		cin >> fuels[i][j];
		id[i][j] = k++;
	  }
	}
	cin >> x1 >> y1 >> x2 >> y2;
	vector<vector<pair<int, int>>> graph(r * c + 2);
	for (int i = 1; i <= r; i++) {
	  for (int j = 1; j <= c; j++) {
		for (int k = 0; k < 4; k++) {
		  int x = i + dir_x[k];
		  int y = j + dir_y[k];
		  if (x >= 1 && x <= r && y >= 1 && y <= c)
			graph[id[i][j]].push_back(make_pair(fuels[x][y], id[x][y]));
		}
	  }
	}
	vector<int> dist(id[r][c] + 2, INF);
	dijkstra(graph, dist, r * c, id[x1][y1]);
	cout << dist[id[x2][y2]] + fuels[x1][y1] << endl;
  }
  return 0;
}
```

‍答案做法

```
#include <iostream>  
#include <cstring>  
#include <queue>  
using namespace std;  
int dir_x[] = {-1, 0, 1, 0};  
int dir_y[] = {0, 1, 0, -1};  
struct Node {  
    int x;  
    int y;  
    int cost;  
    Node(int a, int b, int c) {  
        x = a;  
        y = b;  
        cost = c;  
    }  
    friend bool operator < (Node a, Node b) {  
        return a.cost > b.cost;   
    }  
};  
  
int main() {  
    int t;  
    int city[101][101];  
    bool visit[101][101];      
    cin >> t;  
    while (t--) {  
        int m, n;  
        cin >> m >> n;  
        memset(visit, false, sizeof(visit));  
        for (int i = 1; i <= m; i++) {  
            for (int j = 1; j <= n; j++) {  
                cin >> city[i][j];  
            }  
        }  
        int s_x, s_y, e_x, e_y;  
        cin >> s_x >> s_y >> e_x >> e_y;  
        visit[s_x][s_y] = true;  
        priority_queue<Node> q;  
        q.push(Node(s_x, s_y, city[s_x][s_y]));  
        Node top = q.top();    
        while (!visit[e_x][e_y]) {  
            for (int i = 0; i < 4; i++) {  
                int x = top.x + dir_x[i];  
                int y = top.y + dir_y[i];  
                if (x >= 1 && x <= m && y >= 1 && y <= n && !visit[x][y]) {  
                    q.push(Node(x, y, top.cost + city[x][y]));  
                }  
            }  
            top = q.top();    
            while (visit[top.x][top.y]) {  
                q.pop();  
                top = q.top();;  
            }  
            visit[top.x][top.y] = true;  
        }  
        cout << top.cost << endl;  
    }  
    return 0;  
}
```

##### 

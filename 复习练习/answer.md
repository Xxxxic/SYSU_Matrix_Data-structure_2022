---
title: 小测练习
date: 2023-03-04T14:11:06Z
lastmod: 2023-03-04T14:22:09Z

---

# 小测练习

# mid_ex1

字典树

```
#include<iostream>
#include<string>
using namespace std;
const int N=1e6+10;

int s[N][26],cnt[N],idx;
void add(char *str){
	int p=0;
	for(int i=0;str[i];i++){
		int j=str[i]-'a';
		if(!s[p][j]) s[p][j]=++idx;
		cnt[p]++;       //每次过就+1
		p=s[p][j];
	}
	cnt[p]++;
}
int query(char* str){
	int p=0;
	for(int i=0;str[i];i++){
		int j=str[i]-'a';
		if(!s[p][j]) return cnt[p];     //没有了就返回
		p=s[p][j];
	}
	return cnt[p];
}

int n,m;
int main(){
	scanf("%d",&n);
	for(int i=0;i<n;i++){
		char str[22];
		scanf("%s",str);
		add(str);
	}
	scanf("%d",&m);
	for(int i=0;i<m;i++){
		char str[22];
		scanf("%s",str);
		printf("%d\n",query(str));
	}

	return 0;
}
```



# mid_ex2

数组模拟双向链表

```
#include<bits/stdc++.h>
using namespace std;

//数据从1-n 直接拿下标表示
int r[1000000], l[1000000];

int main()
{
    int n, m;
    cin >> n >> m;
    for (int i = 0; i <= n + 1; ++i)    //初始化头r[0] 中间 尾l[n+1]
        r[i] = i + 1, l[i] = i - 1;
    while (m--) {
        int op, u;
        cin >> op >> u;
        //将u从原来删掉
        l[r[u]] = l[u];
        r[l[u]] = r[u];
        switch (op) {
        case 1: {
            //将u插入0后
            r[u] = r[0];
            l[u] = 0;
            l[r[0]] = u;
            r[0] = u;
            break;
        }
        case 2: {
            //将u插入n+1前
            r[u] = n + 1;
            l[u] = l[n + 1];
            r[l[n + 1]] = u;
            l[n + 1] = u;
            break;
        }
        case 3: {
            int v;
            cin >> v;
            //将u插入v后
            r[u] = r[v];
            l[u] = v;
            l[r[v]] = u;
            r[v] = u;
            break;
        }
        }
    }
    for(int i = r[0]; r[i] != n + 2; i = r[i])
	    cout << i << ' ';

    return 0;
}
```



# mid_ex3

```
#include<cstdio>
#include<algorithm>
using namespace std;

const int maxl=5e5+10;

int n;
int a[maxl];

int main()
{
	scanf("%d",&n);
	for(int i=1;i<=n;i++)
		scanf("%d",&a[i]);
	sort(a+1,a+1+n);
	int ans;
	if(n&1)
		ans=a[n/2+1];
	else
		ans=(a[n/2]+a[n/2+1])/2;
	printf("%d\n",ans);
	return 0;
}

```



# mid_ex4

解方程 或者浮点数二分

```
#include<bits/stdc++.h>
using namespace std;

int main()
{
    unsigned long long n, m;
    cin >> n >> m;
    unsigned long long x = (sqrt(9 + 8 * (m + n)) - 3) / 2;
    cout << n - x;
    

    return 0;
}
```



# 小测1 - 字符串的反转

‍字符分割+栈

```
#include <iostream>
#include <string>
using namespace std;
const int N=1e6+10;

char stk[N];
int tt;

int main()
{  
    string s;
    getline(cin,s);
    for(int i=0;i<s.size();i++){
        int j=i;
        while(j<s.size()&&s[j]!=' '){
            stk[++tt]=s[j];
            j++;
        }
        while(tt){
            cout<<stk[tt];
            tt--;
        }
        cout<<' ';
        i=j;
    }
}
```



# 小测2 - 数一数叶数

二叉树：分左右递归

```
#include "BinaryNode.h"

int leaves(const BinaryNode* root)
{
    if(!root)
        return 0;
    else if(!root->left && !root->right)
        return 1;
    else
        return leaves(root->left)+leaves(root->right);
}

```



# 小测3 - 求两个集合的交集

‍类似归并排序的合并

```
#include "SeqList.h"

//LC是LA和LB表示集合的交集
void merge(SeqList *LA, SeqList *LB, SeqList *LC)
{
    LC->last=-1;
    int cnt1=0,cnt2=0;
    while(cnt1<=LA->last && cnt2<=LB->last)
    {
        if(LA->elem[cnt1]==LB->elem[cnt2])
        {
            LC->elem[++LC->last]=LA->elem[cnt1];
            cnt1++;
            cnt2++;
        }
        else if(LA->elem[cnt1]>LB->elem[cnt2])
            cnt2++;
        else
            cnt1++;
    }
}
```





# 小测4 - 检查一个序列是否构成堆

定义

```
#include<bits/stdc++.h>
using namespace std;
// 注意i不能从0开始
bool judgemax(int a[], int n) {
	for (int i = 1; i < n / 2; ++i)
		if (a[i] < a[2 * i] || (2 * i + 1 < n && a[i] < a[2 * i + 1]))
			return false;
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
	int nums[n + 1];
	nums[0] = 0;
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





# 小测5 - 验证回文字符串

递归做法（未验证正误）

```
#include<iostream>
using namespace std;

string s;
int judge(int i, int j, int in) {
	int flag = 1;
	while (i < j) {
		if (s[i] == s[j]) {
			i++;
			j--;
		} else if (in && s[i] != s[j]){
			flag = 0;
			break;
		}
		else {
			flag = judge(i + 1, j, 1) || judge(i, j - 1, 1);
			break;
		}
	}
	return flag;
}

int main() {
	cin >> s;
	int len = s.size();
	int i = 0, j = len - 1;

	cout << judge(i, j, 0) << endl;

	return 0;
}
```

直接做法

```
#include <bits/stdc++.h>
using namespace std;

bool judge(string str) {
	int begin = 0, end = str.length() - 1;
	while (begin < end) {
		if (str[begin] != str[end])
			return false;
		begin++;
		end--;
	}
	return true;
}

int main() {
	string str;
	cin >> str;
	int flag = 0;
	for (int i = 0; i < str.length(); ++i) {
		string temp = str;
		temp.erase(temp.begin() + i);
		if (judge(temp)) {
			flag = 1;
			break;
		}
	}
	cout << flag ? 1 : 0;

	return 0;
}
```





# 小测6 - 最长有效括号

```
#include <bits/stdc++.h>
using namespace std;


int main()
{
    string s;
    cin>>s;
    stack<int>st;
    int res = 0;
    for(int i = 0;i<s.size();++i)
    {
        if(s[i]=='(')st.push(i);
        else
        {
            if(st.empty() || s[st.top()]==')') 
                st.push(i);
            else
            {
                st.pop();
                if(st.empty())
                    res = max(res,i+1);
                else 
                    res = max(res,i-st.top());
            }
        }
    }
    cout<<res;

  return 0;
}
```

‍

# 小测7 - 坐缆车

也是最短路

短点的floyd：

```
#include <iostream>
#include <cstring>
using namespace std;
const int N = 210;
const int inf=0x3f3f3f3f;

int n;
int d[N][N];
void floyd(){
	for(int k=1;k<=n;k++)
		for(int i=1;i<=n;i++)
			for(int j=1;j<=n;j++)
				if(d[i][j]>d[i][k]+d[k][j])
					d[i][j]=d[i][k]+d[k][j];
}

int main(){
	cin>>n;
	::memset(d,0x3f,sizeof(d));
	for(int i=1;i<=n;i++)
		for(int j=1;j<=n;j++)
			if(j>i){
				int t;cin>>t;
				d[i][j]=min(d[i][j],t);
			}

	floyd();
	cout<<d[1][n];

	return 0;
}
```



# 小测8 - 最短路径

和之前的机器人差不多，广搜或者dijkstra都行

```
#include<iostream>
using namespace std;
#define INF 0x3f3f3f3f

struct note {
	int x;
	int y;
	int s;
};

int main() {
    int n, m;
    cin >> n >> m;
    struct note que[n * m + 1];
    int a[n + 1][m + 1] = { 0 }, book[n + 1][m + 1] = { 0 };
    
    for (int i = 1; i <= n; i++) {
		for (int j = 1; j <= m; j++) {
			cin >> a[i][j];
		}
    }
    int next[4][2] = {
		{0,1},
		{1,0},
		{0,-1},
		{-1,0}
    };
    
    int head = 1, tail = 1;
	int u1, v1, u2, v2, tx, ty, flag;
	cin >> u1 >> v1 >> u2 >> v2;

    for (int i = 0; i < n * m + 1; i++)que[i].s = INF;
    que[tail].x = u1;
	que[tail].y = v1;
	que[tail].s = 0;
	tail++;
	book[u1][v1] = 1;
    flag = 0;
    
	while (head < tail) {
        for (int k = 0; k <= 3; k++) {
            tx = que[head].x + next[k][0];
			ty = que[head].y + next[k][1];
			if (tx<1 || ty<1 || tx>n || ty>m) {
				continue;
			}
			if (a[tx][ty] == 0 && book[tx][ty] == 0) {
				
				book[tx][ty] = 1;
				
				que[tail].x = tx;
				que[tail].y = ty;
				que[tail].s = que[head].s + 1;
				tail++;
			}
			if (tx == u2 && ty == v2) {
				flag = 1;
				break;
			}
        }
        if (flag == 1) {
			break;
		}
		head++;
    }
    if (book[u2][v2])cout << que[tail - 1].s << endl;
    else cout << "No" << endl;
    return 0;
}
```



‍

# 练习1

```
#include "getFirstPublicNode.h"
ListNode* getFirstPublicNode(ListNode *headA, ListNode *headB) {
    if(!headA||!headB) 
        return NULL;
    ListNode *t1=headA;
    ListNode *t2=headB;
    while(t1!=t2){
        t1=(t1->next==NULL)?headB:t1->next;
        t2=(t2->next==NULL)?headA:t2->next;
    }
    return t1;
}
```



‍

# 练习2

字典树做法：注意有个问题就是string数组开太大的话会卡住

```
#include <string>
#include <iostream>
using namespace std;

const int N = 100000;
int son[N][26], idx;
string st[1000];
string s1, s2;
string s;
void insert(string word, string word_) {
	int p = 0;
	for (auto c : word) {
		int j = c - 'a';
		if (!son[p][j]) son[p][j] = ++idx;
		p = son[p][j];
	}
	st[p] = word_;
}
string find(string word) {
	int p = 0;
	for (auto c : word) {
		int j = c - 'a';
		if (!son[p][j]) return "eh";
		p = son[p][j];
	}
	return st[p];
}

int main() {
	getline(cin, s);
	while (s != "") {
		int i = 0;
		while (s[i] != ' ') i++;
		s1 = s.substr(0, i);
		s2 = s.substr(i + 1);
		insert(s2, s1);
		getline(cin, s);
	}
	while (cin >> s2) cout << find(s2) << endl;

	return 0;
}
```

暴力map做法：

```
#include<iostream>
#include<map>
#include <string>
#include <cstdio>

using namespace std;

int main()

{
    string str1, str2, str;
    map<string, string> m;
    map<string, string>::iterator it;
    while(1)
    {
        cin>>str1;
        if(getchar()!=' ')
            break;
        cin>>str2;
        m[str2] = str1;
    }
    do
    {
        it = m.find(str1);
        if(it==m.end())
            cout<<"eh"<<endl;
        else
            cout<<m[str1]<<endl;
    }
    while(cin>>str1);
    return 0;
}
```



# 练习3

```
#include <string>
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>
#include <cstdlib>
#include <map>
using namespace std;

bool cmp1(int x,int y){
    return x>y;
}
bool cmp2(int x,int y){
    return x<y;
}

int main()
{
    int n,q;
    while(cin>>n>>q)
    {
        int cnt=0;          //箱子使用个数
        int goods[n];
        int box[n];
        for(int i=0;i<n;++i){
            cin>>goods[i];
            box[i]=q;
        }
        sort(goods,goods+n,cmp1);
        for(int i=0;i<n;i++){
            sort(box,box+n,cmp2);
            //找到剩余空间最小的箱子
            int t=0;
            while(box[t]<goods[i])
                t++;
            box[t]-=goods[i];
        }
        for(int i=0;i<n;++i,++cnt)
            if(box[i]==q)
                break;
        cout<<cnt<<endl;
    }

    return 0;
}
```



‍

# 练习4

```
#include "TreeNode.h"
#include<iostream>
using namespace std;

int maxAns;

/* 0 => left, 1 => right */
void dfs(TreeNode* o, bool dir, int len)
{
    maxAns = max(maxAns, len);
    if (!dir)
    {
        if (o->left) dfs(o->left, 1, len + 1);
        if (o->right) dfs(o->right, 0, 1);
    }
    else
    {
        if (o->right) dfs(o->right, 0, len + 1);
        if (o->left) dfs(o->left, 1, 1);
    }
}

int longestZigZag(TreeNode* root)
{
    if (!root) return 0;
    maxAns = 0;
    dfs(root, 0, 0);
    dfs(root, 1, 0);
    return maxAns;
}
```

‍

# 练习5

```
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
		memset(e, 0, sizeof(e));
		cnt = 0;
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





# 习题1 - 飞盘高手

数组优化方法

```
#include<iostream>
using namespace std;
const int N=1e6+10;

int q[N],hh=0,tt=0;


int main()
{
    int t;
    cin>>t;
    while(t--)
    {
        int n;
        cin>>n;
        for(int i=1;i<=n;++i)
            q[i]=i;
        hh=1;
        tt=n+1;
        while(hh!=tt)
        {
            cout<<q[hh]<<' ';
            hh++;
            q[tt++]=q[hh];
            hh++;
        }
        cout<<endl;
    }

    return 0;
}
```

‍直接stl：

```
#include<iostream>
#include<queue>
using namespace std;
int main()
{
    int t;
    cin>>t;
    while(t--)
    {
        int n;
        cin>>n;
        queue<int>q;
        for(int i=1;i<=n;++i)
            q.push(i);
        while(q.size()>1)
        {
            cout<<q.front()<<' ';
            q.pop();
            q.push(q.front());
            q.pop();
        }
        cout<<q.front()<<endl;
    }

    return 0;
}
```



# 习题2 - 畅通工程

### 多源汇floyd

```
#include<iostream>
#include<cstring>
#include<queue>
using namespace std;
// 邻接矩阵要注意这个
const int N = 210;
const int INF = 0x3f3f3f3f;
typedef pair<int, int> PII;

int n, m;
int d[N][N];
void floyd() {
	for (int k = 0; k < n; k++)
		for (int i = 0; i < n; i++)
			for (int j = 0; j < n; j++)
				d[i][j] = min(d[i][j], d[i][k] + d[k][j]);
}

int main() {
	while (scanf("%d%d", &n, &m) != EOF) {
		for (int i = 0; i < n; i++)
			for (int j = 0; j < n; j++)
				if (i == j) d[i][j] = 0;
				else d[i][j] = INF;
		while (m--) {
			int a, b, c;
			scanf("%d%d%d", &a, &b, &c);
			d[a][b] = min(d[a][b], c);
			d[b][a] = min(d[b][a], c);
		}
		floyd();

		int s, t;
		scanf("%d%d", &s, &t);
		if (d[s][t] == INF) printf("-1\n");
		else printf("%d\n", d[s][t]);
	}

	return 0;
}
```

### dijkstra 从x点出发

```
#include<iostream>
#include<cstring>
#include<queue>
using namespace std;
const int N = 1e6 + 10;
const int INF = 0x3f3f3f3f;
typedef pair<int, int> PII;

int n, m;
int s, t;
int h[N], e[N], ne[N], w[N], idx;
void add(int a, int b, int c) {
	e[idx] = b, w[idx] = c, ne[idx] = h[a], h[a] = idx++;
}
int dist[N], st[N];
int dijkstra(int x) {
	memset(dist, 0x3f, sizeof(dist));
	dist[x] = 0;

	priority_queue<PII, vector<PII>, greater<PII>> heap;
	heap.push({0, x});

	while (heap.size()) {
		auto t = heap.top();
		int ver = t.second, distance = t.first;
		heap.pop();

		if (st[ver]) continue;
		st[ver] = true;

		for (int i = h[ver]; i != -1; i = ne[i]) {
			int j = e[i];
			if (dist[j] > distance + w[i]){
				dist[j] = distance + w[i];
				heap.push({dist[j], j});
			}
		}
	}

	if(dist[t]==INF) return -1;
	else return dist[t];
}

int main() {
	while (scanf("%d%d", &n, &m) != EOF) {
		memset(h, -1, sizeof(h));
		while (m--) {
			int a, b, c;
			scanf("%d%d%d", &a, &b, &c);
			add(a, b, c);
			add(b, a, c);
		}
		scanf("%d%d", &s, &t);
		printf("%d\n", dijkstra(s));
	}

	return 0;
}
```

‍

# 习题3 - 简单字符串匹配

BF算法

```
#include<iostream>
#include<string>
using namespace std;

string s1,s2,s;
int bf(){
    int i=0,j=0;
    while(i<s.size()&&j<s2.size()){
        if(s[i]==s2[j]){
            i++;
            j++;
        }
        else{
            i=i-j+1;
            j=0;
        }
    }
    if(j==s2.size())
        return i-j;
    else
        return -1;
}

int main(){
    int n;
    cin>>n;
    while(n--)
    {
        cin>>s1>>s2;
        s=s1+s1;
        if(bf()==-1)
            cout<<"False"<<endl;
        else
            cout<<"True"<<endl;
    }
}
```

两字符拼接：

```
#include<iostream>
#include<string>
using namespace std;

int main(){
    int n;
    cin>>n;
    while(n--)
    {
        string s1,s2,s;
        cin>>s1>>s2;
        s=s1+s1;
        string::size_type idx=s.find(s2);
        if(idx==string::npos)
            cout<<"False"<<endl;
        else
            cout<<"True"<<endl;
    }
}
```



# 习题4 - 简单哈希

‍开放寻址法：数组模拟

```
#include<iostream>
#include<vector>
using namespace std;
const int N=1e6+3;
const int INF=0x3f3f3f3f;

int h[N];
int n,m;
int find(int x){
	int k=(x%m+m)%m;
	while(h[k]!=INF&&h[k]!=x){
		k++;
		if(k==m) k=0;
	}
	return k;
}


int main(){
	memset(h,0x3f,sizeof(h));
	scanf("%d%d",&n,&m);
	for(int i=0;i<n;i++) {
		int t;
		scanf("%d",&t);
		int k=find(t);
		h[k]=t;
	}


	for(int i=0;i<m;i++)
		if(h[i]==INF) printf("%d#NULL\n",i);
		else printf("%d$%d\n",i,h[i]);

	return 0;
}
```

‍

# 习题5 - 第二小数

就蒽sort？

```
#include<iostream>
#include<algorithm>
using namespace std;

int main()
{
    int n;
    cin>>n;
    int num[n];
    for(int i=0;i<n;++i){
        int t;cin>>t;
        num[i]=t;
    }
    sort(num,num+n);
    cout<<num[1];

    return 0;
}
```



‍

# 习题6 - 栈

O(1)求栈最大最小值

维护一个单调栈（不符合不入栈） 使栈顶是最大最小值
push pop判断空
pop：``if (s.top() == s_m.top()) s_m.pop();``

```
int n;
int main() {
	while (cin>>n) {
		stack<int> s;
		stack<int> s_m;
		while (n--) {
			int op;
			cin >> op;
			if (op == 0) {
				int x;
				cin >> x;
				s.push(x);
				if (s_m.empty() || x <= s_m.top()) s_m.push(x);
			} else if (op == 1) {
				if(s.empty()) continue;
				if (s.top() == s_m.top()) s_m.pop();
				s.pop();
			} else if (op == 2) {
				if (s.empty()) cout << -1 << endl;
				else cout << s.top() << endl;
			} else if (op == 3) {
				if (s_m.empty()) cout << -1 << endl;
				else cout << s_m.top() << endl;
			}
		}
	}

	return 0;
}
```

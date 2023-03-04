---
title: answer
date: 2023-01-10T20:43:12Z
lastmod: 2023-01-10T20:53:32Z
---

# answer

# postorder

```cpp
#include <iostream>

using namespace std;

int cnt;

void postOrder(int* pre, int* in, int len);

int main()
{
    int n, num;
    cin >> n;
    cnt = n;
    int *preOrder = new int[n];
    int *inOrder = new int[n];  
    for (int i = 0; i < n; ++i) {
        cin >> preOrder[i];
    }
    for (int i = 0; i < n; ++i) {
        cin >> inOrder[i];
    }
    postOrder(inOrder, preOrder, n);
    cout << endl;
    delete[]preOrder;
    delete[]inOrder;
    return 0;
}

void postOrder(int* inOrder, int* preOrder, int len)
{
    if (len == 0)
        return;
    int root = *preOrder;
    int rootIndex = 0;
    for (; rootIndex < len; ++rootIndex) {
        if (inOrder[rootIndex] == *preOrder)
            break;
    }
    postOrder(inOrder, preOrder + 1, rootIndex);
    postOrder(inOrder + rootIndex + 1, preOrder + rootIndex + 1, len - (rootIndex + 1));
    cout << root;
    cnt--;
    if (cnt)
        cout << ' ';
}
```

## my answer

```cpp
#include<bits/stdc++.h>
using namespace std;

struct Node  
{  
    Node* l;  
    Node* r;  
    int c;  
};  

void postorder(int* A,int* B, int n)  
{  
    if(n <= 0)  
        return;  
    int node_value = B[0];  
    int llen = 0;  
    for(;llen < n; llen++)  {  
        if(A[llen] == B[0])  
        break;  
    }  
    postorder(A, B+1, llen);  
    postorder(A+llen+1, B+llen+1, n-(llen+1));  
    cout<<node_value<<' ';  
    return;  
}  

int main()
{
    int n;
    cin>>n;
    int A[n];
    int B[n];
    for(int i=0;i<n;++i)
        cin>>B[i];
    for(int i=0;i<n;++i)
        cin>>A[i];
  
    postorder(A, B, n);  

    return 0;
}
```

‍

# Play with Tree

```cpp
#include<iostream>
#include "play.h"
using namespace std;


int Height(const Node *root)  
{  
    int lheight, rheight;  
    if(root== NULL)  
        return 0;  
    else  
    {  
        lheight = Height(root->lc) + 1;  
        rheight = Height(root->rc) + 1;  
    }  
    if(lheight>rheight)
    return lheight;
    else
    return rheight;
}  

int count(const Node*root)
{
    if(root==0) return 0;
    return count(root->lc) + count(root->rc) + 1;
}


void query(const Node *root, int &size, int &height)
{ size=count(root);
    height=Height(root);
  
}
```

## my answer

```cpp
#include<bits/stdc++.h>
#include<play.h>
using namespace std;

int preorder(const Node* cur) {
	if (!cur)
        return 0;
    return preorder(cur->lc) + preorder(cur->rc) + 1;
}
int gettreeheight(const Node* cur){
    if(!cur)
        return 0;
    int lh=gettreeheight(cur->lc);
    int rh=gettreeheight(cur->rc);
    return max(lh,rh)+1;
}

void query(const Node *root, int &size, int &height)
{
    size=preorder(root);
    height=gettreeheight(root);
}

```

‍

# 二叉搜索树的遍历

```cpp
#include <iostream>
using namespace std;

struct BSTnode{
    int data;
    BSTnode *lchild;
    BSTnode *rchild;
};

void insert(BSTnode *root,int add)
{
    BSTnode *temp,*p;
    temp = root;
    while(1)
    {
        if(add > temp->data)
        {
            if(temp->rchild == NULL)
            {
                p = new BSTnode;
                p->data = add;
                p->lchild = NULL;
                p->rchild = NULL;
                temp->rchild = p;
                break;
            }
            else temp = temp->rchild;  
        }
        else
        {
            if(temp->lchild == NULL)
            {
                p = new BSTnode;
                p->data = add;
                p->lchild = NULL;
                p->rchild = NULL;
                temp->lchild = p;
                break;
            }
            else temp = temp->lchild;
        }   
    }
  
}

void preorder(BSTnode *temp)
{
    if(temp != NULL)
    {
        cout<<temp->data<<" ";
        preorder(temp->lchild);
        preorder(temp->rchild);
    }
}

void inorder(BSTnode *temp)
{
    if(temp != NULL)
    {
        inorder(temp->lchild);
        cout<<temp->data<<" ";
        inorder(temp->rchild);
    }
}

int main()
{ 
    int n,m;
    while(cin>>n)
    {
        if(n==0) 
        break;
        else
        {
            BSTnode *root;
            root = new BSTnode;
            root->lchild = NULL;
            root->rchild = NULL;
          
            cin>>m;
            root->data = m;  
            for(int i=0;i<n-1;i++)
            {
                cin>>m;
                insert(root,m);
            }
            inorder(root);
            cout<<endl;
            preorder(root); 
            cout<<endl;
        }
    }
}
```

## my answer

```cpp
#include<bits/stdc++.h>
using namespace std;

struct Node {
  Node *l, *r;
  int data;
  Node(int x) : l(nullptr), r(nullptr), data(x) {}
};

class bst {
 public:
  Node *root;
  void insert(int x) {
	if (root == nullptr) {
	  root = new Node(x);
	  return;
	}
	Node *cur = root;
	while (cur != nullptr) {
	  if (x > cur->data) {
		if (cur->r == nullptr) {
		  cur->r = new Node(x);
		  return;
		} else {
		  cur = cur->r;
		}
	  } else {
		if (cur->l == nullptr) {
		  cur->l = new Node(x);
		  return;
		} else {
		  cur = cur->l;
		}
	  }
	}
  }
  void inorder(Node* cur) {
	if (cur != nullptr){
	  inorder(cur->l);
	  cout<<cur->data<<' ';
	  inorder(cur->r);
	}
  }
  void preorder(Node* cur) {
	if (cur != nullptr) {
	  cout << cur->data << ' ';
	  preorder(cur->l);
	  preorder(cur->r);
	}
  }
};

int main() {
  int m;
  while (cin >> m && m != 0) {
	bst tree;
	tree.root = nullptr;
	int num;
	for (int i = 0; i < m; ++i) {
	  cin >> num;
	  tree.insert(num);
	}
	tree.inorder(tree.root);
	cout<<endl;
	tree.preorder(tree.root);
	cout<<endl;
  }

  return 0;
}
```

‍

# Huffman coding

```cpp
#include <iostream>  
#include <queue>  
#include <vector>  
using namespace std;
struct cmp {
    bool operator()(int a, int b)
    {
        return a > b;
    }
};
int main()
{
    int n, frequency, BT = 0;
    char character;
    priority_queue<int, vector<int>, cmp> f; 
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> character >> frequency;
        f.push(frequency);
    }
    while (f.size()>1) {
        int tmp1, tmp2, tmp;
        tmp1 = f.top();
        f.pop();
        tmp2 = f.top();
        f.pop();
        tmp = tmp1 + tmp2;
        f.push(tmp); 
        BT = tmp1 + tmp2 + BT;
    }
    cout << BT << endl;
    return 0;
}

```

## my answer

```cpp
#include<bits/stdc++.h>
using namespace std;

int main() {
  vector<int>nums;
  int t;
  //并没有用到c 但是c++不能往int里输入char
  char c;
  int n;
  cin>>n;
  if(n==0){
	cout<<0<<endl;
	return 0;
  }
  for(int i=0;i<n;++i){
	cin>>c>>t;
	nums.push_back(t);
  }
  if(n==1){
	cout<<t<<endl;
	return 0;
  }
  sort(nums.begin(),nums.end());
  
  int ans=0;
  while(nums.size()>1)
  {
	int tem=nums[0]+nums[1];
	ans+=tem;
	nums.erase(nums.begin());
	nums.erase(nums.begin());
	nums.push_back(tem);
	sort(nums.begin(),nums.end());
  }
  cout<<ans<<endl;

  return 0;
}
```

‍

# 判断二叉查找树是否平衡

```cpp
#include <iostream>
#include <vector>

using namespace std;

typedef int T;
struct BinaryNode{
  T data; //store data
  BinaryNode *left, *right;
  BinaryNode(T d, BinaryNode *l=NULL, BinaryNode* r=NULL):data(d), left(l), right(r) {};
};

//#include "source.cpp"


void insert(BinaryNode* &root, T x){
  if (root==NULL)
     root = new BinaryNode(x);
  else if (x < root->data)
     insert(root->left,x);
  else insert(root->right, x);
  
}

int height(BinaryNode *root){
    if (root==NULL)
      return -1;
    else
      return 1 + max(height(root->left), height(root->right));
}
bool isAVL(BinaryNode *root){
    if (root==NULL)
       return true;
    else
       return (abs(height(root->left)-height(root->right))<=1) && isAVL(root->left)&& isAVL(root->right);
}

void clear(BinaryNode*root){
  if (root){
    clear(root->left);clear(root->right);
    delete root;
  }
}

int main(){
  int m, n,x;
  bool b;
  cin >> m;
  while (m--) {
    cin >> n;
    BinaryNode *root = NULL;
    for (int i=0;i<n;i++){
      cin >>x;
      insert(root, x);
     //b1 = isRegularBT(root);
      b = isAVL(root);
//cout<<"after insert "<<x<<":"<<b1<<endl;
    }
      if (b)
        cout <<"YES"<<endl;
      else
        cout <<"NO"<<endl;
  
   clear(root);  
 }
  return 0;
}


```

## my answer

```cpp
#include<bits/stdc++.h>
using namespace std;

//对于先序遍历中每个数x 右边：小于x的为其左子树 大于x的为其右子树  两者高度需要差不超过2
//题目转化为 递归求平衡因子
int height(vector<int> &a, int begin, int end, bool& flag) {
  if (begin > end || end >= a.size()) return 0;
  if (begin == end) return 1;  
  int rbegin = begin + 1;
  for (; rbegin <= end; ++rbegin)
	if (a[rbegin] > a[begin]) break;
  int lh = height(a, begin + 1, rbegin - 1, flag);
  int rh = height(a, rbegin, end, flag);
  if (fabs(lh - rh) >= 2) flag = false;
  return max(lh, rh) + 1;
}

int main() {
  int m, n;
  cin >> m;
  while (m--) {
	cin >> n;
	bool flag = true;
	vector<int> nums;
	int t;
	for (int i = 0; i < n; ++i) {
	  cin >> t;
	  nums.push_back(t);
	}
	int hei = height(nums, 0, n - 1, flag);
	if (flag == 0) cout << "NO" << endl;
	else cout << "YES" << endl;
  }

  return 0;
}
```

‍

# 多叉树与二叉树

```cpp
#include<bits/stdc++.h>
#define LL long long
#define dl double
#define Pi pair<int,int>
#define SZ(a) ((int)a.size())
using namespace std;

const int N = 1e5 + 10;

int n,l[N],r[N];
vector<int>e[N];
void dfs1(int x){
  if(SZ(e[x]) == 0)return ;
  l[x] = e[x][0];
  for(int i = 0;i < SZ(e[x]) - 1;i++)r[e[x][i]] = e[x][i + 1];
  for(auto v : e[x])dfs1(v);
}
vector<int>id[N];
void dfs2(int x,int dep){
  id[dep].push_back(x);
  if(l[x])dfs2(l[x],dep + 1);
  if(r[x])dfs2(r[x],dep + 1);
}

int main(){

  cin >> n;
  for(int i = 2;i <= n;i++){
    int x;cin >> x;e[x].push_back(i);
  }
  for(int i = 1;i <= n;i++)sort(e[i].begin(),e[i].end());
  dfs1(1);dfs2(1,0);
  for(int i = 0;i < N;i++)
    for(auto x : id[i])cout << x << " ";
  cout << endl;
  return 0;
}
/**/

```

## my answer

```cpp
#include<bits/stdc++.h>
using namespace std;

struct node{
  int l;	//left-child：child
  int r;	//right-child：bro
  node():l(0),r(0) {}
};

int main() {
  int n;
  cin>>n;
  node tree[n+1];	//1-n
  for(int i=2;i<=n;++i){
	int t;
	cin>>t;					//i是t的孩子
	if(tree[t].l==0)		//二叉树中，t没有儿子，插入l中
	  tree[t].l=i;
	else{
	  int c=tree[t].l;		//根结点的儿子
	  while(tree[c].r)
		c=tree[c].r;		//找到二叉树中 t的最右边儿子 插入其儿子（从小到大）
	  tree[c].r=i;
	}
  }
  queue<int>bfs;
  bfs.push(1);
  while(bfs.size()>0){
	cout<<bfs.front()<<' ';
	if(tree[bfs.front()].l) bfs.push(tree[bfs.front()].l);
	if(tree[bfs.front()].r) bfs.push(tree[bfs.front()].r);
	bfs.pop();
  }

  return 0;
}
```

‍

# 完全二叉树-最近公共祖先

## my answer

```cpp
#include<bits/stdc++.h>
using namespace std;

int main()
{
    int t;cin>>t;
    while(t--){
        int x,y;cin>>x>>y;
        if(x==y) cout<<x<<endl;
        else{
            int ma=max(x,y);
            int mi=min(x,y);
            while(ma!=mi){
                ma/=2;
                if(ma<mi) swap(ma,mi);
            }
            cout<<ma<<endl;
        }
    }

    return 0;
}
```

‍

‍

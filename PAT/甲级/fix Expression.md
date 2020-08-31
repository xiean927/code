

### 1130 Infix Expression (25分)

#### 中序遍历，除了根节点和叶节点之外的其他结点，要加括号
#### [思路，转自CSDN](https://blog.csdn.net/galesaur_wcy/article/details/82354161)
```
#include<iostream>
#include<cstdio>
#include<cstring>
#include<algorithm>
#include<vector>
#include<map>
#include<queue>
using namespace std;
struct node
{
	char data[15];
	int left,right;
}tree[25];
int view[25],root;
void InOrder(int v)
{
    if(v != -1){
        if(v != root && (tree[v].left != -1 || tree[v].right != -1))
			printf("(");
        InOrder(tree[v].left);
        printf("%s ",tree[v].data);
        InOrder(tree[v].right);
        if(v != root && (tree[v].left != -1 || tree[v].right != -1))
		 	printf(")");
    }
}
int main()
{
	int n ;
	scanf("%d",&n);
	for(int i = 1; i <= n; i++)
	{
		scanf("%s %d %d",tree[i].data,&tree[i].left, &tree[i].right);
		view[tree[i].left] = 1;
		view[tree[i].right] = 1;
	}
	for(int i = 1; i <= n; i++)
	{
		if(view[i] == 0)
		{
			root = i ;
			break;
		}
	}
	InOrder(root);
	return 0;
}

```




### 3 Postfix Expression
#### 中缀表达式节点应该有三种状态
* 左右孩子都非空,输出(后序遍历左孩子 + 后序遍历右孩子 + V)
* 左为空右非空时,输出(后序遍历右孩子 + V)，如果子节点只有一个,应该先输出运算符
* 左右都为空时,输出(V)

```
#include <bits/stdc++.h>

using namespace std;

struct node
{
	char data[15];
	int left,right;
}tree[25];

int view[25],root;

void InOrder(int v){
    if(v==-1)
        return ;
    printf("(");///后序表达式
    if(tree[v].left!=-1&&tree[v].right!=-1){
        InOrder(tree[v].left);
        InOrder(tree[v].right);
        printf("%s",tree[v].data);
    }
    ///如果子节点只有一个,应该先输出运算符
    else if(tree[v].left==-1&&tree[v].right!=-1){
        printf("%s",tree[v].data);
        InOrder(tree[v].right);
    }
    else if(tree[v].right==-1&&tree[v].left!=-1)///这个判断可以去掉
        InOrder(tree[v].left);
    else///左右子树均为空
        printf("%s",tree[v].data);
    printf(")");
}

int main()
{
	int n ;
	scanf("%d",&n);
	for(int i = 1; i <= n; i++)
	{
		scanf("%s %d %d",tree[i].data,&tree[i].left, &tree[i].right);
		view[tree[i].left] = 1;
		view[tree[i].right] = 1;
	}
	for(int i = 1; i <= n; i++)
	{
		if(view[i] == 0)
		{
			root = i ;
			break;
		}
	}
	InOrder(root);
	return 0;
}
```

































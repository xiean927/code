
* 我的中序遍历，不好使！不知什么原因
```
#include <bits/stdc++.h>

using namespace std;

struct Node{
    char ch[15];
    int lf,rt;
}nd[22];
int n;
bool isRoot[22];

void InOrder(int index){
    if(index==-1)
        return ;
    InOrder(nd[index].lf);
    cout<<nd[index].ch<<" ";
    InOrder(nd[index].rt);
}

int main(){

    scanf("%d",&n);
    //getchar();
    memset(isRoot,false,sizeof(isRoot));
    for(int i=0;i<n;i++){
        getchar();
        scanf("%s %d %d",nd[i].ch,&nd[i].lf,&nd[i].rt);
        if(nd[i].lf!=-1)
            isRoot[nd[i].lf]=true;
        if(nd[i].rt!=-1)
            isRoot[nd[i].rt]=true;
    }
    int root;
    for(int i=1;i<=n;i++)
        if(!isRoot[i]){
            root=i;
            break;
        }
    printf("%d\n",root);
    InOrder(root);

//    for(int i=0;i<n;i++){
//        printf("%s %d %d\n",nd[i].ch,nd[i].lf,nd[i].rt);
//    }


    return 0;
}

```



* [思路，转自CSDN](https://blog.csdn.net/galesaur_wcy/article/details/82354161)
  * 中序遍历除了根节点和叶节点之外，要加括号
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












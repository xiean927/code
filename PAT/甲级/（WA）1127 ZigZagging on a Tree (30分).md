

* [建树写法](https://blog.csdn.net/galesaur_wcy/article/details/84026940)

```
#include <bits/stdc++.h>

using namespace std;

const int maxn=35;

struct node{
	int data;
	node* lchild;
	node* rchild;
	node(int val){
        data=val;
        lchild=rchild=NULL;
	}
};

int in[maxn],post[maxn];
int tree[maxn][2];
vector<int> res[maxn];
int n,root;

///先序和中序，那叫构建树,而非求出后序
node* create(int inL,int inR,int postL,int postR){
	if (postL>postR)
		return NULL;
	//node* root = new node;
	//root->data = pre[preL];
	//node* root=new node(pre[preL]);
	node* root=new node(post[postR]);
	int k;
	for (k=inL;k<inR;k++){
		if(in[k]==root->data)
			break;
	}
	int numLeft=k-inL;
	root->lchild=create(inL,k-1,postL,postL+numLeft-1);
	root->rchild=create(k+1,inR,postL+numLeft,postR-1);
	return root;
}

void inorder(node *root){
    if(root==NULL)
        return ;
    inorder(root->lchild);
    printf("%d-",root->data);
    inorder(root->rchild);
}

int main(){
    scanf("%d",&n);
    for(int i=1;i<=n;i++)
        scanf("%d",&in[i]);
    for(int i=1;i<=n;i++)
        scanf("%d",&post[i]);
    node *root=NULL;
    root=create(1,n,1,n);
    //inorder(root);

    return 0;
}


```


* [按照层号排序](https://blog.csdn.net/xmj15715216140/article/details/82263663)






```
L旋，R旋，LL，LR，RR，RL

示意图:


LL型 
       1
   	 2        3
  4     5    
6   7
  
  对根1右旋
       2
    4    1
   6  7  5  3
   

LR型
       1
	 2    3
  4    5
      6  7
  对2左旋
      1
	5    3
   2  7 
  4 6
   对根1右旋
     5
   2   1
  4 6 7 3
  
RR型
     1
   2    3
       4  5
	      6  7
		  
对根1左旋
    3
  1   5
 2 4  6 7
 
 RL型
    1
  2    3
     4   5
	6  7

对结点3右旋
   1
  2  4
    6  3
	  7  5
对根1左旋

    4
  1    3
 2  6  7  5
  
  



#include <bits/stdc++.h>

using namespace std;

struct node{
    int data,height;
    node *lchild,*rchild;
};

node* newNode(int v){
    node* Node=new node;
    Node->data=v;
    Node->height=1;
    Node->lchild=Node->rchild=NULL;
    return Node;
}

///获取以root为根结点的子树的当前height
int getHeight(node* root){
    if(root==NULL)  return 0;
    return root->height;
}

///计算结点root的平衡因此
int getBalanceFactor(node* root){
    ///左子树高度 减 右子树高度
    return getHeight(root->lchild)-getHeight(root->rchild);
}

///更新结点root的height
void updateHeight(node* root){
    ///max(左孩子的height,右孩子的height)+1
    root->height=max(getHeight(root->lchild),getHeight(root->rchild))+1;
}

///search函数查找AVL树中数据域为x的结点
void search_(node* root,int x){
    if(root==NULL){
      //  printf("search failed\n");
        return ;
    }
    if(x==root->data)
        printf("%d\n",root->data);
    else if(x<root->data)
        search_(root->lchild,x);
    else
        search_(root->rchild,x);
}


///左旋
void L(node* &root){
    node* tmp=root->rchild;
    root->rchild=tmp->lchild;
    tmp->lchild=root;
    updateHeight(root);
    updateHeight(tmp);
    root=tmp;
}

///右旋
void R(node* &root){
    node* tmp=root->lchild;
    root->lchild=tmp->rchild;
    tmp->rchild=root;
    updateHeight(root);
    updateHeight(tmp);
    root=tmp;
}

///插入权值为v的结点
void insert_(node* &root,int v){
    if(root==NULL){
        root=newNode(v);
        return ;
    }
    if(v<root->data){///v比根节点的权值小
        insert_(root->lchild,v);        ///往左子树插入
        updateHeight(root);             ///更新树高
        if(getBalanceFactor(root)==2){
            if(getBalanceFactor(root->lchild)==1){///LL型
                R(root);
            }
            else if(getBalanceFactor(root->lchild)==-1){///LR型
                L(root->lchild);
                R(root);
            }
        }
    }
    else{   ///v比根结点的权值大
        insert_(root->rchild,v);      ///往右子树插入
        updateHeight(root);         ///更新树高
        if(getBalanceFactor(root)==-2){
            if(getBalanceFactor(root->rchild)==-1){///RR型
                L(root);
            }else if(getBalanceFactor(root->rchild)==1){///RL型
                R(root->rchild);
                L(root);
            }
        }
    }

}

///AVL树的建立
node* Create(int data[],int n){
    node* root=NULL;
    for(int i=0;i<n;i++){
        insert_(root,data[i]);
    }
    return root;
}

int isComplete=1,after=0;
vector<int> levelOrder(node *tree){
    vector<int> v;
    queue<node *> q;
    q.push(tree);

    while(!q.empty()){
        node *tmp=q.front();
        q.pop();

        v.push_back(tmp->data);
        if(tmp->lchild!=NULL){///判断是否是完全AVL树
            if(after)   isComplete=0;
            q.push(tmp->lchild);
        }
        else{
            after=1;
        }

        if(tmp->rchild!=NULL){
            if(after)   isComplete=0;
            q.push(tmp->rchild);
        }
        else{
            after=1;
        }
    }

    return v;
}


int main()
{
    int n,tmp;

    scanf("%d",&n);
    node* tree=NULL;
    for(int i=0;i<n;i++){
        scanf("%d",&tmp);
        insert_(tree,tmp);
    }

    vector<int> v=levelOrder(tree);

    for(int i=0;i<(int)v.size();i++){
        if(i)
            printf(" ");
        printf("%d",v[i]);
    }

    printf("\n%s",isComplete?"YES":"NO");


    return 0;
}

```

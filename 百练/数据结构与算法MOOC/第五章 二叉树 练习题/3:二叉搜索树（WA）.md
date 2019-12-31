

```
#include <bits/stdc++.h>

using namespace std;


struct Node{
    Node *left,*right;
    int data;
};

Node* newNode(int val){
    Node* node=new Node;
    node->data=val;
    node->left=NULL;
    node->right=NULL;
    return node;
}

void insert_(Node* &root,int x){
    if(root==NULL){
        root=newNode(x);
        return ;
    }
    if(x==root->data)
        return ;
    else if(x<root->data)
        insert_(root->left,x);
    else
        insert_(root->right,x);
}

void preorder(Node* root){
    if(root==NULL)
        return ;
    printf("%d ",root->data);
    preorder(root->left);
    preorder(root->right);
}

int main(){
    int val;
    Node* root=NULL;
    while(scanf("%d",&val)){
        insert_(root,val);
    }
    preorder(root);
    return 0;
}


```

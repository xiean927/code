* [1,参考BFS解法](https://blog.csdn.net/acm_zh/article/details/88036318)
  * ```变量f1 f2```判断一个节点的左右子树是否存在
```
#include<iostream>
#include<string>
#include<vector> 
#include<cstdio>
#include<queue>
using namespace std;
struct node{
	int lchild,rchild;
};
struct node a[25];
int f1=0,f2=0;
int cnt;
void level(int root){
	queue<int> q;
	q.push(root);
	while(!q.empty()){
		cnt = q.front();
		q.pop();
		if(a[cnt].lchild!=-1){
			if(f1==1) f2 = 1;///如果右子树不存在，而左子树存在，f2置为1
			q.push(a[cnt].lchild);
		}else{///如果左子树不存在
			f1 = 1;
		}
		if(a[cnt].rchild!=-1){
			if(f1==1) f2 =1;///如果左子树不存在，而右子树存在，f2置为1
			q.push(a[cnt].rchild);
		}else{
			f1 = 1;///如果右子树不存在
		}
		
	}
}
int main(){
	int n;
	vector<int> book(25,0);
	cin >> n;
	for(int i = 0;i < n;i++){
		string l,r;
		cin >> l >> r;
		if(l=="-"){
			a[i].lchild = -1;
		}else{
			a[i].lchild = stoi(l);
			book[stoi(l)] = 1;
		}
		if(r=="-"){
			a[i].rchild = -1;
		}else{
			a[i].rchild = stoi(r);
			book[stoi(r)] = 1;
		}
	} 
	int root=0;
	while(book[root] != 0){
		root++;
	}
	level(root);
	if(f2==0){
		cout << "YES" << " " << cnt << endl; 
	}else{
		cout << "NO" << " " << root << endl;
	}
}
```

* [根据完全二叉树的特点判断](https://blog.csdn.net/S_999999/article/details/98611310)
  * 分析：递归出最大的下标值，完全二叉树一定把前面的下标充满： 最大的下标值 == 最大的节点数；不完全二叉树前满一定有位置是空，会往后挤： 最大的下标值 > 最大的节点数～
```
#include <bits/stdc++.h>

using namespace std;

/*
判断是否是完全二叉树

*/

int tree[25][2];
int n;
bool isroot[25];
int maxindex,last;///maxindex记录最大下标，last记录最后的结点序号

void judge(int root,int index){
    if(root==-1)
        return ;
    if(index>maxindex){
        maxindex=index;
        last=root;
    }
    judge(tree[root][0],2*index);
    judge(tree[root][1],2*index+1);
}

int main(){
    char lf[5],rt[5];
    //int ilf,irt;
    scanf("%d",&n);
    memset(isroot,false,sizeof(isroot));
    for(int i=0;i<n;i++){
        scanf("%s%s",lf,rt);
        //cout<<lf<<" "<<rt<<endl;
        if(lf[0]=='-')
            tree[i][0]=-1;
        else{
            tree[i][0]=atoi(lf);
            isroot[tree[i][0]]=true;
        }
        if(rt[0]=='-')
            tree[i][1]=-1;
        else{
            tree[i][1]=atoi(rt);
            isroot[tree[i][1]]=true;
        }
        //cout<<tree[i][0]<<" "<<tree[i][1]<<endl;
    }
    int root;
    for(int i=0;i<n;i++){
        if(isroot[i]==false){
            root=i;
            break;
        }
    }

    judge(root,1);
    if(maxindex==n)
        printf("YES %d\n",last);
    else
        printf("NO %d\n",root);

    return 0;
}
```
  

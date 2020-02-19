* 利用树的两条性质判断：
  * 1. 树的节点数比边数多1（空树除外）
  * 2. 树中除根节点的每个节点只有唯一的父节点
  * 条件1可以排除有环的图，条件2可以排除多个根的图。
  * 特别注意的是，空树不满足条件1，需单独判断！
* 空树也是树
* [题解思路](https://blog.csdn.net/da_kao_la/article/details/80721158)

* 0分思路代码
```
#include <bits/stdc++.h>

using namespace std;

const int maxn=510;
///叶节点编号从1开始
int father[maxn],nodenum,edgenum,Case=1;
bool is_tree;
set<int> tree_nodes;

void process(){
    //printf("%d %d %d\n",is_tree,tree_nodes.size(),edgenum);
    if(is_tree&&(((int)tree_nodes.size()==0&&edgenum==0)||((int)tree_nodes.size()==edgenum+1)))
        printf("Case %d is a tree.\n",Case);
    else
        printf("Case %d is not a tree.\n",Case);
}

int main(){
    int a,b;
    nodenum=0,edgenum=0;
    is_tree=true;
    tree_nodes.clear();
    memset(father,0,sizeof(father));
    while(scanf("%d%d",&a,&b)!=EOF){
        if(a==-1&&b==-1)
            break;
        if(a==0&&b==0){
            process();
            Case++;
            nodenum=0,edgenum=0;
            is_tree=true;
            tree_nodes.clear();
            memset(father,0,sizeof(father));
        }
        //else{///注意顺序，如果这样写,is_tree始终为false
        //    tree_nodes.insert(a);
        //    tree_nodes.insert(b);
        //    edgenum++;
        //    father[b]=a;
        //}
        if(father[b]){///如果子节点b已经有父节点a了，则说明这不是一棵树
            //printf("%d %d\n",a,b);
            is_tree=false;
        }
        else{
            tree_nodes.insert(a);
            tree_nodes.insert(b);
            edgenum++;
            father[b]=a;
        }
    }
    return 0;
}

```

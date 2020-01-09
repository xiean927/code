### 思路来源:
* [1](https://blog.csdn.net/weixin_40116174/article/details/86760248)
* [2](https://blog.csdn.net/weixin_40446193/article/details/89716161)

### 思路：
* 种类并查集的关键在于与结点与根结点的距离， 如果距离是奇数那么性别就和跟结点相反，如果是偶数就和跟结点性别相同。
```
假设有

1，2

2，3

即1--2--3， 明显相邻的两个不能是同性别的，如果相邻两个是同性的，那么说明就可能是有同性恋存在。

上面假设1是男性，用false来代替，那么按顺序分别是false, true, false

假设  再加个关系3， 1

那么由于1和3已经都有值了，都是false，说明可能有同性恋。

```
* 我自己的路径压缩并不能用，因为是先找到根，然后从后向根调整，
* 这个抄的是，从根向```x```结点来更新距离关系


```
#include <bits/stdc++.h>

using namespace std;

///题目最大的问题就是得先假设性别
int father[2010];///定义父节点
int rank1[2010];///定义性别
bool flag;

/*
从x=>根
路径压缩
int find_father(int x){
    int a=x;
    while(x!=father[x])
        x=father[x];

    while(a!=father[a]){
        int z=a;
        a=father[a];
        rank1[z]=(rank1[z]+rank1[a])%2;///更新与父节点的关系
        father[z]=x;
    }
    return x;
}
*/

///从根=>x路径压缩
int find_father(int x)
{
    if (x == father[x]) return x;
    int temp = father[x];
    //为路径压缩!!!
    father[x] = find_father(father[x]);//当该节点的下标与父节点不等的时候，将父节点的值付给x继续查找直到找到根节点
    rank1[x] = (rank1[x] + rank1[temp]) % 2;//更新x与父节点之间的关系,0,1表示不同性别%2判断性别
    return father[x];
}

bool Union(int x,int y){
    int f_x=find_father(x);
    int f_y=find_father(y);
    if(f_x!=f_y){
        father[f_x]=f_y;
        //rank1[f_x]=(rank1[x]+rank1[y]+1)%2;
        rank1[f_x]=(rank1[x]==rank1[y]);
        return flag;
    }
    else{//根节点相同，且距离（性别）相同 
        if(rank1[x]==rank1[y]){///如果x,y同根，且到根的距离相同，x,y又存在合并，说明存在同性恋
            flag=false;
            return false;
        }
    }
}

int main(){
    int t,k=1;
    scanf("%d",&t);
    while(t--){
        int cnum,jnum;
        flag=true;
        scanf("%d%d",&cnum,&jnum);
        for(int i=1;i<=cnum;i++){
            father[i]=i;
            rank1[i]=0;
        }
        int x,y;
        for(int i=0;i<jnum;i++){
            scanf("%d%d",&x,&y);
            Union(x,y);
        }

        printf("Scenario #%d:\n",k);
        if(flag==false)
            printf("Suspicious bugs found!\n");
        else
            printf("No suspicious bugs found!\n");
        k++;
        printf("\n");
    }

    return 0;
}




```


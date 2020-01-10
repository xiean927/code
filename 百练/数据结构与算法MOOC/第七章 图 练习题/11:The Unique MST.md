
### 描述
* 给出一个无向连通图，判断它的最小生成树是否唯一

### 思路
* 从最小生成树中之外选择一条边，构建次小生成树
* ```vis数组```
* [次小生成树证明（没看懂）](https://zhuanlan.zhihu.com/p/24950356?utm_source=com.tencent.tim&utm_medium=social)

```
#include <bits/stdc++.h>

using namespace std;

typedef long long LL;
const int maxn = 110;
const int inf = 0x3f3f3f3f;
int n,m;

struct edge
{
    int u,v,w;
    bool operator < (const edge &a)const
    {
        return w < a.w;
    }
} edge[maxn*maxn];

int father[maxn*2];
bool vis[maxn*maxn];

int findfather(int x){
    int a=x;
    while(x!=father[x])
        x=father[x];

    while(a!=father[a]){
        int z=a;
        a=father[a];
        father[z]=x;
    }

    return x;
}

void kruskal_pro(){
    int ans=0,num_edge=0;
    for(int i=1;i<=n;i++)
        father[i]=i;
    for(int i = 0; i < m; ++i)
        vis[i] = false;
    for(int i=0;i<m;i++){
        int faU=findfather(edge[i].u);
        int faV=findfather(edge[i].v);
        if(faU!=faV){
            father[faU]=faV;
            ans+=edge[i].w;
            num_edge++;
            vis[i]=true;
            if(num_edge==n-1)
                break;
        }
    }
    //寻找次小生成树
    int min2 = inf;
    //枚举不是在最小生成树中的边
    for(int i = 0; i < m; i++){
        if(vis[i])  continue;
        //首先把当前边加入最小生成树中
        int sum = 0;
        for(int i=1;i<=n;i++)
            father[i]=i;
        father[edge[i].v]=edge[i].u;
        sum+=edge[i].w;
        num_edge=1;
        for(int j=0;j<m;j++){
            int faU=findfather(edge[j].u);
            int faV=findfather(edge[j].v);
            if(faU!=faV){
                father[faV]=faU;
                sum+=edge[j].w;
                num_edge++;
                if(num_edge==n-1){
                    min2=min(min2,sum);
                    break;
                }
            }
        }
    }

    if(min2 == ans)puts("Not Unique!");
    else printf("%d\n",ans);
}

int main()
{
    int t;
    scanf("%d",&t);
    while(t--)
    {
        scanf("%d%d",&n,&m);
        for(int i = 0; i < m; ++i)
        {
            scanf("%d%d%d",&edge[i].u,&edge[i].v,&edge[i].w);
        }
        kruskal_pro();
    }
    return 0;
}

```


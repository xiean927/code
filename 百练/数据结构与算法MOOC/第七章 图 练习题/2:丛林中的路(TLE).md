### 最小生成树

```
#include <bits/stdc++.h>

using namespace std;

typedef long long LL;
const int maxn = 106;
const int inf = 0x3f3f3f3f;
int n,m;

struct Edge{
    int u,v,w;
} edge[106];

bool cmp(const Edge &a,const Edge &b){
    return a.w<b.w;
}

int father[106];

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

void kruskal(){
    int ans=0,num_edge=0;
    for(int i=0;i<maxn;i++)
        father[i]=i;
    sort(edge,edge+m,cmp);
    for(int i=0;i<m;i++){
        int faU=findfather(edge[i].u);
        int faV=findfather(edge[i].v);
        if(faU!=faV){
            father[faU]=faV;
            ans+=edge[i].w;
            num_edge++;
            //vis[i]=true;
            if(num_edge==n-1)
                break;
        }
    }
    if(num_edge != n-1){
        cout<<"-1"<<endl; // 图不连通
    }
    else{
        cout<<ans<<endl; // 返回最小生成树的边权和
    }
}

int main()
{
    while(scanf("%d",&n),n!=0){
        char number,tmpn;
        int digit,tmpd;
        m=0;
        getchar();
        for(int i=1;i<=n-1;i++){
            scanf("%c%d",&number,&digit);
            //cout<<number<<" "<<digit<<endl;
            for(int i = 0; i < digit; ++i){
                scanf(" %c%d",&tmpn,&tmpd);
                //cout<<tmpn<<" "<<tmpd<<endl;
                edge[m].u=number-'A'+1;
                edge[m].v=tmpn-'A'+1;
                edge[m++].w=tmpd;
            }
            getchar();
        }

        //cout<<endl;
        //for(int i=0;i<m;i++)
            //cout<<edge[i].u<<" "<<edge[i].v<<" "<<edge[i].w<<endl;
        kruskal();
    }
    return 0;
}

```

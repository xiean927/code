

### [思路，转自CSDN](https://blog.csdn.net/u013480600/article/details/30513421)：
* 构造图，拓扑排序判断是否可行

```
#include<cstdio>
#include<cstring>
#include<vector>
#include<queue>
using namespace std;
const int maxn=10;
vector<int> value[maxn][maxn];
int dr[]={0,1,0,1};//原地,下,右,右下
int dc[]={0,0,1,1};
int G[maxn][maxn]; //图
int in[maxn];      //入度
 
bool topo()
{
    queue<int> Q;
    for(int i=0;i<9;i++)
        if(in[i]==0) Q.push(i);
    int sum=0;//记录我们删除的0入度点
    while(!Q.empty())
    {
        int u=Q.front(); Q.pop();
        for(int v=0;v<9;v++)if(G[u][v])
        {
            G[u][v]=0;
            if(--in[v]==0) Q.push(v);
        }
        sum++;
    }
    return sum==9;
}

int main()
{
    for(int i=0;i<9;i++)                ///处理0-8每个应用所在的方格vector
    {
        int r=i/3, c=i%3;               ///i应用左上角的格子所在的(r,c)
        for(int dir=0;dir<4;dir++)      ///i应用所在的其他3个点
        {
            int nr=r+dr[dir], nc=c+dc[dir];
            value[nr][nc].push_back(i); ///将i压入对应方格的vector中
        }
    }
 
    char str[100];
    while(scanf("%s",str)==1&&str[0]!='E')
    {
        memset(G,0,sizeof(G));
        memset(in,0,sizeof(in));
        for(int i=0;i<4;i++)
        for(int j=0;j<4;j++)
        {
            int v;
            scanf("%d",&v);
            v--;
            for(int k=0;k<value[i][j].size();k++)
            if((value[i][j])[k]!=v)///构造有向边
            {
                int x=(value[i][j])[k];
                if(G[x][v]==0)///一定要做这个判断,因为会重复添加有向边
                {
                    in[v]++;
                    G[x][v]=1;
                }
                ///printf("当前格子为:(%d,%d),当前边为:%d v=%d, %d点的入度为%d\n",i,j,x,v,v,in[v]);
            }
        }
        if(topo()) printf("THESE WINDOWS ARE CLEAN\n");
        else printf("THESE WINDOWS ARE BROKEN\n");
        scanf("%s",str);
    }
 
    return 0;
}
```

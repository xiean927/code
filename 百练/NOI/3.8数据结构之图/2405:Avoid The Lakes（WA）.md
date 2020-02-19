

* 3分代码
  * 我的代码和正解代码，没有区别，我用vis数组记录是否访问过
```
#include<bits/stdc++.h>

using namespace std;

const int maxn=110;

int dx[]={1,-1,0,0};
int dy[]={0,0,1,-1};
int e[maxn][maxn];
bool vis[maxn][maxn];
int n,m,k,ans;


void dfs(int ix,int iy,int cnt){
    vis[ix][iy]=true;
    ans=max(ans,cnt);
    //printf("%d %d %d\n",ix,iy,cnt);
    for(int i=0;i<4;i++){
        int x=ix+dx[i];
        int y=iy+dy[i];
        if(!e[x][y]||vis[x][y]||x>n||x<=0||y>m||y<=0)
            continue;
        dfs(x,y,cnt+1);
    }
}

int main(){
    memset(vis,false,sizeof(vis));
    memset(e,0,sizeof(e));
    scanf("%d%d%d",&n,&m,&k);
    int a,b;

    for(int i=0;i<k;i++){
        scanf("%d%d",&a,&b);
        e[a][b]=1;
    }
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
            if(vis[i][j]==false&&e[a][b])
                dfs(i,j,1);
        }
    }

    printf("%d\n",ans);
    return 0;
}
```





* 一开始忘记回溯了，直接跑不了
* [我的解法和这个差不多](https://blog.csdn.net/qq_42995099/article/details/82193192)
```
#include <bits/stdc++.h>

using namespace std;

bool vis[12][12];
int n,m,x,y;

int mov[4][2]={{-2,1},{2,1},{2,-1},{-2,-1}};
int cnt;

bool isuse(){
    for(int i=0;i<n;i++)
        for(int j=0;j<m;j++)
            if(!vis[i][j])  return false;
    return true;
}

void dfs(int x,int y){
    if(isuse()){
        cnt++;
        return ;
    }
    for(int i=0;i<4;i++){
        int dx=x+mov[i][0];
        int dy=y+mov[i][1];
        if(vis[dx][dy]==true||(dx<0||dx>=n||dy<0||dy>=m))
            continue;
        vis[dx][dy]=true;
        dfs(dx,dy);
        vis[dx][dy]=false;
    }
}

int main(){
    int T;
    scanf("%d",&T);
    while(T--){
        cnt=0;
        memset(vis,0,sizeof(vis));
        scanf("%d%d%d%d",&n,&m,&x,&y);
        vis[x][y]=true;
        dfs(x,y);
        printf("%d\n",cnt);

    }
    return 0;
}



```


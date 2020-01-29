### 描述
* Each square contains either water ('W') or dry land ('.'). 
* Farmer John would like to figure out how many ponds have formed in his field. 
* A pond is a connected set of squares with water in them, where a square is considered adjacent to all eight of its neighbors.

* 相邻是指八个方向相邻


### 思路
* ```dfs```

```
#include <bits/stdc++.h>

using namespace std;

char mp[110][110];
int n,m;
int dx[8]={-1,0,1,1,1,0,-1,-1};
int dy[8]={1,1,1,0,-1,-1,-1,0};
bool vis[110][110];

void dfs(int x,int y){
    vis[x][y]=true;
    for(int i=0;i<8;i++){
        int dix=x+dx[i];
        int diy=y+dy[i];
        if(vis[dix][diy]||dix>=n||dix<0||diy>=m||diy<0||mp[dix][diy]=='.')
            continue;
        dfs(dix,diy);
    }
}

int main(){
    scanf("%d%d",&n,&m);
    for(int i=0;i<n;i++){
        getchar();
        for(int j=0;j<m;j++){
            scanf("%c",&mp[i][j]);
        }
    }
    /*
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            printf("%c",mp[i][j]);
        }
        printf("\n");
    }
    */
    memset(vis,false,sizeof(vis));
    int cnt=0;

    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            if(!vis[i][j]&&mp[i][j]=='W'){
                dfs(i,j);
                cnt++;
            }
        }
    }

    printf("%d\n",cnt);
    return 0;
}
```

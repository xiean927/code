
* 我写成了```DFS```，所以写错了
```
#include <bits/stdc++.h>

using namespace std;
int M,N;
int mp[210][210];
int comx,comy;///司令部位置
int P;///放水点总数
int fangs[210][210];///放水点位置
bool flag;///是否被淹
int mov[4][2]={{0,1},{1,0},{0,-1},{-1,0}};
bool vis[210][210];

void dfs(int x,int y){
    vis[x][y]=true;
    if(x==comx&&y==comy){
        flag=true;
        return ;
    }
    for(int i=0;i<4;i++){
        int dx=x+mov[i][0];
        int dy=y+mov[i][1];
        if(vis[dx][dy]==true||dx<1||dx>M||dy<1||dy>N||mp[dx][dy]>mp[x][y])
            continue;
        dfs(dx,dy);
    }
}

int main(){
    int K;
    scanf("%d",&K);
    while(K--){
        memset(mp,0,sizeof(mp));
        memset(vis,0,sizeof(vis));
        memset(fangs,0,sizeof(fangs));
        scanf("%d%d",&M,&N);
        for(int i=1;i<=M;i++)
        for(int j=1;j<=N;j++)
            scanf("%d",&mp[i][j]);
        scanf("%d%d",&comx,&comy);
        scanf("%d",&P);
        flag=false;
        for(int i=0;i<P;i++){
            int a,b;
            scanf("%d%d",&a,&b);
            //fangs[a][b]=1;
            dfs(a,b);
        }
        cout<<flag<<endl;
    }
}


```


* ```BFS```
```
#include <bits/stdc++.h>

using namespace std;
int M,N;
int mp[210][210];
int comx,comy;///司令部位置
int P;///放水点总数
bool flag;///是否被淹
int mov[4][2]={{0,1},{1,0},{0,-1},{-1,0}};
bool vis[210][210];

struct Node{
    int x,y;
}now,next_;

int bfs(int x,int y){
    queue<Node> q;
    now.x=x;
    now.y=y;
    vis[x][y]=true;
    q.push(now);
    while(!q.empty()){
        now=q.front();
        q.pop();
        for(int i=0;i<4;i++){
            next_.x=now.x+mov[i][0];
            next_.y=now.y+mov[i][1];
            if(vis[next_.x][next_.y]==true||next_.x<1||next_.x>M||next_.y<1||next_.y>N||mp[next_.x][next_.y]<mp[now.x][now.y])
                continue;
            if(next_.x==comx&&next_.y==comy)
                return 1;
            vis[next_.x][next_.y]=true;
            q.push(next_);
        }
    }
    return 0;
}

int main(){
    int K;
    scanf("%d",&K);
    while(K--){
        flag=false;
        memset(mp,0,sizeof(mp));
        scanf("%d%d",&M,&N);
        for(int i=1;i<=M;i++)
        for(int j=1;j<=N;j++)
            scanf("%d",&mp[i][j]);
        scanf("%d%d",&comx,&comy);
        scanf("%d",&P);
        for(int i=0;i<P;i++){
            int a,b;
            memset(vis,false,sizeof(vis));
            scanf("%d%d",&a,&b);
            //fangs[a][b]=1;
            if(bfs(a,b)){
                flag=true;
                break;
            }
        }
        if(flag)
            printf("Yes\n");
        else
            printf("No\n");
    }
}
```
















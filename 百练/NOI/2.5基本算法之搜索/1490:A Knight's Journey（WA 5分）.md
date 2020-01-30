### 思路
* 一开始写成```bfs```了，```bfs```无法一条路遍历整个图，
* 得写```dfs```

```
#include <bits/stdc++.h>

using namespace std;

int dx[8]={-2,-1,1,2,2,1,-1,-2};
int dy[8]={1,2,2,1,-1,-2,-2,-1};
int p,q;
//pair<int,int> mp[30][30];
struct Node{
    int x,y;
}st,ed,mp[900];
bool vis[30][30],success;


bool judge(){
    for(int i=1;i<=p;i++)
    for(int j=1;j<=q;j++)
        if(!vis[i][j])
            return false;
    return true;
}
/*
void bfs(){
    queue<Node> que;
    vis[st.x][st.y]=true;
    que.push(st);
    while(!que.empty()){
        Node nd=que.front(),tmp;
        que.pop();
        if(judge()){
            ed.x=nd.x;ed.y=nd.y;
            mp[ed.x][ed.y].x=nd.x;mp[ed.x][ed.y].y=nd.y;
            mp[ed.x][ed.y].prex=nd.prex;mp[ed.x][ed.y].prey=nd.prey;
            break;
        }

        for(int i=0;i<8;i++){
            int dix=nd.x+dx[i];
            int diy=nd.y+dy[i];
            if(vis[dix][diy]||dix>p||dix<1||diy>q||diy<1)
                continue;
            vis[dix][diy]=true;
            cout<<dix<<" "<<diy<<endl;
            //tmp.x=dix;tmp.y=diy;
            mp[dix][diy].x=dix;
            mp[dix][diy].y=diy;
            mp[dix][diy].prex=nd.x;
            mp[dix][diy].prey=nd.y;
            tmp.x=dix;tmp.y=diy;
            tmp.prex=nd.x;tmp.prey=nd.y;
            que.push(tmp);
        }
    }
}
*/
void dfs(Node nd,int num){
    vis[nd.x][nd.y]=true;
    mp[num].x=nd.x;mp[num].y=nd.y;
    Node tmpd;
    if(judge()){///如果都走完了
        success=true;
        return ;
    }

    for(int i=0;i<8;i++){
        int dix=nd.x+dx[i];
        int diy=nd.y+dy[i];
        if(!success&&!vis[dix][diy]&&dix<=p&&dix>=1&&diy<=q&&diy>=1){
             vis[dix][diy]=true;
             tmpd.x=dix;tmpd.y=diy;
             dfs(tmpd,num+1);
             vis[dix][diy]=false;
        }
    }
}

int main(){
    int T;
    scanf("%d",&T);
    for(int t=1;t<=T;t++){
        scanf("%d%d",&p,&q);
        st.x=1;st.y=1;
        memset(vis,false,sizeof(vis));
        //ed.x=-1,ed.y=-1;
        //bfs();
        //if(ed.x==-1&&ed.y==-1){
         //   printf("impossible\n");
            //continue;
        //}
        //else{
            //dfs(ed);
        //    printf("\n");
        //}
        success=false;
        dfs(st,1);
        printf("Scenario #%d:\n", t);
        if(success){
            for(int i=1;i<=p*q;i++)
                printf("%c%c",mp[i].y+'A'-1,mp[i].x+'0');
            printf("\n");
        }
        else
            printf("impossible\n");
        if(t!=T)
             printf("\n");      //注意该题的换行
    }
    return 0;
}

```

### 思路
* ```三维BFS```

```
#include <bits/stdc++.h>

using namespace std;

struct Node{
    int x,y,z,step;
}st,ed,tmp;
char mp[35][35][35];///L,R,C
int L,R,C;
bool vis[35][35][35];
int dx[6]={0,0,0,0,1,-1};
int dy[6]={1,-1,0,0,0,0};
int dz[6]={0,0,1,-1,0,0};

void bfs(){
    queue<Node> q;
    q.push(st);
    vis[st.z][st.x][st.y]=true;
    while(!q.empty()){
        Node nd=q.front();
        q.pop();

        if(nd.x==ed.x&&nd.y==ed.y&&nd.z==ed.z){
            ed.step=nd.step;
            break;
        }
        for(int i=0;i<6;i++){
            int dix=nd.x+dx[i];
            int diy=nd.y+dy[i];
            int diz=nd.z+dz[i];
            if(dix>=R||dix<0||diy>=C||diy<0||diz>=L||diz<0||vis[dix][diy][diz]||mp[diz][dix][diy]=='#')
                continue;
            vis[diz][dix][diy]=true;
            //cout<<dix<<" "<<diy<<" "<<diz<<endl;
            tmp.x=dix;
            tmp.y=diy;
            tmp.z=diz;
            tmp.step=nd.step+1;
            q.push(tmp);
        }

    }
}

int main(){

    while(scanf("%d%d%d",&L,&R,&C)!=EOF){
        if(L==0&&R==0&&C==0)    break;
        for(int k=0;k<L;k++){
            for(int i=0;i<R;i++){
                getchar();
                for(int j=0;j<C;j++){
                    scanf("%c",&mp[k][i][j]);
                    if(mp[k][i][j]=='S'){
                        st.x=i;
                        st.y=j;
                        st.z=k;
                        st.step=0;
                    }
                    if(mp[k][i][j]=='E'){
                        ed.x=i;
                        ed.y=j;
                        ed.z=k;
                        ed.step=-1;
                    }
                }
            }
            getchar();
        }
        memset(vis,false,sizeof(vis));
        bfs();
        if(ed.step==-1)
            printf("Trapped!\n");
        else
            printf("Escaped in %d minute(s).\n",ed.step);

    }
    return 0;
}


/*
    for(int k=0;k<L;k++){
        for(int i=0;i<R;i++){
            //getchar();
            for(int j=0;j<C;j++){
                printf("%c",mp[k][i][j]);
            }
            printf("\n");
        }
        printf("\n");
    }
*/
```

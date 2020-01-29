### 输入
*  'Y' (you), 'T' (target), 'S' (steel wall), 'B' (brick wall), 'R' (river) and 'E' (empty space). Both 'Y' and 'T' appear only once. 
* Your tank can't move through rivers or walls, but it can destroy brick walls by shooting. A brick wall will be turned into empty spaces when you hit it, however, if your shot hit a steel wall, there will be no damage to the wall.
* you can choose to move to a neighboring (4 directions, not 8) empty space, or shoot in one of the four directions without a move. The shot will go ahead in that direction, until it go out of the map or hit a wall. If the shot hits a brick wall, the wall will disappear (i.e., in this turn).
* Well, given the description of a map, the positions of your tank and the target, how many turns will you take at least to arrive there?


### 思路：
![](https://github.com/xiean927/code/blob/master/Image/F%20Battle%20City.png)
* 这个题得拿优先队列写，用普通队列会```WA```
* 要实时更新结点```ed```的```step```，否则，输出的话，只会输出```-1```
```
if(nd.x==ed.x&&nd.y==ed.y){
    ed.step=nd.step;
    break;
}
```

```
#include <bits/stdc++.h>

using namespace std;

struct Node{
    int x,y,step;
}st,ed;

int dix[4]={1,-1,0,0};///四个方向
int diy[4]={0,0,1,-1};
char mp[310][310];
int m,n;///m:行;n:列
bool vis[310][310];

//优先队列的排列方式
bool operator < (Node a, Node b)
{
    return a.step > b.step;
}

void bfs(){
    priority_queue<Node> q;
    q.push(st);
    vis[st.x][st.y]=true;
    while(!q.empty()){
        Node nd=q.top(),tmp;
        q.pop();
        if(nd.x==ed.x&&nd.y==ed.y){
            ed.step=nd.step;
            break;
        }


        for(int i=0;i<4;i++){
            int dx=nd.x+dix[i];
            int dy=nd.y+diy[i];
            if(dx<0||dx>=m||dy<0||dy>=n||mp[dx][dy]=='S'||mp[dx][dy]=='R'||vis[dx][dy])
                continue;
            tmp.x=dx;
            tmp.y=dy;
            vis[dx][dy]=true;
            if(mp[dx][dy]=='B')
                tmp.step=nd.step+1+1;
            else
                tmp.step=nd.step+1;
            //cout<<dx<<" "<<dy<<" "<<tmp.step<<endl;
            q.push(tmp);
        }
    }
}

int main(){
    int i,j;
    while(scanf("%d%d",&m,&n)!=EOF){
        if(m==0&&n==0)  break;
        for(i=0;i<m;i++){
            getchar();
            for(j=0;j<n;j++)
                scanf("%c",&mp[i][j]);
        }

        for(i=0;i<m;i++){
        for(j=0;j<n;j++){
            //cout<<mp[i][j];
            if(mp[i][j]=='Y'){
                st.x=i;
                st.y=j;
                st.step=0;
            }
            if(mp[i][j]=='T'){
                ed.x=i;
                ed.y=j;
                ed.step=-1;
            }
        }
        //cout<<endl;
        }
        //cout<<st.x<<" "<<st.y<<" "<<ed.x<<" "<<ed.y<<endl;
        memset(vis,false,sizeof(vis));
        bfs();
        //for(int )
        cout<<ed.step<<endl;
    }

    return 0;
}


```

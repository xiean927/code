### 不知图是不是无向图
```
#include <bits/stdc++.h>

using namespace std;

const int maxn=100010;

vector<int> e[maxn],res;
int n,m,inDegree[maxn];
queue<int> q;
int num;
int cnt,a;


void topologicalSort(){
    num=0;
    while(!q.empty()) q.pop();
    for(int i=1;i<=n;i++)
        if(inDegree[i]==0)  q.push(i);

    while(!q.empty()){
        int u=q.front();
         res.push_back(u);
        q.pop();
        for(int i=0;i<(int)e[u].size();i++){
            int v=e[u][i];
            inDegree[v]--;
            if(inDegree[v]==0){
                q.push(v);

            }
        }
        //e[u].clear();
        num++;
    }

}

int main(){
    int t;
    int a,b;
    scanf("%d",&t);
    while(t--){
        scanf("%d%d",&n,&m);
		for(int i=0;i<=n;i++){
            e[i].clear();
            inDegree[i]=0;
        }
        for(int i=0;i<m;i++){
            scanf("%d%d",&a,&b);
            e[a].push_back(b);
            //e[b].push_back(a);
            inDegree[b]++;
            //inDegree[a]++;
        }

        topologicalSort();

        for(int i=0;i<(int)res.size();i++)
            cout<<" "<<res[i];

    }
    return 0;
}
```


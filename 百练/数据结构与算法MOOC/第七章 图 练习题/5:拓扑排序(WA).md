### 思路：
* 图为有向图
* 存储图的数组不能太大
* [priority_queue自定义排序](https://www.cnblogs.com/yalphait/articles/8889221.html)
  * ```priority_queue<pair<int,int>,vector<pair<int,int> >,greater<pair<int,int> > > coll;```，小顶堆，升序
  * ```priority_queue<int, vector<int>, greater<int> > q;```，小顶堆，升序


```
#include <bits/stdc++.h>

using namespace std;

const int maxn=10010;

vector<int> e[maxn],res;
int n,m,inDegree[maxn];
priority_queue<int,vector<int>, greater<int> > q;
int num;
int cnt,a;


void topologicalSort(){
    num=0;
    while(!q.empty()) q.pop();
    for(int i=1;i<=n;i++)
        if(inDegree[i]==0)  q.push(i);

    while(!q.empty()){
        int u=q.top();
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

    int a,b;
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

    for(int i=0;i<(int)res.size();i++){
        if(i==0)
            cout<<"v"<<res[i];
        else
            cout<<" v"<<res[i];
    }

    return 0;
}
```


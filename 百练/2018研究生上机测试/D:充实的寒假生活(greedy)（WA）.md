

### 思路：
* 区间贪心

```
#include <bits/stdc++.h>

using namespace std;

struct Node{
    int st,ed;
}node[10010];

bool cmp(const Node &a,const Node &b){
    if(a.st!=b.st)
        return a.st<b.st;
    else
        return a.ed<b.ed;
}

int main(){
    int n;
    scanf("%d",&n);
    for(int i=0;i<n;i++)    scanf("%d%d",&node[i].st,&node[i].ed);

    sort(node,node+n,cmp);
    int ans=1;
    int preed=node[0].ed;
    for(int i=1;i<n;i++){
        if(node[i].st>=preed){
            preed=node[i].ed;
            ans++;
        }
    }
    printf("%d\n",ans);

    return 0;
}

```

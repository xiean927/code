

```
#include <bits/stdc++.h>

using namespace std;

int in[1010],e[1010][1010];
vector<int> vec;

int main(){
    int v,a;
    int x,y;
    memset(e,0,sizeof(e));
    scanf("%d%d",&v,&a);
    for(int i=0;i<a;i++){
        scanf("%d%d",&x,&y);
        in[y]++;
        e[x][y]=1;
        //out[x]++;
    }
    set<int> st;
    while(true){
        int i;
        for(i=1;i<=v;i++)
            if(in[i]==0&&st.find(i)==st.end())    break;
        vec.push_back(i);
        st.insert(i);
        for(int j=1;j<=v;j++)
            if(e[i][j])
                in[j]--;
        if((int)vec.size()==v)
            break;
    }
    for(int i=0;i<(int)vec.size();i++)
        printf("%d ",vec[i]);

    return 0;
}

```

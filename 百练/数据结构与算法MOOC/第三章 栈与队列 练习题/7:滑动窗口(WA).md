* 我的常规做法,```WA```代码
```
#include <bits/stdc++.h>

using namespace std;

vector<int> vMax,vMin;
int a[1000010];

int Find_Max(int st,int ed){
    int Max=0;
    for(int i=st;i<ed;i++)
        if(a[i]>Max)    Max=a[i];
    return Max;
}

int Find_Min(int st,int ed){
    int Min=0x3f3f3f3f;
    for(int i=st;i<ed;i++)
        if(a[i]<Min)    Min=a[i];
    return Min;
}

int main(){
    int n,k;
    scanf("%d%d",&n,&k);
    for(int i=0;i<n;i++)
        scanf("%d",&a[i]);
    for(int i=0;i+k<=n;i++){
        int Max=Find_Max(i,i+k);
        int Min=Find_Min(i,i+k);
        vMax.push_back(Max);
        vMin.push_back(Min);
    }

    for(int i=0;i<(int)vMin.size();i++){
        printf("%d",vMin[i]);
        if(i<(int)vMin.size()-1)
            printf(" ");
    }
    printf("\n");
    for(int i=0;i<(int)vMax.size();i++){
        printf("%d",vMax[i]);
        if(i<(int)vMax.size()-1)
            printf(" ");
    }

    return 0;
}

```

* 滑动窗口法未看懂，















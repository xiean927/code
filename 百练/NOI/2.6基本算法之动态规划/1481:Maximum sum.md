### 思路：
* 顺着倒着各求一次最大连续子序列和，分成前后两部分，求最大值
* [不懂为什么要在```A[0]与0```之间取小值](https://www.cnblogs.com/Willendless/p/9399095.html)
```
#include <bits/stdc++.h>

using namespace std;

int A[50010],dpl[50010],dpr[50010],prenum[50010];
int lmax[50010],rmax[50010];

int main(){
    int k,n;
    scanf("%d",&k);
    while(k--){
        memset(A,0,sizeof(A));
        memset(dpl,0,sizeof(dpl));
        memset(dpr,0,sizeof(dpr));
        memset(lmax,0,sizeof(lmax));
        memset(rmax,0,sizeof(rmax));
        memset(prenum,0,sizeof(prenum));
        scanf("%d",&n);

        for(int i=0;i<n;i++){
            scanf("%d",&A[i]);
            //if(i==0)
            //    prenum[0]=A[0];
            //else
            //    prenum[i]=prenum[i-1]+A[i];
        }
        dpl[0]=A[0];lmax[0]=A[0];
        for(int i=1;i<n;i++){
            dpl[i]=max(dpl[i-1]+A[i],A[i]);
            lmax[i]=max(lmax[i-1],dpl[i]);
        }
        dpr[n-1]=A[n-1];rmax[n-1]=A[n-1];
        for(int i=n-2;i>=0;i--){
            dpr[i]=max(dpr[i+1]+A[i],A[i]);
            rmax[i]=max(rmax[i+1],dpr[i]);
        }
        int ans=lmax[0]+rmax[1];
        for(int i=1;i<n-1;i++)
            ans=max(ans,lmax[i]+rmax[i+1]);
        printf("%d\n",ans);
    }

    return 0;
}

```

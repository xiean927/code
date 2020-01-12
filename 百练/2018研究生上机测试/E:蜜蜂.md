### ```dp动态规划```

```
#include <bits/stdc++.h>

using namespace std;

int dp[50][50];

int main(){
    ///计算以1为起点的
    dp[1][1]=1;
    dp[1][2]=1;
    for(int i=3;i<=49;i++){
        dp[1][i]=dp[1][i-1]+dp[1][i-2];
    }

    //for(int i=3;i<=6;i++)
    //    printf("%d:%d\n",i,dp[1][i]);

    ///i:起点
    for(int i=2;i<49;i++){
        dp[i][i]=1;
        dp[i][i+1]=1;
        for(int j=i+2;j<49;j++)
            dp[i][j]=dp[i][j-1]+dp[i][j-2];

    }

    int n;
    scanf("%d",&n);
    int a,b;
    for(int i=0;i<n;i++){
        scanf("%d%d",&a,&b);
        printf("%d\n",dp[a][b]);
    }

    return 0;
}

```


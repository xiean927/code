
### 思路：
* 最大矩阵和问题
### 关键代码：
* ```ans=max(ans,width*1);///这一句是判断当只有一行时，面积是否为最大，不加这句，最后示例结果会得4```
* ```width=min(width,dp[k][j]);  ans=max(ans,width*(i-k+1));```计算最大宽度，乘上高度，就是矩阵面积

```
#include <bits/stdc++.h>

using namespace std;

int mp[25][25],dp[25][25];

int main(){
    int m,n;
    scanf("%d%d",&m,&n);
    for(int i=1;i<=m;i++)
    for(int j=1;j<=n;j++)
        scanf("%d",&mp[i][j]);
    for(int i=1;i<=m;i++){
        if(mp[i][1]==0) dp[i][1]=1;///最左边一列dp数组置1
        else dp[i][1]=0;
        for(int j=2;j<=n;j++){
            if(mp[i][j]==0) dp[i][j]=dp[i][j-1]+1;///在每一行一直向右延伸，不断更新dp数组
            else    dp[i][j]=0;
        }
    }
/*
长方形的宽:width
长:ans
*/
    int ans=0,width=0;
    for(int i=1;i<=m;i++){
        for(int j=1;j<=n;j++){
            if(mp[i][j]==0){
                width=dp[i][j];///从该位置向左的位置
                ans=max(ans,width*1);///这一句是判断当只有一行时，面积是否为最大，不加这句，最后示例结果会得4
                for(int k=i-1;k>=1;k--){///在此位置的上边遍历，寻找最小的宽
                    if(mp[k][j]==1)///如果是障碍，就直接退出
                        break;
                    else{
                        width=min(width,dp[k][j]);///更新最小的宽
                        ans=max(ans,width*(i-k+1));///更新长方形的高的最大值
                    }
                }
            }
        }
    }
    printf("%d\n",ans);
    return 0;
}
```

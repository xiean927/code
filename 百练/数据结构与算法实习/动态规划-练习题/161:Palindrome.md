
### 题目：
* 求一个字符串成为回文串，所要插入的最少字符个数

### 思路：
* [最长公共子序列(LCS)+滚动数组](https://blog.csdn.net/better_space/article/details/52195314)
* 需要添加的字符个数=总字符数-正序与倒序字符串的最长公共子序列的长度。



```
#include<bits/stdc++.h>

using namespace std;

const int maxn = 5001;
char a[maxn],b[maxn];
int dp[2][maxn];

int main() {
	int n,i,j;
	while(scanf("%d",&n)!=EOF) {
		memset(dp,0,sizeof(dp));
		scanf("%s",a);
		for(i=0; i<n; i++)
			b[i]=a[n-1-i];
		for(i=1; i<=n; i++)
			for(j=1; j<=n; j++)
				if(a[i-1]==b[j-1])
					dp[i%2][j]=dp[(i-1)%2][j-1]+1;
				else
					dp[i%2][j]=max(dp[(i-1)%2][j],dp[i%2][j-1]);
		printf("%d\n",n-dp[n%2][n]);
	}
	return 0;
}

```


### 思路
* 动态规划

```
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <vector>
using namespace std;

int dp[10010], w[10010];
bool choice[10010][110];
bool cmp(int a, int b) {
	return a > b;
}

int main() {
	int n, m;
	scanf("%d%d", &n, &m);
	for (int i = 1; i <= n; i++) {
		scanf("%d", &w[i]);
	}
	sort(w + 1, w + n + 1, cmp);///以价值的从小到大排序
	for (int i = 1; i <= n; i++) {///物品号
		for (int j = m; j >= w[i]; j--) {
			if (dp[j] <= dp[j - w[i]] + w[i]) {
				choice[i][j] = true;
				dp[j] = dp[j - w[i]] + w[i];
			}
		}
	}
	if (dp[m] != m)
		printf("No Solution");
	else {
		vector<int> arr;
		int v = m, index = n;///总钱数序号
		while (v > 0) {
			if (choice[index][v] == true) {///序号从后向前枚举
				arr.push_back(w[index]);///
				v -= w[index];///价值减少
			}
			index--;///序号减1
		}
		for (int i = 0; i < arr.size(); i++) {
			if (i != 0)
				printf(" ");
			printf("%d", arr[i]);
		}
	}
	return 0;
}
```

* [```dfs解法```](https://blog.csdn.net/qq_38996065/article/details/99620300)

```
#include <bits/stdc++.h>

using namespace std;

const int maxn=110;
///num数组:每种硬币的实际数量,
///ans数组:每种硬币的输出数量
int num[maxn],ans[maxn];
int n,m;
bool flag=false;///判断是否有合法序列输出

///cur:当前总费用
///pre:上一次累加的费用数
void dfs(int cur,int pre){
    if(cur>m)
        return ;
    if(cur==m&&flag==false){
        bool sflag=false;
        flag=true;
        for(int i=1;i<=m;i++){
            if(ans[i]){
                for(int j=0;j<ans[i];j++){
                    if(sflag==false)
                        printf("%d",i);
                    else
                        printf(" %d",i);
                    sflag=true;
                }
            }
        }
    }

    for(int i=pre;i<=m-cur;i++){
        if(ans[i]+1<=num[i]){///如果硬币总数小于给定的硬币数
            ans[i]++;
            dfs(cur+i,i);
            ans[i]--;
        }
    }
}

int main(){
    int tmp;
    scanf("%d%d",&n,&m);
    for(int i=0;i<n;i++){
        scanf("%d",&tmp);
        ///只有当硬币币值小于等于给定的m时，才可以
        if(tmp<=m)  num[tmp]++;
    }
    dfs(0,1);
    if(flag==false)
        printf("No Solution\n");
    return 0;
}
```

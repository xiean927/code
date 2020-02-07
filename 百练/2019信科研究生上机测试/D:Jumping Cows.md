### 题意：
* 奶牛喜欢跳，在月光之下，就像奶牛在他们最喜欢的旋律之下

* 当地的医生混合了P剂量的药品来解决奶牛的跳跃问题
* 剂量被产生按照他们创造的顺序
* 每个剂量有一个力量来增强奶牛的跳跃能力
* 当是奇数步时增加奶牛的跳跃能力，当当是剂量为偶数时减少奶牛的跳跃能力
* 在给出任何剂量之前，奶牛的跳跃能力为0，

* 没有剂量会给两次，一旦奶牛接受这个剂量，一个剂量一定会被给出，当以1开始时，
* 在一次循环下，一个或多个剂量被跳过

* 题目大意：题目要求从输入的p个数中任意选出n(n<=p)个数按输入顺序排好，假设给n个数1至N编号，若i(1<=i<=N)是偶数，则将第i个数变为负数，最后求n个数的最大和。

### 输入：
* 第1行，P
* 第2----P+1行，每一行包含一个整数，显示剂量的力量

### 输出：
* 奶牛最远跳多远

### 思路：

* 1,```二维dp```数组,
  * 0维,1维分别记录奇数步,偶数步
  
  
```
#include <bits/stdc++.h>

using namespace std;

const int maxn = 150005;

int dp[maxn][2],a[maxn];

int max(int x,int y)
{
	if(x>y)
		return x;
	else
		return y;
}

int main()
{
    int n,i;
	while(scanf("%d",&n)!=EOF)
	{
        for(i=1;i<=n;i++)   scanf("%d",&a[i]);
		memset(dp,0,sizeof(dp));
		memset(dp,0,sizeof(dp));
		dp[2][0]=max(0,a[1]-a[2]);///从第1步开始跳,第2步也跳
		dp[2][1]=max(a[1],a[2]);///从第2步或第1步开始跳
		for(i=3;i<=n;i++)
		{
		    /*
		    dp[3][0]=max(dp[2][0],dp[2][1]-a[3]);///max(从第1步开始跳 第2步也跳,从第1步或第2步开始跳 - 第3步跳的剂量(因为是第2次跳(偶数步)))
		    dp[3][1]=max(dp[2][1],dp[2][0]+a[3]);///max(从第1步或第2步开始跳,从第1步开始跳,第2步也跳 + 第3步跳的剂量)
		    
		    dp[4][0]=max(dp[3][0],dp[3][1]-a[4]);///max( max(从第1步开始跳,从第1步或第2步开始跳 - 第3步跳的剂量(因为是第2次跳(偶数步))) ,
                                                 ///  (从第1步或第2步开始跳,从第1步开始跳 第2步也跳 + 第3步跳的剂量) - 第4步跳(Q1:第2步,Q2:第4步))
		    dp[4][1]=max(dp[3][1],dp[3][0]+a[4]);/// max( max(从第1步或第2步开始跳,从第1步开始跳,第2步也跳 + 第3步跳的剂量),
                                                    (从第1步开始跳 第2步也跳,从第1步或第2步开始跳 - 第3步跳的剂量(因为是第2次跳(偶数步))) +第4步跳(Q1:第3步,Q2:第3步))
		    
		    
		    */
			dp[i][0]=max(dp[i-1][0],dp[i-1][1]-a[i]);///前面就是不选的状态
		    dp[i][1]=max(dp[i-1][1],dp[i-1][0]+a[i]);///从
		}
		printf("%d\n",max(dp[n][0],dp[n][1]));
	}
	return 0;
}


```

* [2,贪心](https://blog.csdn.net/zqf3535/article/details/78400782)
  * 直接贪心
  
```
#include <bits/stdc++.h>

using namespace std;

int a[150005];
int n;
int ans=0;
bool flag=true;

int main(){
    cin >> n;
    for (int i=1;i<=n;i++){
        cin >> a[i];
    }
/*
代码含义：
首先找到，奇数步，第一步大于第二步的位置，作为起始步
而后偶数步，找前一步比后一步小的位置

*/
    for (int i=1;i<=n;i++){
        if (flag){///奇数步
            if (a[i]>a[i+1]){///一开始，如果第一步a[1]的值大于a[2]的值，就蹦到a[1]，接着蹦a[2]
                ans+=a[i];///如果此时，
                flag=0;
            }
        }
        else{///偶数步
            if (a[i]<a[i+1]){///如果a[3]大于a[2]，就接着蹦到a[2],
                ans-=a[i];
                flag=1;
            }
        }
    }

    cout << ans << endl;
}

```
* 3,[在线算法]()

```
#include<bits/stdc++.h>

using namespace std;

int main() {
    int n,i,x;
    int ans,sum;
    while(~scanf("%d",&n)) {
        scanf("%d",&x);
        ans = x;///走第一步
        sum = 0;
        for(i=1; i<n; i++) {
            scanf("%d",&x);
            if(sum+x>ans)   ans = sum+x;
            ///走第2步 大于 走第1步 ans=第2步,sum=0
            ///走第3步 大于 走第2步 ans=第3步,sum=
            ///
            
            if(ans-x>sum)   sum = ans-x;
            ///走第1步 也走第2步 sum=第1步-第2步, 
            ///走第2步 也走第3步 sum=第2步-第3步,
            ///
            
            
        }
        if(ans>sum)
            printf("%d\n",ans);
        else
            printf("%d\n",sum);
    }
    return 0;
}
```



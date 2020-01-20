### [LCS+滚动数组,转自CSDN](https://blog.csdn.net/freezhanacmore/article/details/9768071)
#### 题意： 

* 求最长公共上升子序列，就是第一个序列和第二个序列中有几个相同的子序列：
* 如果有一个序列 <A1, A2, A3,... An> 还有个序列 <Ak1, A k2, ... A kn> 满足 k1 < k2 < k3，
  * 那么 第二个序列是第一个序列的子序列
* 最长公共子序列：
  * 就是从几个序列【一般是两个了】中找出一样的最长的子序列

#### 分析：
* 用 dp[i][j] 记录序列 A 中从 0 到 i-1  和序列 B 中从 0  到 j-1  的最长公共子序列长度,O（n^n）写法：
* 先初始化 dp 为 0
* 当 A 序列遍历到第 i-1 个,序列 B  遍历到第 j-1 个
  * (1) 如果此时 A[i-1] == B[j-1] , 那么可想而知 dp[i][j] = dp[i-1][j-1] +1
  * (2) 如果此时 A[i-1] != B[j-1], 那么 dp[i][j] = max( dp[i-1][j],  dp[i][j-1] )

* 总之相当于记忆化搜索的了 dp[i][j] 从左到右从上到下, 当确立了当前字符是否相等时
* 那么 dp[i][j] 就由它的左上角 ( dp[i-1][j-1] )、上面的 ( dp[i-1][j] )、前面的 ( dp[i][j-1] ) 确定
```
    /**
    求长度为 len1 的序列 A 和长度为 len2 的序列 B 的LCS
    注意：序列下标从 0 开始
    */
    void LCS(int len1,int len2)
    {
        for(int i = 1; i <= len1; i++)
        {
            for(int j = 1; j <= len2; j++)
            {
                if(s1[i-1] == s2[j-1]) dp[i][j] = dp[i-1][j-1]+1;
                else
                {
                    int m1 = dp[i-1][j];
                    int m2 = dp[i][j-1];
                    dp[i][j] = max(m1, m2);
                }
            }
        }
    }
```

* 将 dp[maxn][maxn]优化到 dp[2][maxn]
* 其实也是滚动数组的概念：
* 由上面的分析我们发现这一点：当前的 dp[i][j] 只是与以它为右下角的四个 dp 有关
  * ```dp[i-1][j-1]  dp[i-1][j]```
  * ```dp[i][j-1]    dp[i][j]```
* 而我们并不是要求出每一段的 LCS 而只是求出最终的长度的 LCS,那么每次对 i %2 就可以解决问题

```
void LCS(int len1,int len2)
{
    for(int i = 1; i <= len1; i++)
    {
        for(int j = 1; j <= len2; j++)
        {
            if(s1[i-1] == s2[j-1]) dp[i%2][j] = dp[(i-1)%2][j-1]+1;
            else
            {
                int m1 = dp[(i-1)%2][j];
                int m2 = dp[i%2][j-1];
                dp[i%2][j] = max(m1, m2);
            }
        }
    }
}
```














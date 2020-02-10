我的超时代码,83分
* 去TK题库下载的测试数据全对
```
#include <bits/stdc++.h>

using namespace std;

int in[25];
bool vis[25];
int n,k;

bool isprime(int x){
    if(x<=1)    return false;
    int sqr=sqrt(1.0*x);
    for(int i=2;i<=sqr;i++)
        if(x%i==0)  return false;
    return true;
}

int ans;
///和，走到的下标号，有多少个数被计算
void dfs(int sum,int index,int cnt){
    if(cnt>k||index>=n)
        return ;
    if(isprime(sum)&&cnt==k){
        ans++;
        return ;
    }
    //printf("sum:%d index:%d cnt:%d\n",sum,index,cnt);
    for(int i=index;i<n;i++){
        if(vis[i]==false){
            vis[i]=true;
            dfs(sum+in[i],i,cnt+1);///改成i+1,得17分
            vis[i]=false;
        }
    }
}

int main(){
    scanf("%d%d",&n,&k);
    for(int i=0;i<n;i++)
        scanf("%d",&in[i]);

    ans=0;
    dfs(0,0,0);
    printf("%d\n",ans);
    return 0;
}

```
* [题解1](https://blog.csdn.net/Mr_Zhangmc/article/details/81941836)
* [题解2](https://blog.csdn.net/hjl_heart/article/details/104002447)


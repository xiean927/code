## [关于lower_bound( )和upper_bound( )的常见用法](https://blog.csdn.net/qq_40160605/article/details/80150252)
## 得拿手推导一下，不然真的不懂

## 01:查找最接近的元素

* ```TLE```代码

```
#include <bits/stdc++.h>

using namespace std;

int a[100010];

struct Node{
    int num,minu;
}node[100010];

bool cmp(const Node a,const Node b){
    return a.minu<b.minu;
}

int main(){
    int n,m,tmp;
    scanf("%d",&n);
    for(int i=0;i<n;i++)    scanf("%d",&node[i].num);
    scanf("%d",&m);
    for(int i=0;i<m;i++){
        scanf("%d",&tmp);
        for(int i=0;i<n;i++)
            node[i].minu=abs(node[i].num-tmp);
        sort(node,node+n,cmp);
        cout<<node[0].num<<endl;
    }
    return 0;
}
```

* ```AC```代码
```
#include <bits/stdc++.h>

using namespace std;

int a[100010];


int main(){
    int n,m,tmp;
    scanf("%d",&n);
    for(int i=0;i<n;i++)    scanf("%d",a+i);
    scanf("%d",&m);
    for(int i=0;i<m;i++){
        scanf("%d",&tmp);
        int j=lower_bound(a,a+n,tmp) - a;///输入10 返回3
        if(j==n){///说明不存在大于等于tmp的数，也就是都小于,
            cout<<a[j-1]<<endl;
        }
        else{
            if(j>0){
                if(abs(a[j]-tmp)>abs(a[j-1]-tmp))
                    cout<<a[j-1]<<endl;
                else if(abs(a[j]-tmp)<abs(a[j-1]-tmp))
                    cout<<a[j]<<endl;
                else
                    cout<<a[j-1]<<endl;///若有多个值满足条件，输出最小的一个。
            }
            else
                cout<<a[j]<<endl;
        }

    }
    return 0;
}

```
### 利用自己写的二分来构建

## 02:二分法求函数的零点

* ```AC代码```
```
#include <bits/stdc++.h>

using namespace std;

double result(double x){
    return pow(x,5)-15*pow(x,4)+85*pow(x,3)-225*pow(x,2)+274*x-121;
}

int main(){
    double st=1.5,ed=2.4;
    double mid;

    while(ed-st>0.00000001){
        mid=(ed-st)/2+st;
        if(result(mid)==0.0)
            break;
        else if(result(mid)*result(st)<0)
            ed=mid;
        //写成这样，错误：else if(result(mid)*result(ed)<0)///有根存在
        else
            st=mid;
    }

    printf("%.6lf",mid);
    return 0;
}
```
* [转自CSDN](https://blog.csdn.net/mayuan2017/article/details/78534427)
  * 
```
#include <iostream>
#include <iomanip>
#include <cmath>
using namespace std;
bool check(double mid)
{
    double f = pow(mid,5)-15.0*pow(mid,4)+85.0*pow(mid,3)-225.0*pow(mid,2)+274.0*mid-121.0;
    if(f > 0.0) return 1;
    return 0;
}
int main()
{
    double l=1.5, r=2.4, mid;
    while(r-l > 0.00000001){
        mid = (l+r)/2.0;
        if (check(mid)) l = mid;
        else r = mid;
    }
    cout << fixed << setprecision(6) << mid << endl;
    return 0;
}
```

## 03:矩形分割
* [二分查找+降维处理](https://blog.csdn.net/liusu201601/article/details/88416993)
* [题解2](https://blog.csdn.net/SSYITwin/article/details/81543534)
* [题解3](https://blog.csdn.net/zhhe0101/article/details/52794852)

* 8分代码
```
#include <bits/stdc++.h>

using namespace std;

typedef long long ll;

ll R,N;
struct Rec{
    ll L,T;///小矩形的左上角坐标是(L,T)
    ll W,H;///宽度是W，高度是H
}rec[10010];
int a[1000005];


ll area[2];///0：左边的面积；1：右边的面积
ll make_area(int n){///以x=n作为分隔线，计算左右两端的面积
    area[0]=0,area[1]=0;

    for(int i=0;i<N;i++){///计算分割线以左的矩形面积
        if(rec[i].L+rec[i].W<=n){///如果矩形完全在直线的左侧
            area[0]+=rec[i].H*rec[i].W;
        }
        else if(rec[i].L<n&&rec[i].L+rec[i].W>n){///如果矩形有一部分在左侧
            area[0]+=rec[i].H*(n-rec[i].L);
        }
    }

    for(int i=0;i<N;i++){///计算分割线以左的矩形面积
        if(rec[i].L>n){///如果矩形完全在直线的右侧
            area[1]+=rec[i].H*rec[i].W;
        }
        else if(rec[i].L<n&&rec[i].L+rec[i].W>n){///如果矩形有一部分在右侧
            area[1]+=rec[i].H*(rec[i].W+rec[i].L-n);
        }
    }

    return area[0]-area[1];
}

int main(){
    scanf("%lld%lld",&R,&N);
    memset(a,0,sizeof(a));
    for(int i=0;i<N;i++){
        scanf("%lld%lld%lld%lld",&rec[i].L,&rec[i].T,&rec[i].W,&rec[i].H);
        for(int j=rec[i].L;j<rec[i].L+rec[i].W;j++){
			a[j]+=rec[i].H;
		}
    }
    ll st=0,ed=R,mid;

    if(N==1&&rec[0].W==1){
        cout<<R<<endl;
        return 0;
    }

    while(st+3<ed){
        mid=(ed-st)/2+st;

        if(make_area(mid)<=0)
            st=mid;
        else
            ed=mid;
        //else{
          //  ok=mid;
         //   break;
        //}

    }
    int ans;
    ll su=999999999999;//因为 这个longlong，搞了2个小时！！！
	for(int i=ed;i>=st;i--)//对终值进行简单的判断
	{
		ll s=make_area(i);
		if(s>=0&&s<su) {su=s; ans=i;}
	}
    //细节2：需要切线尽可能靠右
	while(ans<R&&a[ans]==0) ans++;

	printf("%d",ans);
    return 0;
}
```

## 04:网线主管
* [二分注意边界问题](https://blog.csdn.net/a402630999/article/details/8710835)
  * 我刚看得画一下图
* [题解1](https://www.cnblogs.com/sjymj/p/5244811.html)
* [题解2](https://blog.csdn.net/ehdhg13455/article/details/81408918)
 ```
 二分法：

l 可行边界

r 不可行边界

终止条件 l == r - 1

注意：输出“0.00” 的判断

当 l ！= 0时，即可认为找到可行解
 ```
* [题解3](https://blog.csdn.net/WhiStLenA/article/details/51588752)
* 10分代码
```
#include <bits/stdc++.h>

using namespace std;

double a[10010];
int N,K;

int get_nums(double len){
    int cnt=0;///计算
    for(int i=0;i<N;i++)    cnt+=a[i]/len;
    return cnt;
}

int main(){
    double maxx=0;
    scanf("%d%d",&N,&K);///库存中的网线数,N;需要的网线数量,K
    for(int i=0;i<N;i++){
        //scanf("%lf",&a[i]);
        cin>>a[i];
        a[i]*=100;
        maxx=max(maxx,a[i]);
    }
    //sort(a,a+N);
    int st=0,ed=maxx+1,mid;///double => int 10分
    while(st+1<ed){///左开右开区间
        mid=(ed-st)/2+st;
        if(get_nums(mid)<K)///得到的根数小于题目所需
            ed=mid;
        else
            st=mid;
    }

    printf("%.2lf\n",st/100.00);
    return 0;
}
```
















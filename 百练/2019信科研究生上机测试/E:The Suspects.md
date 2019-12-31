### 题意：
* SARA一种不知名的
* 为了最小化传递给他人，最好的策略是隔离被怀疑患者
* 在不传播你的疾病的大学里，这里有一些学生分组。
* 在一个组内的学生频繁和其他人交流，并且一个学生可能会加入其它分组，为了繁殖SARA的传染，
* 收集了所有学生分组的成员信息，在他们的标准化下程序下按如下规则运转
* 一旦分组内的一个成员被怀疑，这个分组内的所有人员都被怀疑。
* 然而，发现所有被怀疑患者不是容易的当一个学生被识别为一个患者时，


### 输入：
* N，学生人数；M，学生组数
* 0 < n <= 30000 and 0 <= m <= 500

* 每个学生编号唯一，0~N-1
* 初始化被怀疑学生编号为0，
### 输出：
* 被怀疑总人数

### 思路：
* 简单并查集
```
#include <bits/stdc++.h>

using namespace std;

int n,m;
int father[30010],cnt[30010];
bool exists[30010];

int findFather(int x){
    int a=x;
    while(x!=father[x])
        x=father[x];

    while(a!=father[a]){
        int z=a;
        a=father[a];
        father[z]=x;
    }
    return x;
}


void Union(int a, int b) {
	int faA = findFather(a);
	int faB = findFather(b);
	if (faA != faB)
		father[faA] = faB;
}

int main(){

    int k,tmp,id;
    while(scanf("%d%d",&n,&m)){
        if(n==0&&m==0)  break;
        for(int i=0;i<30010;i++)
            father[i]=i;
        for(int i=0;i<m;i++){
            scanf("%d%d",&k,&id);
            for(int j=0;j<k-1;j++){
                scanf("%d",&tmp);
                Union(id,tmp);
            }
        }
        int resnum=1;
        int zeronum=findFather(0);///0号怀疑人员的分组
        for(int i=1;i<n;i++){
            int gnum=findFather(i);
            if(gnum==zeronum)
                resnum++;
        }
        printf("%d\n",resnum);
    }
    return 0;
}

```







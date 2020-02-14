* 测试用例推演
```
11 3
25 18 0 46 37 3 19 22 57 56 10
6 0 8 7 10 5 9 1 4 2 3

4组
19 25 57 22 10 3 56 18 37 0 46
5  5        5  5    5  5  5 

2组
57 22 56 46
   3  3

1组
57 46
2   2

57
1  

```


```
#include <bits/stdc++.h>

using namespace std;

/*
一开始有Np个程序员,然后每Ng个程序员分成一组
一组中最快的进入下一组,然后Ng个人组成下一组,

假定重量就是得分,

如果最后一组少于Ng个人,那么把剩下的人分成另一组,

line3:给出每只老鼠的位置
11 3
25 18 0 46 37 3 19 22 57 56 10
6 0 8 7 10 5 9 1 4 2 3

6号老鼠在第1个位置,
0号老鼠在第2个位置
8号老鼠在第3个位置
...

*/


const int maxn=1010;
struct mouse{
  int weight,R;
}mouse[maxn];

int main(){
    int np,ng,order;
    queue<int> q;
    scanf("%d%d",&np,&ng);
    for(int i=0;i<np;i++)
        scanf("%d",&mouse[i].weight);
    for(int i=0;i<np;i++){
        scanf("%d",&order);
        q.push(order);
    }
    int temp=np,group;//temp为参赛总人数，group为参赛组数
    while(q.size()!=1){
        if(temp%ng==0)///如果参赛总人数/参赛组数 为 整数
            group=temp/ng;
        else
            group=temp/ng+1; ///否则多一组
        for(int i=0;i<group;i++){///组数
            int k=q.front();
            for(int j=0;j<ng;j++){///是每组的人数，而不是总人数
                if(i*ng+j>=temp){///如果这些人超出组,就退出
                    break;
                }
                int front_=q.front();
                if(mouse[front_].weight>mouse[k].weight){///寻找该组中的最大重量
                    k=front_;
                }
                mouse[front_].R=group+1;///被淘汰的人(一开始将组内所有人记为相同名次)的名次为group+1(通过判断得到的)
                q.pop();
            }
            q.push(k);///推入该组的优胜者
        }
        temp=group;///最后要更新参赛人数
    }
    mouse[q.front()].R=1;///优胜者
    for(int i=0;i<np;i++){
        printf("%d",mouse[i].R);
        if(i<np-1)
            printf(" ");
    }
    return 0;
}

```

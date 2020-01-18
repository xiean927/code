### 题意：
* 输出数字出现次数第二多的数字，并且按顺序输出。
### 思路：
* 典型的索引字典思想+获得第二次数多的值的方法注意点，即先获取最大的值然后据此找到第二大的值。
* [转自CSDN](https://blog.csdn.net/hackerwin7/article/details/40896183)

```
#include<stdio.h>
#include<string.h>
int players[10000+1];//begin with 1
int N=0,M=0;
int main()
{
    while(scanf("%d%d",&N,&M)!=EOF&&(M+N)>0)
    {
        memset(players,0,sizeof(players));
        int num=0,max_cnt=0,sec_cnt=0;
        for(int i=1;i<=N;i++)
        {
            for(int j=1;j<=M;j++)
            {
                scanf("%d",&num);
                players[num]++;
                if(players[num]>max_cnt) max_cnt=players[num];
            }
        }
        int j=0;
        for(sec_cnt=max_cnt-1;sec_cnt>=1;sec_cnt--)
        {
            int find_flag=0;
            for(j=1;j<=10000;j++)
            {
                if(sec_cnt==players[j]) {find_flag=1;printf("%d",j);break;}///输出第一个第二多的数
            }
            if(find_flag) break;
        }
        for(j=j+1;j<=10000;j++) if(sec_cnt==players[j]) printf(" %d",j);///输出剩余的第二多的数
        printf("\n");
    }
    return(0);
}

```

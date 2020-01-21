### 描述
* 决定邀请小孩参加她的婚礼纪念日，她想要准备一个正方形巧克力蛋糕并且已知大小。
* 她问每一个被邀请的人来决定他想要的蛋糕片的大小（应该是正方形的）
* 她知道他不会允许任何浪费，他也知道他是否能够做一个正方形蛋糕来服务所有人大小，并且没有浪费

### 输入
* line1,t,测试用例数
* line2 -- t+1 ,s,蛋糕的边长,n,蛋糕片的数目,1~n个蛋糕片的边长

### 输出
* 没有浪费输出 KHOOOOB! ,有浪费输出 HUTUTU!


```
#include <bits/stdc++.h>

using namespace std;

int col[45]; //将蛋糕分为1*1的小块，下标表示列，值表示用到第几行
int cakesize;   //蛋糕大小
int part[11];    //数组值为该大小的小块的个数
int num;    //蛋糕个数

bool DFS(int fillnum)     //从前往后，从左往右放入
{
    int min=50;
    int flag;///所在列
    int wide;
    if(fillnum==num)//安排好num个正方形块
        return true;
    for(int i=1; i<=cakesize; i++)   //记录所有列里所用最少的
        if(min>col[i]){
            min=col[i];
            flag=i;
        }
    for(int size=10; size>0; size--)    //从大到小遍历，从大的开始放，越小灵活性越大
    {
        if(!part[size])					//如果存在未用过的
            continue;
        if(cakesize-min>=size&&cakesize-flag+1>=size)   //判断蛋糕放入‘是否有可能’溢出，是否有‘可能’放入
        {// 蛋糕的边长 - 列所用的行数 >= 蛋糕片的边长
		 // 蛋糕的边长 - 列数 + 1 >= 蛋糕片的边长，加1是因为数组的索引决定的
		 
            wide=0;                      //之前错在这里
            for(int j=flag; j<=flag+size-1; j++)  //与上面的if判断一起，其作用为判断是否能放下该块蛋糕
            {//判断 flag ~ flag+size_-1 列 能否放下,
                if(col[j]<=min)///
                    wide++;
                else
                    break;
            }
            if(wide>=size)//如果可以放下
            {
                part[size]--;//可以放下一个
                for(int k=flag; k<=flag+size-1; k++)
                    col[k]+=size;
                if(DFS(fillnum+1))
                    return true;
                part[size]++;                              //回溯
                for(int k=flag; k<=flag+size-1; k++)
                    col[k]-=size;//每一列减去要添加的正方形片
            }
        }
    }
    return false;
}

int main()
{
    int t,side;
    cin>>t;
    while(t--)
    {
        memset(part,0,sizeof(part));
        memset(col,0,sizeof(col));
        cin>>cakesize;
        cin>>num;
        for(int i=1; i<=num; i++)
        {
            cin>>side;
            part[side]++;///记录大小
        }
        if(DFS(0))
            cout<<"KHOOOOB!"<<endl;
        else
            cout<<"HUTUTU!"<<endl;
    }
    return 0;
}
```

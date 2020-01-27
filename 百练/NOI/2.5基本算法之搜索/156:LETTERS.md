
### 描述：
* 给出一个R*C的大写字母矩阵，开始的位置为左上角，你可以向上下左右四个方向移动，但不能访问同一字母两次。
* 问最多可以移动几个位置，即最多可以访问几个字母。 
### 输入：
* 第一行，输入字母矩阵的行数R和列数C，1 <= R, C <= 20。
* 接着输出R行C列字母矩阵。
### 输出：
* 最多可以访问的字母个数。

### [思路,转自CSDN](https://blog.csdn.net/qiaoruozhuo/article/details/75171314)
* 连英语也看不懂


```
#include <bits/stdc++.h>

using namespace std;

bool letters[30];
char mp[30][30];
int R,C;
int maxans;
int mov[4][2]={{0,1},{1,0},{0,-1},{-1,0}};


void DFS(int row,int col,int step){
    if(step>maxans)
        maxans=step;

    for(int i=0;i<4;i++){
        int dx=row+mov[i][0];
        int dy=col+mov[i][1];
        if(dx>=0&&dx<R&&dy>=0&&dy<C&&!letters[mp[dx][dy]-'A']){
            letters[mp[dx][dy]-'A']=true;
            DFS(dx,dy,step+1);
            letters[mp[dx][dy]-'A']=false;
        }
    }
}

int main()
{
    scanf("%d%d",&R,&C);
    for(int i=0;i<R;i++){
        getchar();
        for(int j=0;j<C;j++)
            scanf("%c",&mp[i][j]);
    }

    memset(letters,false,sizeof(letters));
    letters[mp[0][0]-'A']=true;
    maxans=0;
    DFS(0,0,1);

    cout<<maxans<<endl;

    return 0;
}

```

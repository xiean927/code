### 思路：
* 构建图

```
#include <bits/stdc++.h>

using namespace std;

struct module
{
	char north;
	char south;
	char east;
	char west; //上下左右四面墙
	int sum;
	int sr;
	int sc; // (sr,sc)记录到达此位置的上一个位置，以便返回
	bool flag;
}md[50][50];

int main()
{
	int i,j,m , n; //m行，n列
	scanf("%d",&m);
	scanf("%d",&n);
	//struct module md[50][50];
	//struct module **md=(struct module**)malloc(sizeof(struct module)*m);
	for(i=0;i<m;i++){
        for(int j=0;j<n;j++){
            scanf("%d",&md[i][j].sum);
            if(md[i][j].sum%2==1)
                md[i][j].west='y';///西面是否是墙
            else
                md[i][j].west='n';
            md[i][j].sum/=2;
            if(md[i][j].sum%2==1)///北面是否是墙
                md[i][j].north='y';
            else
                md[i][j].north='n';
            md[i][j].sum/=2;
            if(md[i][j].sum%2==1)///东面是否是墙
                md[i][j].east='y';
            else
                md[i][j].east='n';
            md[i][j].sum/=2;
            if(md[i][j].sum%2==1)///南面是否是墙
                md[i][j].south='y';
            else
                md[i][j].south='n';
            md[i][j].flag=false;
        }
	}

	int r , c; //记录当前搜索的行和列
	int NumRoom ,MaxRoom,temp,count;
	count=0; //标记被占有的module
	NumRoom=0;
	MaxRoom=0;
	bool fg;
	while(count<m*n){
		fg=false;
		for(r=0;r<m;r++){
            for(c=0;c<n;c++){
                if(!md[r][c].flag){///如果是房间，就弹出
                    fg=true;
                    break;
                }
            }
            if(fg)
                break;
		}

		md[r][c].flag=true;///标记已经访问过了
		count++;
		temp=1;///记录房间面积
		i=r;
		j=c; ///记录开始搜索的位置
		md[r][c].sr=r;
		md[r][c].sc=c;
		int si,sj;
		int redo=0;//
		do{
			if(md[r][c].west=='n' && c>0 && !md[r][c-1].flag){
            ///西面无墙 未越界 且西面房间未访问过
				md[r][c-1].sr=r;
				md[r][c-1].sc=c;
				c--;
				count++;///房间数加1
				temp++;
				md[r][c].flag=true;///标记访问过
			}//左走，west
			else if(md[r][c].north=='n' && r>0 && !md[r-1][c].flag){
            ///北面无墙 未越界 且北面无墙
				md[r-1][c].sr=r;
				md[r-1][c].sc=c;
				r--;
				count++;
				temp++;
				md[r][c].flag=true;
			}//上走，north
			else if(md[r][c].east=='n' && c<n-1 && !md[r][c+1].flag){
            ///东面无墙 未越界 且东面无墙
				md[r][c+1].sr=r;
				md[r][c+1].sc=c;
				c++;
				count++;
				temp++;
				md[r][c].flag=true;
			}//右走，east
			else if(md[r][c].south=='n' && r<n-1 && !md[r+1][c].flag){
            ///南面无墙 未越界 且南面无墙
				md[r+1][c].sr=r;
				md[r+1][c].sc=c;
				r++;
				count++;
				temp++;
				md[r][c].flag=true;
			}//下走，south
			else{
            ///返回上一个位置
				si=md[r][c].sr;
				sj=md[r][c].sc;
				r=si;
				c=sj;
			}
			if(r==i&&c==j)///因为如果每一个都是墙，则r,c会等于原来开始位置，重复四次，就是探索四次
				redo++; ///在每个开始搜索的位置重复4次
		}while(redo<4);
		NumRoom++;
		if(temp>MaxRoom)///房间最大面积
			MaxRoom=temp;
	}
	printf("%d\n%d\n",NumRoom,MaxRoom);
	return 0;
}

```

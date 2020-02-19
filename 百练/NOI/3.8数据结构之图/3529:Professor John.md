
* [Floyd,计算传递闭包（例如：求不等式A<B,B<C）](https://blog.csdn.net/da_kao_la/article/details/80723562)

```
#include <bits/stdc++.h>

using namespace std;

const int maxn=110;
int e[maxn][maxn],backe[maxn][maxn];
int k,n;
char line[10];

/*
A<B
B<C
-->
A<C

*/

void Floyd(){
    for(int k=1;k<=26;k++)
        for(int i=1;i<=26;i++)
            for(int j=1;j<=26;j++)
                if(e[i][k]&&e[k][j])
                    e[i][j]=1;
}


int main(){
    int a,b,Case=1;
    bool flag;
    scanf("%d",&k);
    while(k--){
        flag=false;
        memset(e,0,sizeof(e));
        memset(backe,0,sizeof(backe));
        scanf("%d",&n);
        for(int i=0;i<n;i++){
            scanf("%s",line);
            a=line[0]-'A'+1;
            b=line[2]-'A'+1;
            if(line[1]=='>'){///
                e[b][a]=1;
                backe[b][a]=1;
            }
            else{
                e[a][b]=1;
                backe[a][b]=1;
            }
            //printf("a:%d ,b:%d\n",a,b);
        }
        Floyd();
        printf("Case %d:\n",Case++);
        for(int i=1;i<=26;i++){
            for(int j=1;j<=26;j++){
                if(e[i][j]&&!backe[i][j]){
                    printf("%c<%c\n",'A'+i-1,'A'+j-1);
                    flag=true;
                }
            }
        }
        if(!flag)
            printf("NONE\n");
    }

    return 0;
}


```

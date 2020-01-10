
### 并查集求闭包

```
#include <bits/stdc++.h>

using namespace std;

char mat[310][310];

int father[310];

int findfather(int x){
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
	int faA = findfather(a);
	int faB = findfather(b);
	if (faA != faB)
		father[faA] = faB;
}


int main(){
    int n;
    scanf("%d",&n);
    for (int i = 0; i < n; ++i) {
        scanf("%s", mat[i]);
        father[i] = i;
    }
    for (int i = 0; i < n; ++i)
    for (int j = 0; j < i; ++j)
        if (mat[i][j] == '1') Union(i, j);

    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j)
            putchar((i == j || findfather(i) == findfather(j)) ? '1' : '0');
        putchar('\n');
    }

    return 0;
}

```

### [warshall算法暴力自乘求闭包 OLE](https://blog.csdn.net/weixin_44646116/article/details/90544796)

```
#include <bits/stdc++.h>

using namespace std;

char mat[310][310];

int e[310][310];

int main(){
    int n;
    scanf("%d",&n);
    for (int i = 0; i < n; ++i) 
        scanf("%s", mat[i]);
    
    memset(e,0,sizeof(e));
    for (int i = 0; i < n; ++i)
    for (int j = 0; j < n; ++j)
        if (mat[i][j] == '1')   e[i][j]=1;

    for(int i=0;i<n;i++)         //warshall算法的核心代码部分
    for(int j=0;j<n;j++)
        if(e[j][i]>=1)
        for(int k=0;k<n;k++)
            e[j][k]=e[j][k]+e[i][k];

    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++) 	
            if(e[i][j]>1)   e[i][j]=1;

    for (int i = 0; i < n; ++i){
        for (int j = 0; j < n; ++j)
            printf("%d",e[i][j]);
        printf("\n");
    }
    return 0;
}

```




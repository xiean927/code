
### 思路：
* 求逆序对，[原题：1007:DNA排序](http://bailian.openjudge.cn/practice/1007/)

```
#include <bits/stdc++.h>

using namespace std;

char chr[55];

struct Str{
    char ch[55];
    int cnt;
    int order;
}str[105];

bool cmp(const Str &a,const Str &b){
    if(a.cnt!=b.cnt)
        return a.cnt<b.cnt;
    else
        return a.order<b.order;
}

int main()
{
    int m,n;
    scanf("%d%d",&n,&m);
    for(int k=0;k<m;k++){
        scanf("%s",str[k].ch);
        str[k].order=k;
        int len=strlen(str[k].ch);
        for(int i=0;i<len;i++)
            for(int j=i+1;j<len;j++)
            if(str[k].ch[i]>str[k].ch[j])
                str[k].cnt++;
    }
    sort(str,str+m,cmp);
    for(int k=0;k<m;k++)
        printf("%s\n",str[k].ch);

    return 0;
}


```

### 思路（没法检测是否写对了）：
* 回文串

```
#include <bits/stdc++.h>

using namespace std;

char chr[20];

int main()
{
    int k,cnt=0;
    scanf("%d",&k);
    getchar();
    while(k--){
        scanf("%s",chr);
        int len=strlen(chr);
        int lf=0,rt=len-1;
        bool flag=true;
        while(lf<=rt){
            if(chr[lf]!=chr[rt])
                flag=false;
            lf++,rt--;
        }
        if(flag)
            cnt++;
    }
    cout<<cnt<<endl;
    return 0;
}
```


* 这题没看懂什么```k```是什么意思???
* [题解](https://blog.csdn.net/NNNNNNNNNNNNY/article/details/51836152)

### 思路:
* 计算的```next_```数组，一开始是```-1```,所以在最后计算的时候要```减1```
```
#include <bits/stdc++.h>

using namespace std;

int next_[1000010];
char line[1000010];

void getNext(char s[],int len){
    int j=-1;
    next_[0]=-1;
    for(int i=1;i<len;i++){
        while(j!=-1&&s[i]!=s[j+1])
            j=next_[j];
        if(s[i]==s[j+1])
            j++;

        next_[i]=j;
    }
}


int main(){
    int n;
    int cases=0;
    while(scanf("%d",&n)&&n){
        scanf("%s",line);
        memset(next_,0,sizeof(next_));
        getNext(line,n);
        cout << "Test case #" << ++cases << endl;
        for(int i=2; i<=n; i++) {
            if (i%(i-next_[i-1]-1)==0 && i/(i-next_[i-1]-1) > 1) {
                cout << i << " " << i/(i-next_[i-1]-1) << endl;
            }
        }
        //for(int i=0;i<n;i++)
        //    printf("%d ",next_[i]);
        cout << endl;
    }
    
    return 0;
}
```

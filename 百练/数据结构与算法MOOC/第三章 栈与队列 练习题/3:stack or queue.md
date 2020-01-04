* ```WA```,很简单的一道题，但我做不对,
```
#include <bits/stdc++.h>

using namespace std;

int st[2010],que[2010];

int main(){
    int t;
    int n;
    int st_size,st_front,que_front,que_rear;
    scanf("%d",&t);
    while(t--){
        st_size=0,st_front=0,que_front=0,que_rear=0;
        scanf("%d",&n);
        bool st_qu=false;///如果是false，代表stack;如果是true，代表queue
        while(n--){
            int type,num;
            scanf("%d%d",&type,&num);
            if(type==1){///进栈,
                st_front=st_size;
                st[st_front++]=num;
                st_size=st_front;
                que[que_rear++]=num;
            }
            else{
                if(st[st_size-1]==num)
                    st_qu=false;
                st_size--;
                if(que[que_front]==num)
                    st_qu=true;
                que_front++;
            }
        }
        if(st_qu)
            printf("Queue\n");
        else
            printf("Stack\n");
    }
    return 0;
}
```



### 1078 Hashing (25分)
#### 题目大意：给出散列表长和要插入的元素，将这些元素按照读入的顺序插入散列表中，其中散列函数为h(key) = key % TSize，解决冲突采用只向正向增加的二次方探查法。如果题中给出的TSize不是素数，就取第一个比TSize大的素数作为TSize

* ```测试点3 运行超时```
* 加一个```break```就不超时了

```
#include <bits/stdc++.h>

using namespace std;

bool is_prime(int n){
    if(n<=1)    return false;
    int sqr=(int)sqrt(n*1.0);
    for(int i=2;i<=sqr;i++){
        if(n%i==0)
            return false;
    }
    return true;
}

unordered_map<int,int> table;
int a[11111];
bool vis[31111];
int main(){
    int MSize,N;
    scanf("%d%d",&MSize,&N);
    for(int i=0;i<N;i++){
        scanf("%d",a+i);
    }
    while(!is_prime(MSize)){
        MSize++;
    }

    for(int i=0;i<N;i++){
        int tmpos=a[i]%MSize;
        if(vis[tmpos]==false){///没有发生冲突
            table[a[i]]=tmpos;
            vis[tmpos]=true;
        }
        else{///发生冲突
            int flag=0;
            for(int j=0;j<MSize;j++){
                tmpos=(a[i]+j*j)%MSize;
                if(vis[tmpos]==false){///没有发生冲突
                    table[a[i]]=tmpos;
                    vis[tmpos]=true;
                    flag=1;
                    break;///必加
                }
            }
            if(flag==0)
                table[a[i]]=-1;
        }
    }
    for(int i=0;i<N;i++){
        if(i!=0)
            printf(" ");
        if(table[a[i]]==-1)
            printf("-");
        else
            printf("%d",table[a[i]]);
    }
    printf("\n");
    return 0;
}

```

* 把数组```table```去掉了,也还是```超时代码```，
*　得在```for循环```中加一个```break```，否则超时
```
#include <bits/stdc++.h>

using namespace std;

bool is_prime(int n){
    if(n<=1)    return false;
    int sqr=(int)sqrt(n);
    for(int i=2;i<=sqr;i++){
        if(n%i==0)
            return false;
    }
    return true;
}

int a[11111];
bool vis[31111];
int main(){
    int MSize,N;
    scanf("%d%d",&MSize,&N);
    for(int i=0;i<N;i++){
        scanf("%d",a+i);
    }
    while(!is_prime(MSize)){
        MSize++;
    }

    for(int i=0;i<N;i++){
        int tmpos=a[i]%MSize;
        int flag=0;
        if(vis[tmpos]==false){///没有发生冲突
            //table[a[i]]=tmpos;
            flag=1;
            vis[tmpos]=true;
        }
        else{///发生冲突
            for(int j=0;j<MSize;j++){
                tmpos=(a[i]+j*j)%MSize;
                if(vis[tmpos]==false){///没有发生冲突
                    //table[a[i]]=tmpos;
                    vis[tmpos]=true;
                    flag=1;
                    break;///必加
                }
            }
            //if(flag==0)
                //table[a[i]]=-1;
        }
        if(i!=0)
            printf(" ");
        if(flag==0)
            printf("-");
        else
            printf("%d",tmpos);
    }

    printf("\n");
    return 0;
}

```


* AC代码,代码整洁易懂，值得学习

```
#include <bits/stdc++.h>

using namespace std;
int tsize, n;
int table[10010], tmp, step;

bool isprime(int num) {
    if (num == 1) return false;
    for (int i = 2; i * i <= num; i++)
        if (num % i == 0) return false;
    return true;
}

int main() {
    cin >> tsize >> n;
    while (!isprime(tsize))tsize++;
    for (int i = 0; i < n; i++) {
        step = 0;
        cin >> tmp;
        int pos = tmp % tsize;
        while ( table[pos] != 0 && step < tsize) {
            pos = (tmp + step * step) % tsize;
            step++;
        }
        if (i != 0)
            cout << ' ';
        if (table[pos] == 0) {
            table[pos] = 1;
            cout << pos;
        } else {
            cout << '-';
        }
    }
    return 0;
}

```








```
#include <bits/stdc++.h>

using namespace std;

priority_queue<int> pq;

int main(){
    int t;
    scanf("%d",&t);
    while(t--){
        while(!pq.empty())
            pq.pop();
        int n;
        scanf("%d",&n);
        while(n--){
            int tmp;
            scanf("%d",&tmp);
            pq.push(tmp);
        }
        int sum=0;
        if(pq.size()==2){
            sum+=pq.top();
            pq.pop();
            sum+=pq.top();
            pq.pop();
        }
        else
            while(pq.size()>2){
                int top1=pq.top();
                pq.pop();
                int top2=pq.top();
                pq.pop();
                int sum1=top1+top2;
                sum+=sum1;
                pq.push(sum1);
            }

        cout<<sum<<endl;

    }
    return 0;
}

```

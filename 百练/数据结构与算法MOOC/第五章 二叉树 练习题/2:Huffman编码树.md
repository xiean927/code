
* 我的```WA```代码

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

* ```AC```代码
  * 对于优先队列队内元素判断，每次求和，要进行两次判断队列是否为空， 

```
#include <cstdio>
#include <iostream>
#include <queue>
#include <cstring>
using namespace std;

int t,n;
priority_queue<int,vector<int>,greater<int>> q;

int main()
{
	cin >> t;
	while(t--) {
	    cin >> n;
	    while(n--) {
	        int a;
	        cin >> a;
	        q.push(a);
	    }
	    int sum = 0;
	    while(!q.empty()) {
	        int a = q.top();q.pop();
	        if(!q.empty()){
	        	int b = q.top();q.pop();
	        	sum += a+b;
	        	q.push(a+b);
	        }
	    }
	    cout << sum << endl;
	}
	return 0;
}

```

```


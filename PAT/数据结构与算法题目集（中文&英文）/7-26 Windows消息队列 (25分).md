* 得换成```printf&scanf进行输入输出```

```
#include <iostream>
#include <string>
#include <algorithm>
#include <queue>
using namespace std;

struct Node{
	char cmd[15];
	int rank;
    friend bool operator <(Node a,Node b){
		return a.rank>b.rank;
	}
}node;

priority_queue<Node> pq;

int main(){
	int n;
	char cmd1[10];
	int cmd3;
	scanf("%d",&n);
	for(int i=0;i<n;i++){
		cin>>cmd1;
		if(cmd1[0]=='P'){
			scanf("%s%d",node.cmd,&node.rank);
			pq.push(node);
		}
		else{
			if(pq.size()==0)
				printf("EMPTY QUEUE!\n");
			else{
				Node a=pq.top();
				pq.pop();
				printf("%s\n",a.cmd);
			}
		}
	}
	return 0;
}
```

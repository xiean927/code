### 思路
* 类似于2019年秋季甲级考试第一题
* [算法笔记代码](https://blog.csdn.net/qq_34649947/article/details/81208186)
* 超时代码
```


void DFS(int curindex,int curN,int nowK,int facsum){
    if(nowK>K||curN>N)
        return ;
    if(nowK==K&&curN==N){
        if(!flag){
			ans=lujing;
			flag=1;
			ansum=facsum;
		}
		else
		{
			if(ansum<facsum)
			{
				ansum=facsum;
				ans=lujing;
			}
		}
        return ;
    }
    
    lujing.push_back(curindex);
    if(curN+poww[curindex]<=N)
        DFS(curindex,curN+poww[curindex],nowK+1,facsum+curindex);
    lujing.pop_back();
    
    if(curindex-1>=0)
        DFS(curindex-1,curN,nowK,facsum);
}

```


* AC代码
```

#include <bits/stdc++.h>

using namespace std;

int N,K,P,flag,ansum=0;
vector<int> poww,lujing,ans;

bool cmp(){//判断是否可取
	for(int i=0;i<K;i++){
		if(ans[i]<lujing[i])
			return 1;
		else if(ans[i]>lujing[i])
			return 0;
	}
	return 0;
}

void DFS(int curindex,int curN,int nowK,int facsum){
    if(nowK>K||curN>N)
        return ;
    if(nowK==K&&curN==N){
        if(!flag){
			ans=lujing;
			flag=1;
			ansum=facsum;
		}
		else
		{
			if(ansum<facsum)
			{
				ansum=facsum;
				ans=lujing;
			}
		}
        return ;
    }
    if(curindex-1>=0){
        lujing.push_back(curindex);
        if(curN+poww[curindex]<=N)
            DFS(curindex,curN+poww[curindex],nowK+1,facsum+curindex);
        lujing.pop_back();
        DFS(curindex-1,curN,nowK,facsum);
    }
    //if(curindex-1>=0)
    //    DFS(curindex-1,curN,nowK,facsum);
}

int main(){
    scanf("%d%d%d",&N,&K,&P);
    int inum=1;
    flag=0;
    poww.push_back(inum);
    while(pow(inum,P)<=N){
        poww.push_back(pow(inum,P));
        inum++;
    }
    //for(int i=0;i<(int)poww.size();i++)
    //    printf("%d ",poww[i]);
    DFS(poww.size()-1,0,0,0);
	if(!flag)
		printf("Impossible");
	else{
		printf("%d = ",N);
		for(int i=0;i<K;i++){
			printf("%d^%d",ans[i],P);
			if(i!=K-1)
				printf(" + ");
		}
	}
    return 0;
}






```

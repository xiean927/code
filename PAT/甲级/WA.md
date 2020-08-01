### 1021 Deepest Root (25分)

* 改成无前驱结点的方法，出错，更新不了树高

```
#include <bits/stdc++.h>

using namespace std;

const int maxn = 100010;
vector<int> e[maxn];

bool isRoot[maxn],vis[maxn];
int father[maxn];

int findFather(int x){
	int a=x;
	while(x!=father[x]){
		x=father[x];
	}
	while(a!=father[a]){
		int z=a;
		a=father[a];
		father[z]=x;
	}
	return x;
}
void Union(int a,int b){
	int faA=findFather(a);
	int faB=findFather(b);
	if (faA!=faB){
		father[faA]=faB;
	}
}

void init(int n){
	for(int i=1;i<maxn;i++){
		father[i]=i;
        isRoot[i]=false;
        vis[i]=false;
	}
}

int calBlock(int n){
	int Block=0;
	for(int i=1;i<=n;i++){
		isRoot[findFather(i)]=true;
	}
	for(int i=1;i<=n;i++) {
		Block+=isRoot[i];
	}
	return Block;
}

set<int> temp,Ans;
int maxH=0;
void DFS(int u,int Height,int pre){
    if(Height>maxH){///更新最大树高，和最大树高下的叶子节点
        maxH=Height;
        temp.clear();
        temp.insert(u);
    }
    else if(Height==maxH){///更新最大树高下的叶子节点
        temp.insert(u);
    }
    for(int i=0;i<(int)e[u].size();i++){
        if(e[u][i]==pre)///不能回溯
            continue;
        DFS(e[u][i],Height+1,u);///
    }
}

void dfs(int u,int height){
    //cout<<u<<" "<<height<<endl;
    vis[u]=true;
    cout<<u<<" "<<height<<" "<<maxH<<endl;
    if(height>maxH){
        height=maxH;
        temp.clear();
        temp.insert(u);
    }
    else if(height==maxH)
        temp.insert(u);
    for(int i=0;i<(int)e[u].size();i++){
        int v=e[u][i];
        if(vis[v]) continue;
        dfs(v,height+1);
    }
}

int main(){
	int a,b,n;
	scanf("%d",&n);
	init(n);
	for (int i=1;i<n;i++) {
		scanf("%d%d",&a,&b);
		e[a].push_back(b);
		e[b].push_back(a);
		Union(a,b);
	}
	int Block=calBlock(n);
	if (Block!=1)
		printf("Error: %d components",Block);
	else{
        //DFS(1,1,-1);
        dfs(1,1);
        cout<<maxH<<endl;
        Ans=temp;
        set<int>::iterator it=Ans.begin();
        //memset(vis,false,sizeof(vis));
        fill(vis,vis+maxn,false);
        cout<<"--------------"<<endl;
        dfs(*it,1);
        cout<<maxH<<endl;
        //DFS(*it,1,-1);
        for(set<int>::iterator itt=temp.begin();itt!=temp.end();itt++){
            Ans.insert(*itt);
            //cout<<*itt<<" *";
        }
        for(set<int>::iterator itt=Ans.begin();itt!=Ans.end();itt++){
            cout<<*itt<<" *";
        }
        it=Ans.begin();

        printf("\n%d\n",*it);
        it++;
        for(;it!=Ans.end();it++){
            printf("%d\n",*it);
        }
	}
	return 0;
}

```



### ``` 1118 Birds in Forest (25分)```
* 为什么```union_()```函数无需做特殊处理即可合并根？？？



* ```1130 Infix Expression (25分)```与2019年秋季```7-3 Postfix Expression```，不知道在哪里加括号，应该再做一遍2019年秋季（第一题，深度遍历也不会）

## 凉凉题目（看了题解也是毫无思路，反复看题解还是毫无思路）：
### 1049 Counting Ones (30分)
* 

### 1117 Eddington Number (25分)

* http://codeup.cn/problem.php?cid=100000601&pid=0
* http://codeup.cn/problem.php?cid=100000592&pid=1
* http://codeup.cn/problem.php?cid=100000598&pid=0
* https://blog.csdn.net/wchzh2015/article/details/102759736
* https://blog.csdn.net/rhao999/article/details/104049577#comments
* http://codeup.cn/problem.php?cid=100000602&pid=0
* 八皇后问题
  * https://blog.csdn.net/wchzh2015/article/details/102810936
  * https://blog.csdn.net/weirdo_coder/article/details/89005706
* 向量组等价,https://www.baidu.com/baidu?tn=monline_7_dg&ie=utf-8&wd=%E5%90%91%E9%87%8F%E7%BB%84%E7%AD%89%E4%BB%B7%E5%92%8C%E7%BA%BF%E6%80%A7%E7%9B%B8%E5%85%B3%E4%BB%A5%E5%8F%8A%E4%BA%92%E7%9B%B8%E8%A1%A8%E7%A4%BA  

* ch06-6.7 队列的应用得看看







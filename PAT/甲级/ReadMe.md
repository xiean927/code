
### 1013 Battle Over Cities (25分)
* ```DFS```寻找连通块个数

### 1014 Waiting in Line (30分)
* 

### 1018 Public Bike Management (30分)
* ```Dijsktra+DFS```

### 1019 General Palindromic Number (20分)
* 进制转换 + 回文判断

### 1020 Tree Traversals (25分)
* 已知树的中序，后序 ==> 求树的层次遍历

### 1021 Deepest Root (25分)
* 两次遍历结果的并集为所求的根节点集合
* 由于题目给定的是无向图，因此在邻接表中会同时存放两个方向的边，所以在使用DFS/BFS进行树的遍历时，需要记录当前结点的前驱结点，以免出现“走回头路”的情况。
* 处理N==1的特殊数据，当输入1时，应该输出1。
* 邻接矩阵会超时

### 1022 Digital Library (30分)
* ```map<string,set<int> > mpTitle,mpAuthor,mpKey,mpPub,mpYear;```，```title，author，key，publisher，year对应set<int>类型的7位id```
* 如何读取```key```，
```
while(cin>>key){///书的关键字
    mpKey[key].insert(id);
    c=getchar();
    if(c=='\n')
        break;
}
```
### 1025 PAT Ranking (25分)
#### 思路：
* 解决 分考场 下考生成绩排序问题
  * 对于每一个考场，给定```localnumber```(1 To k,k+1 To m,m+1 To n···)， 在这个范围内对```localnumber```进行排序

### 1029 Median (25分)
* 数组直接开到4*10^5,排序即可

### 1030 Travel Plan (30分)
* ```Dijsktra + DFS```
```
void DFS(int v){
    tempath.push_back(v);
    if(v==st){
        int tempcost=0;
        for(int i=tempath.size()-1;i>0;i--){
            int id=tempath[i],nextid=tempath[i-1];
            tempcost+=cost[id][nextid];
        }
        if(mincost>tempcost){
            mincost=tempcost;
            ans=tempath;
        }
        tempath.pop_back();
        return ;
    }
    for(int i=0;i<(int)pre[v].size();i++){
        DFS(pre[v][i]);
    }
    tempath.pop_back();
    return ;
}

```
### 1032 Sharing (25分)

```
struct Node{
    bool flag;
    int address,next_;
    char data;
}node[100000];
```
### 1033 To Fill or Not to Fill (25分)
* 将目的地设置为最后一个地点。未看懂!!!
* 不断寻找所能到达的最远地点，且记录油价是否为最低，根据油价，更新花费和油箱的容量

### 1038 Recover the Smallest Number (30分)
* 排序
```
bool cmp(string a, string b) {
	return a + b < b + a;
}
```
* 去除前导零
```
while (ans.size() != 0 && ans[0] == '0') {
    ans.erase(ans.begin());
}
```
### 1039 Course List for Student (25分)
* 这个用```set```就做不了，得用```hash```，```数据结构与算法题目集（中文&英文）```用```set```可以```A```

### 1040 Longest Symmetric String (25分)
* ```最长公共子序列(LCS)```
```
int ans=1;
for(int i=1;i<(int)line.size();i++){
    dp[i][i]=1;
    if(line[i]==line[i-1]){
        dp[i-1][i]=1;
        ans=2;
    }
}

for(int L=3;L<=(int)line.size();L++){
    for(int i=0;i+L-1<(int)line.size();i++){
        int j=i+L-1;
        if(line[i]==line[j]&&dp[i+1][j-1]==1){
            dp[i][j]=1;
            ans=L;
        }
    }
}
```
### 1043 Is It a Binary Search Tree (25分)
* 判断输入样例是否是前序遍历（输出后序遍历），或前序镜像遍历（输出后序镜像遍历）
 
### 1044 Shopping in Mars (25分)

### 1046 Shortest Distance (20分)
* 环形跑道，计算两点之间最短距离

### 1048 Find Coins (25分)
* ```hash```做法，```特判特例：if (i == m - i && HashTable[i] <= 1) {///如果是同一个数，且出现次数小于等于1```
* ```two pointers```解法
```
void twoPointers(int n,int m){
    int i=0,j=n-1;
    while(i<j){
        if(a[i]+a[j]==m)    break;
        else if(a[i]+a[j]<m)
            i++;
        else
            j--;
    }
    if(i<j)///有解
        printf("%d %d\n",a[i],a[j]);
    else///无解
        printf("No Solution\n");
}
```

### 1051 Pop Sequence (25分)
* 模拟栈

### 1052 Linked List Sorting (25分)
* 首先，要选中有效结点，```特判 无有效结点的情况:if(cnt==0) printf("0 -1\n");```

### 1053 Path of Equal Weight (30分)
* ```DFS``` ，首先要排序，不知为何!!!

### 1055 The World's Richest (25分)
* ```if(book[per[i].age]<100){///每个年龄的人数要小于100 ```

### 1067 Sort with Swap(0, i) (25分)
* 贪心
* 19分超时代码，每次从头找不在本位上的数
```

int main() {
	int n;
	cin >> n;
	int left = n-1,num;

	for (int i = 0; i < n; i++) {
		cin >> num;
		a[num] = i;///num所处的位置是i
		if (num == i && num != 0)///如果除0以外有本位上的数
			left--;///left减1
	}
	//int k = 1;///k存放除0以外当前不在本位的最小的数
	int cnt = 0;///总的交换次数
	while (left > 0) {///只要还有数不在本位上
        ///如果0在本位上，则寻找一个当前不在本位上的数与0交换
		if (a[0] == 0) {
			//while (k < n) {
			int k;
			for(int i=1;i<n;i++)
            if(a[i]!=i){
                k=i;
                break;
            }

            if (a[k] != k) {///找到一个档期啊不在本位上的数
                swap(a[0], a[k]);///将k与0交换位置
                cnt++;///交换次数加1
                //break;
            }
				//k++;///判断k+1是否在本位上
			//}

		}
    ///只要0不在本位上，就将0所在位置的数的当前所处位置与0的位置交换
		while (a[0] != 0) {
			int t = a[0];///0所在位置
			swap(a[t], a[0]);///将0与pos[0]交换，
                            /// a[7]=2,a[0]=7
                            /// a[2]=3,a[0]=2,
                            /// a[3]=0,a[0]=3
                            ///
			cnt++;
			left--;///不在本位上的数的个数减1
		}
	}
	//cout<<left<<endl;
	//for(int i=0;i<n;i++)
       // printf("%d ",a[i]);
	printf("%d\n", cnt);
	return 0;
}
```
* ```AC代码```
```

int main() {
	int n;
	cin >> n;
	int left = n-1,num;

	for (int i = 0; i < n; i++) {
		cin >> num;
		a[num] = i;///num所处的位置是i
		if (num == i && num != 0)///如果除0以外有本位上的数
			left--;///left减1
	}
	int k = 1;///k存放除0以外当前不在本位的最小的数
	int cnt = 0;///总的交换次数
	while (left > 0) {///只要还有数不在本位上
        ///如果0在本位上，则寻找一个当前不在本位上的数与0交换
		if (a[0] == 0) {
			while (k < n) {
			//int k;
			//for(int i=1;i<n;i++)
            //if(a[i]!=i){
            //    k=i;
            //    break;
            //}

                if (a[k] != k) {///找到一个档期啊不在本位上的数
                    swap(a[0], a[k]);///将k与0交换位置
                    cnt++;///交换次数加1
                    break;
                }
                    k++;///判断k+1是否在本位上
                }
            }
    ///只要0不在本位上，就将0所在位置的数的当前所处位置与0的位置交换
		while (a[0] != 0) {
			int t = a[0];///0所在位置
			swap(a[t], a[0]);///将0与pos[0]交换，
                            /// a[7]=2,a[0]=7
                            /// a[2]=3,a[0]=2,
                            /// a[3]=0,a[0]=3
                            ///
			cnt++;
			left--;///不在本位上的数的个数减1
		}
	}
	//cout<<left<<endl;
	//for(int i=0;i<n;i++)
       // printf("%d ",a[i]);
	printf("%d\n", cnt);
	return 0;
}

```



### 1075 PAT Judge (25分)（WA）
* 《算法笔记》给的测试数据我的代码可以通过
```

4 3 8
20 30 40
00001 1 15
00001 3 20
00002 2 0
00002 3 0
00003 1 20
00003 2 15
00004 1 -1
00004 3 -1

```

* [柳诺题解](https://blog.csdn.net/liuchuo/article/details/52226005)，我并没有找出和我的代码的区别

### 1085 Perfect Sequence (25分)
* 二分查找
```
///binarySearch函数在[i+1,n-1]范围内查找第一个大于x的数的位置
int binarySearch(int i,ll x){
    if(a[n-1]<=x)   return n;///如果所有数都不大于x，返回n
    int l=i+1,r=n-1,mid;///在[i+1,n-1]内查找
    while(l<r){
        mid=(r-l)/2+l;
        if(a[mid]<=x){///如果a[mid]<=x,说明第一个大于x的数只可能在mid后面
            l=mid+1;///
        }else{///如果a[mid]>x,说明第一个大于x的数在mid之前(含mid)
            r=mid;
        }
    }
    return l;///由于while结束时l==r,因此返回l或r皆可
}

```
* 二分查找（使用upper_bound函数）
```
int ans=1;
for(int i=0;i<n;i++){
	//在a[i+1]~a[n-1]中查找第一个超过a[i]*p的数,返回其位置给j
	int j=upper_bound(a+i+1,a+n,(ll)a[i]*p);
	ans=max(ans,j-i);	
}
```
* 二维遍历
```
for(int i=0;i<n;i++){
    for(int j=i+1;j<n;j++){
        if((a[j]<=(long long)a[i]*p)){
            res=max(res,j-i+1);
        }
    }
}
```

### 1089 Insert or Merge (25分)
```
//插入排序
void insort(int a[],int b[]){
    int key=0;
    for(int i=2;i<=n;i++){
        sort(a,a+i);//从0~n的插入排序的操作
        if(key){
            printf("Insertion Sort\n");
            printf("%d",a[0]);
            for(int j=1;j<n;j++)
                printf(" %d",a[j]);
            return ;
        }
        if(equal(a,a+n,b))
            key=1;
    }
}

void mesort(int a[],int b[]){
    int key=0;
    for(int i=2;;i*=2){
        for(int j=0;j<n;j+=i){
            sort(a+j,a+(i+j<n?j+i:n));
        }
        if(key){
            printf("Merge Sort\n");
            printf("%d",a[0]);
            for(int j=1;j<n;j++){
                printf(" %d",a[j]);
            }
            return ;
        }
        if(equal(a,a+n,b))
            key=1;
        if(i>n)
            break;
    }
}
```

## 凉凉题目（看了题解也是毫无思路，反复看题解还是毫无思路）：
### 1049 Counting Ones (30分)
* 





















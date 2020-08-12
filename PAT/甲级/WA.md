

### ``` 1118 Birds in Forest (25分)```
* 为什么```union_()```函数无需做特殊处理即可合并根？？？
  * 因为题目未规定要以 序号最小 的那个结点作为根
* ```1114 Family Property (25分)```必须以 序号最小 的作为树根（题目规定了）

### ```1119 Pre- and Post-order Traversals (30分)```
* [图解](https://blog.csdn.net/li1615882553/article/details/88061615)

* ```1130 Infix Expression (25分)```与2019年秋季```7-3 Postfix Expression```，不知道在哪里加括号，应该再做一遍2019年秋季（第一题，深度遍历也不会）

### 1127 ZigZagging on a Tree (30分)
#### 题意
* 给出树的中序遍历和后序遍历
#### 输出
* 打印树的```zigzagging```序列
#### 思路

* 静态结点的建树代码
  * 为什么输入是1~n???
    * 因为在层序遍历时，默认情况下```tree[temp.index][0] != 0```序号等于0，代表孩子结点为空，
    * 如果输入时0~n-1，则最终输出时，会遗漏下标0的元素
```
int tree[35][2];
void create(int &index,int inL,int inR,int postL,int postR){
    if(inL>inR)
        return ;
    index=postR;
    int k=0;
    while(in[k]!=post[postR])
        k++;
    int numLeft=k-inL;
    create(tree[index][0],inL,k-1,postL,postL+numLeft-1);
    create(tree[index][1],k+1,inR,postL+numLeft,postR-1);
}

int main(){
    scanf("%d",&n);
    for(int i=1;i<=n;i++)
        scanf("%d",&in[i]);
    for(int i=1;i<=n;i++)
        scanf("%d",&post[i]);
    create(root,1,n,1,n);
```

* 层序遍历（记录层号）
  * 为什么是记录后序遍历的结点值？？？
```
struct node {
	int index, depth;
};

void bfs() {
	queue<node> q;
	q.push(node{ root,0 });
	while (!q.empty()) {
		node temp = q.front();
		q.pop();
		result[temp.depth].push_back(post[temp.index]);
		if (tree[temp.index][0] != 0)
			q.push(node{ tree[temp.index][0],temp.depth + 1 });
		if (tree[temp.index][1] != 0)
			q.push(node{ tree[temp.index][1],temp.depth + 1 });
	}
}
```

* 输出
```
printf("%d", result[0][0]);
for (int i = 1; i < 35; i++) {
	if (i % 2 == 1) {//奇数层
		for (int j = 0; j < result[i].size(); j++)
			printf(" %d", result[i][j]);
	}
	else {
		for (int j = result[i].size() - 1; j >= 0; j--)
			printf(" %d", result[i][j]);
	}
}
```

### 1151 LCA in a Binary Tree (30分)
* ```测试点2 段错误```


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







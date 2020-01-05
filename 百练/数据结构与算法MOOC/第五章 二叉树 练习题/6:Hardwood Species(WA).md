### 描述
* 求每种字符串在所有字符串的占比

### 思想：
#### 解法一：利用map存储单词项，每次更新value值，最后循环输出；
#### 解法二：构建一个二叉查找树（又叫二叉搜索树/二叉排序树），然后中序遍历。
* 二叉查找树：
  * 它或者是一棵空树，或者是具有下列性质的二叉树：
  * 若它的左子树不空，则左子树上所有结点的值均小于它的根结点的值；
  * 若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值；
  * 它的左、右子树也分别为二叉排序树。

#### 解法三：构建一个字典树（这种方法还没写好）

#### [转自](https://blog.csdn.net/xxiaobaib/article/details/79465222)

* 1,```map<string,int> mp;```
```
#include <bits/stdc++.h>

#define pii pair<string, int>

using namespace std;
char ch[50];
int main ()
{
    map <string,int> mp;
    map<string,int>::iterator it;
    int coun=0;
    while(gets(ch)&&strlen(ch))
    {
        string str(ch);
        it = mp.find(str);
        if( it != mp.end())
            it->second = it->second+1;
        else
            mp.insert(pii(str,1));
        coun++;
    }
    for( it=mp.begin() ; it != mp.end(); ++it){
       cout << it->first;
       printf(" %.4f\n",(it->second)*1.0/coun*100);
    }
    return 0;
}

```

* 2,二叉查找树
```
#include<iostream>
#include<cmath>
#include<cstring>
#include<algorithm>
#include<iomanip>
#include<queue>
#include<stack>
#include<vector>
#include<set>
#include<map>
using namespace std;
char c[35];
double sum=1;
struct Node
{
	char s[35]={0};
	int num;
	Node*l;
	Node*r;
	Node(const char*p)
	{
		strcpy(s,p);
		l=NULL;r=NULL;num=1;
	}
};
Node*root;
void Insert(Node*p)
{
	int Cmp=strcmp(c,p->s);
	if(Cmp==0)
	{
		p->num++;return;
	}
	else if(Cmp<0)///如果c的字典序小于p->s的字典序
	{
		if(p->l!=NULL)
		{
			Insert(p->l);return;
		}
			
		else
		{
			p->l=new Node(c);return;
		}
	}
	else///如果c的字典序大于p->s的字典序
	{
		if(p->r!=NULL)
		{
			Insert(p->r);return;
		}
		else
		{
			p->r=new Node(c);return;
		}
	}
}
void Mid(Node*p)
{
	if(p==NULL)return;
	Mid(p->l);
	cout<<p->s<<" "<<fixed<<setprecision(4)<<(double(p->num))*100/sum<<endl;
	Mid(p->r);
}
int main()
{
	gets(c);
	root=new Node(c);
	while(gets(c))
	{
		sum=sum+1;
		Insert(root);
	}
	Mid(root);
	return 0;
}
```

* 3,字典树
```

```




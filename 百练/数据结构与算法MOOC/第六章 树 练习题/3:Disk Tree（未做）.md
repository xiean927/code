### 描述

* 

### 输入：
* 第一行包含一个整数N（between[1,500]）显示唯一路径总数
* 接下来是N行路径
* 每行文件路径
* 每个路径不超过80个字符
* 每个路径被唯一列出并且包含一定数目的分割符（“\”）

### 输出：
* 以格式化目录树的形式写入到输出文件
* 每一个目录名都被列出在它自己的一行，表明在目录后代中的深度
* 
* 最高等级的目录在他的名字之前没有空格被打印
* 


### [题解](https://blog.csdn.net/m0_37975647/article/details/77539948)


```
#include<bits/stdc++.h>

using namespace std;

map<string,int>M[20005];
char c[85];
int Dic[45];
int TotalDicnum=0;

void Pre(int dic,int offset)
{
	for(map<string,int>::iterator it=M[dic].begin();it!=M[dic].end();++it)
	{
		for(int i=0;i<offset;++i)cout<<" ";
		cout<<(it->first).c_str()<<endl;
		Pre(it->second,offset+1);
	}
}

int main()
{
	int n;
	cin>>n;
	while(n--)
	{
		scanf("%s",c);
		Dic[0]=0;
		int Dicnum=1;
		int len=strlen(c);
		for(int i=0;i<len;++i)
		{
			if(c[i]=='\\')
			{
				c[i]=0;
				Dic[Dicnum++]=i+1;///每一个文件名的位置
			}
		}
		int dic=0;
		for(int i=0;i<Dicnum;++i)
		{
			string s=c+Dic[i];///记录每一个文件名
			if(!M[dic].count(s))///如果不存在
			{
				M[dic][s]=(++TotalDicnum);///
			}
			dic=M[dic][s];
		}
	}
	Pre(0,0);
	return 0;
}


```

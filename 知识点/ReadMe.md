### 1，关于输入形如（没有说明输入的数字个数，直接输入两排数）
``` 
9 5 32 67
9 32 67 5
```
#### 读取方式
```
#include <bits/stdc++.h>

using namespace std;

int in[65536];
int post[65536];
int n;

int main()
{
	char c;
	c = getchar();
	n = 0;
	while (c != '\n')
	{
		if (c != ' ')
		{
			ungetc(c, stdin);
			cin >> in[n];
			n++;
		}
		c = getchar();
	}
	for (int i = 0; i < n; i++)
	{
		cin >> post[i];
	}

	for(int i=0;i<n;i++){
        cout<<"in "<<in[i]<<" post "<<post[i]<<endl;
	}
    return 0;
}

Out:
9 5 32 67
9 32 67 5
in 9 post 9
in 5 post 32
in 32 post 67
in 67 post 5

```
#### [对ungetc将字符输入回stdin的一点理解](https://blog.csdn.net/qq_40680653/article/details/79951386)
* 1.传回的字符是以压栈形式 后入先出
* 传入多个字符如'131'，也是读取末尾的字符1
* 2.如果stdin没有字符 传回后会开启一个缓冲区 大小为1 必须在被getchar后才能下次ungetc 否则传入失败
* 但当stdin本来就有字符未读取完时 如getchar留有多个字符未被读取时 缓冲区大小将是getchar时输入的大小 这时候可以多次ungetc直到缓冲区被填满为止

### 3，关于```strtok```
```
/* strtok example */
#include <stdio.h>
#include <string.h>

int main ()
{
  char str[] ="This is a sample string,just testing.";
  char * pch;
  printf ("Splitting string \"%s\" in tokens:\n",str);
  pch = strtok (str," ");
  while (pch != NULL)
  {
    printf ("%s\n",pch);
    pch = strtok (NULL, " ,.");
  }
  return 0;
}

Output:
Splitting string "This is a sample string,just testing." in tokens:
This
is
a
sample
string
just
testing 

```

### 3,```string,char*,char[]```相互转换
* （1）,```string```转```const char*```
```
string line;
cin>>line;
char* pc=new char[line.size()+1];
strcpy(pc,line.c_str());
```
* （2）,```char*,char[]```转```string```，直接赋值就好
* （3）,```string```转```char*```
```
string s ="abc";
char* c;
const int len = s.length();
c =new char[len+1];
strcpy(c,s.c_str());
```









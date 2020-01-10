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

### 4,RuntimeError常见出错的原因可能有以下几种：
* 1、数组开得太小了，导致访问到了不该访问的内存区域
* 2、发生除零错误
* 3、大数组定义在函数内,导致程序栈区耗尽
* 4、指针用错了，导致访问到不该访问的内存区域
* 5、还有可能是程序抛出了未接收的异常


### 5,fixed 和setprecision()的用法

* 使用setprecision(n)可控制输出流显示浮点数的数字个数。C++默认的流输出数值有效位是6。
* 如果setprecision(n)与setiosflags(ios::fixed)合用，可以控制小数点右边的数字个数。setiosflags(ios::fixed)是用定点方式表示实数。
* 如果与setiosnags(ios::scientific)合用， 可以控制指数表示法的小数位数。setiosflags(ios::scientific)是用指数方式表示实数。

```
#include <iostream>
#include <iomanip> //要用到格式控制符

using namespace std;

int main(){
    double amount = 22.0/7;
    cout <<amount <<endl;
    cout <<setprecision(0) <<amount <<endl
    <<setprecision(1) <<amount <<endl
    <<setprecision(2) <<amount <<endl
    <<setprecision(3) <<amount <<endl
    <<setprecision(4) <<amount <<endl;

    cout <<setiosflags(ios::fixed);
    cout <<setprecision(8) <<amount <<endl;

    cout <<setiosflags(ios::scientific)
    <<amount <<endl;
    cout <<setprecision(6); //重新设置成原默认设置

    return 0;
}

Out:
3.14286
3
3
3.1
3.14
3.143
3.14285714
0xc.9249249249248p-2


```
















## [3.3数据结构之栈](http://noi.openjudge.cn/ch0303)

### 1696:逆波兰表达式
* 应该叫波兰表达式，也就是前缀表达式
* [前缀，后缀表达式求值，应该多看几遍](https://www.cnblogs.com/zzliu/p/10801113.html)
#### 前缀表达式求法，和后缀表达式求法，有三点不同：
* 0,遍历方向不同：前缀（从右至左），后缀（从左至右）
* 1,在于a,b的赋值上不同，
```
for(int i=0;i<len;i++){
   if(sline[i]==42||sline[i]==43||sline[i]==45||sline[i]==47){///遇到运算符，弹出 数字栈 的栈顶和次栈顶元素
       double b=number.top();number.pop();
       double a=number.top();number.pop();
       double ans;
```
* 2,何时压入栈的判断不同 
```
else if(sline[i-1]>='0'&&sline[i-1]<='9'&&sline[i]==' ') ///只有数字之后的空格才需要把字符串转换成数字
```

```
#include<bits/stdc++.h>

using namespace std;

const int infi=-98765432;

char k[1001],sline[1001];
int l=-1;

stack<double> number;///数字栈
stack<char> op;///运算符栈

void reverses(char *s){
    int len=strlen(s);
    char *p=NULL;
    strcpy(p,s);
    for(int i=len-1;i>=0;i--)
        s[len-1-i]=p[i];
}

int main()
{
     gets(sline);
     //for(int i=1;i<=1000;i++) num[i]=infi;//num数组赋极值
     int len=strlen(sline);
     for(int i=len-1;i>=0;i--){
        if(sline[i]==42||sline[i]==43||sline[i]==45||sline[i]==47){///遇到运算符，弹出 数字栈 的栈顶和次栈顶元素
            double a=number.top();number.pop();
            double b=number.top();number.pop();
            double ans;

            switch(sline[i]){
                case '+':ans=a+b;break;
                case '-':ans=a-b;break;
                case '*':ans=a*b;break;
                case '/':ans=a/b;break;
            }
            //cout<<a<<" "<<b<<" "<<ans<<endl;
            number.push(ans);
        }
        else if((sline[i]>='0'&&sline[i]<='9')||sline[i]==46) k[++l]=sline[i];///数字或者小数点
        else if(sline[i+1]>='0'&&sline[i+1]<='9'&&sline[i]==' ') ///只有数字之后的空格才需要把字符串转换成数字
        {                                 ///也就是说，遇到空格就停止读取数字，把输入入栈
            ///k是倒着赋值的得翻转一下,i
            //cout<<k<<endl;
            //reverses(k);
            int lenk=strlen(k);
            reverse(k,k+lenk);
            //cout<<k<<endl;
            number.push(atof(k));
            memset(k,'\0',sizeof(k));
            l=-1;///l从-1开始，因为上面k[++l]=s[i]，数组k从0开始赋值
        }
     }

     printf("%f\n",number.top());
     return 0;
}

```
* 递归写法
```
#include<iostream>
#include <cstring>
#include <cstdlib>
using namespace std;
double exp()
{
    char n[100];
    cin >> n;//依次输入即可，中间加空格
    switch (n[0])
    {
    case'+': return exp() + exp();
    case'-': return exp() - exp();
    case'*': return exp() * exp();
    case'/': return exp() / exp();
    default: return atof(n);//char转换为浮点数
        break;
    }
}

int main()
{
    cout<<exp();//例如输入+ 5 3，第一个为+，所以进入exp(),输入的数为5，由于不是‘+-*/’，所以返回int型的5，前面+号右边的输入为3，道理如上，所以返回int 3，一起返回，到5+3=8；
    return 0;
}
```


### 逆波兰表达式求值
* 遇到问题：
```
样例1：
9 3 1 - 3 * + 10 2 / +
3 1 2
2 3 6
9 6 15
10 2 5
15 5 20
20.000000
样例2：
1 2 3 + 4 * + 5 -
2 3 5
5 4 20
1 20 21
21 5 16
16.000000

其中每个样例的最后一行是答案,第一行是表达式，其余行是过程量
```
```
#include<bits/stdc++.h>

using namespace std;

char k[1001],sline[1001];///k数组临时记录 数字，sline数组是输入字符串
int l=-1;

stack<double> number;///数字栈
stack<char> op;///运算符栈

int main()
{
     gets(sline);
     //for(int i=1;i<=1000;i++) num[i]=infi;//num数组赋极值
     int len=strlen(sline);
     for(int i=0;i<len;i++){
        if(sline[i]==42||sline[i]==43||sline[i]==45||sline[i]==47){///遇到运算符，弹出 数字栈 的栈顶和次栈顶元素
            double b=number.top();number.pop();
            double a=number.top();number.pop();
            double ans;

            switch(sline[i]){
                case '+':ans=a+b;break;
                case '-':ans=a-b;break;
                case '*':ans=a*b;break;
                case '/':ans=a/b;break;
            }
            //cout<<a<<" "<<b<<" "<<ans<<endl;
            number.push(ans);
        }
        else if((sline[i]>='0'&&sline[i]<='9')||sline[i]==46) k[++l]=sline[i];///数字或者小数点
        else if(sline[i-1]>='0'&&sline[i-1]<='9'&&sline[i]==' ') ///只有数字之后的空格才需要把字符串转换成数字
        {                                 ///也就是说，遇到空格就停止读取数字，把输入入栈
            ///i肯定小于len-1,所以不用加i<len-1
            number.push(atof(k));
            memset(k,'\0',sizeof(k));
            l=-1;///l从-1开始，因为上面k[++l]=s[i]，数组k从0开始赋值
        }
     }

     printf("%f\n",number.top());
     return 0;
}
```

### 6263:布尔表达式

* 不含括号的布尔表达式匹配（```Output Limit Exceeded```）
  * 暴力模拟，分为带感叹号，和不带感叹号，记录```| &```标志位
```
#include <bits/stdc++.h>

using namespace std;

string line;

int main(){
    ///V&V
    bool flag,preflag,commaflag,ttflag;
    char tflag;

    while(true){
        getline(cin,line);
        ///先考虑无括号的情况
        ///V&V
        ///加上 !
        ttflag=true;
        commaflag=false;
        for(int i=0;i<(int)line.size();i++){
            if(line[i]=='|'||line[i]=='&'){
                tflag=line[i];
                ttflag=false;///表示这个 符号未用过
            }
            else if(line[i]=='V'||line[i]=='F'){
                if(commaflag==false){///没有感叹号
                    if(ttflag==false){///前一个已经读取
                        if(tflag=='|'){
                            if(line[i]=='V')
                                flag=true;
                            else///line[i]=='F'
                                flag=0||preflag;
                        }
                        else{///tflag=&
                            if(line[i]=='V')
                                flag=1&&preflag;
                            else///line[i]=='F'
                                flag=0;
                        }
                        ttflag=true;
                    }
                    else{///ttflag=true，前一个未读取
                        if(line[i]=='V')
                            preflag=1;
                        else
                            preflag=0;
                    }
                }
                else{///有感叹号 形如F|!V
                    if(ttflag==false){///前一个已经读取
                        if(tflag=='|'){
                            if(line[i]=='V')
                                flag=0||preflag;
                            else///line[i]=='F'
                                flag=1;
                        }
                        else{///tflag=&
                            if(line[i]=='V')
                                flag=0;
                            else///line[i]=='F'
                                flag=1&&preflag;
                        }
                        ttflag=true;
                    }
                    else{///ttflag=true，前一个未读取
                        if(line[i]=='V')
                            preflag=1;
                        else
                            preflag=0;
                        preflag=!preflag;
                    }
                    commaflag=false;
                }
            }
            else if(line[i]=='!'){
                commaflag=true;
            }
        }
        cout<<flag<<endl;
    }
    return 0;
}

```

* [转自CSDN](https://blog.csdn.net/INCINCIBLE/article/details/51151222?locationNum=5&fps=1#)
  * ```queue< char > s; ```的作用：就是记录前缀表达式（先进先出特性）
```
#include<iostream>
#include<cstdio>
#include<algorithm>
#include<queue>
#include<stack>
#include<cstring>
using namespace std;
char calculate(char x, char y,char oper ){ // 计算 x oper y
	bool a=(x=='V'),b=(y=='V'),ans;
	if(oper=='|')ans=(a||b);
	else if(oper=='&')ans=(a&&b);
	return ans?'V':'F';
}
char reverse(char x){
	if(x=='V')return 'F';
	return 'V';
}
int main(){
	string in;
	int i,j,len;

	while(getline(cin,in)){
		stack< char > Oper,num; //oper保存运算符，num保存运算结果
		queue< char > s;  	//	s就是前缀表达式
		len=in.length();
		i=len;
		in=" "+in;
		while(i>0){  // 从右往左，中缀表达式转 前缀表达式
			if(in[i]==' '){
				i--;continue;
			}
			else if(isalpha(in[i]))
                s.push(in[i--]);
			else if(in[i]=='!')  	//最高级的运算，直接进入表达式
				s.push(in[i--]);
			else{
				if(in[i]=='&'||in[i]=='|'||in[i]==')')  //低级运算，进栈
                    Oper.push(in[i--]);
				else if(in[i]=='('){  //一个括号结束，弹出中间的所有运算符
					while(Oper.top()!=')'){
						s.push(Oper.top());
						Oper.pop();
					}
					Oper.pop();i--;
				}
			}
		}
        while(!Oper.empty())  	//栈中剩下的运算符
            s.push(Oper.top()),Oper.pop();
        while(!s.empty()){   	//计算前缀表达式
            char ch=s.front();s.pop();
            if(isalpha(ch))
                num.push(ch);
            else
                Oper.push(ch);
            if(!num.empty()&&!Oper.empty()&&Oper.top()=='!'){  //单目运算符‘！’；
                char x=num.top();
                num.pop();Oper.pop();
                num.push(reverse(x));
            }
            else if(num.size()>=2&&!Oper.empty()){  	//双目运算符
                char oper=Oper.top(),x,y;
                Oper.pop();
                x=num.top();num.pop();
                y=num.top();num.pop();
                num.push(calculate(x,y,oper));
            }
        }
        cout<<num.top()<<endl;
    }
    return 0;
}
```





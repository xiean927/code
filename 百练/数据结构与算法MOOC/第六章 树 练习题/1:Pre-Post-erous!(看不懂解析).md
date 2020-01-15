

* [1有图](https://blog.csdn.net/ditian1027/article/details/21132583)
* [解析2](https://blog.csdn.net/LuRiCheng/article/details/52895100)
* 该题解的代码

```
#include <bits/stdc++.h>

using namespace std;

const int maxn=30;
char pre[maxn],post[maxn];

vector<int> branch_vec;

///计算n!
int factorial(int n){
    int res=1;
    if(n==0)    return 1;
    else{
        for(int i=1;i<=n;i++)   res*=i;
        return res;
    }
}

///计算C(n,m)=A(n,m)/A(m,m)
int calc_C(int n,int m){
    unsigned int tmp=1;
    for(int i=0;i<m;++i,--n)
        tmp*=n;

    return (tmp/(factorial(m)));
}

void branch_count(int preL,int preR,int postL,int postR){
    int a,b,len,branch=0;
    
    if(preL==preR&&postL==postR)    return ;
    else{
        a=preL+1;
        b=postL;
        len=0;
        
        while(b<postR){
            while((pre[a]!=post[b+len])&&(b+len<postR)) ++len;
            ++branch;
            branch_count(a,a+len,b,b+len);
            
            a=a+len+1;
            b=b+len+1;
            len=0;
        }
        
        branch_vec.push_back(branch);
    }
}



int main(){

    return 0;
}



```

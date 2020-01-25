## 等着复习数据结构完再看看

## [3.2数据结构之指针和链表](http://noi.openjudge.cn/ch0302/)

### 1748:约瑟夫问题

* [CSDN解法](https://blog.csdn.net/wuzhenzi5193/article/details/80335201)
* ``` Runtime Error ```
```
#include <bits/stdc++.h>

using namespace std;

typedef int ElementType;
typedef struct Node *PtrToNode;
struct Node {
    ElementType Data;
    ElementType flag;///false相当于未出圈
    PtrToNode   Next;
};
typedef PtrToNode List;
int len,mlen;///链表节点数

List Read();
void Print( List L );
void Process(List L);

int main()
{
    List L1,L2;
    while(scanf("%d%d",&len,&mlen)){
        if(len==0&&mlen==0)
            break;
        if(mlen>len)
            mlen=mlen%len;
        L1 = Read();
        L2 = L1;///L2做测试
        //Print(L2);
        Process(L2);
    }
    return 0;
}

///尾插法
List Read(){
    int lentt;
    int num=1;///结点值
    PtrToNode listt=NULL,lastt=NULL,nodet;
    lentt=len;
    if(lentt==0)  return NULL;

    //scanf("%d",&num);
    listt=(PtrToNode)malloc(sizeof(struct Node));
    listt->Data=num;
    listt->Next=NULL;
    listt->flag=false;
    lastt=listt;
    lentt--;
    while(lentt--){
        //scanf("%d",&num);
        num++;
        nodet=(PtrToNode)malloc(sizeof(struct Node));
        nodet->Data=num;
        nodet->Next=NULL;
        nodet->flag=false;
        lastt->Next=nodet;
        lastt=nodet;
    }
    //printf("---%d--\n",nodet->Data);
    //cout<<"---"<<nodet->Next<<"---"<<endl;
    nodet->Next=listt;///形成循环链表
    return listt;
}

void Print(List L){
    int lent=len;
    if(L==NULL) return ;
    printf("%d",L->Data);
    L=L->Next;
    lent--;
    while(lent--){
        printf(" %d",L->Data);
        L=L->Next;
    }
    putchar('\n');
}

void Process(List L){

    int cnt=1,num=0,nlen=0;///num记录未出圈数
    List st=L,tmp;///记录链表起点

    while(L!=NULL){
        tmp=st,num=0,nlen=len;
        while(nlen--){
            if(tmp->flag==false)    num++;
            tmp=tmp->Next;
        }
        //cout<<"num:"<<num<<endl;
        if(num==1)///如果只有一个未出圈，弹出即可
            break;
        if(L->flag==false){
            //L->flag=true;
            if(cnt==mlen)  {
                L->flag=true;
                cnt=0;
            }
            cnt++;
        }
        L=L->Next;
    }

    ///记录结果
    nlen=len;
    while(nlen--){
        if(st->flag==false)    num=st->Data;
        st=st->Next;
    }

    cout<<num<<endl;
}

```

### 6378:删除数组中的元素（链表）

* [AC代码](https://blog.csdn.net/sdau_fangshifeng/article/details/79905616)
* ```Presentation Error 7分```

```
#include <bits/stdc++.h>

using namespace std;

typedef int ElementType;
typedef struct Node *PtrToNode;
struct Node {
    ElementType Data;
    ElementType flag;///false相当于未出圈
    PtrToNode   Next;
};
typedef PtrToNode List;
int len,mlen;///链表节点数

List Read();
void Print( List L );
void Process(List L);
void Delete(List L);

int main()
{
    List L1,L2;
    scanf("%d",&len);
    L1 = Read();
    //L2 = L1;///L2做测试
    //Print(L2);
    Delete(L1);
    //Print(L1);
    return 0;
}

///尾插法
List Read(){
    int lentt;
    int num=1;///结点值
    PtrToNode listt=NULL,lastt=NULL,nodet;
    lentt=len;
    if(lentt==0)  return NULL;

    scanf("%d",&num);
    //listt=(PtrToNode)malloc(sizeof(struct Node));
    listt=new Node;
    listt->Data=num;
    listt->Next=NULL;
    listt->flag=false;
    lastt=listt;
    lentt--;
    while(lentt--){
        scanf("%d",&num);
        //num++;
        //nodet=(PtrToNode)malloc(sizeof(struct Node));
        nodet=new Node;
        nodet->Data=num;
        nodet->Next=NULL;
        nodet->flag=false;
        lastt->Next=nodet;
        lastt=nodet;
    }
    //printf("---%d--\n",nodet->Data);
    //cout<<"---"<<nodet->Next<<"---"<<endl;
    //nodet->Next=listt;///形成循环链表
    return listt;
}

void Print(List L){
    int lent=len;
    if(L==NULL) return ;
    printf("%d",L->Data);
    L=L->Next;
    lent--;
    while(lent--){
        printf(" %d",L->Data);
        L=L->Next;
    }
    putchar('\n');
}

List Delete(List L){
    int deletet;
    List st=L,resL;
    scanf("%d",&deletet);
    if(st->Data!=deletet)
        //printf("%d",st->Data);
        resL
    st=st->Next;
    while(st){
        if(st->Data!=deletet)
            printf(" %d",st->Data);
        st=st->Next;
    }
}

/// Wrong Answer 7分
void Delete(List L){
    int deletet;
    List st=L,resL;
    scanf("%d",&deletet);
/*
0 1 0 3
删除0
st
L=1
st=st->Next;
*/
    while(st){///首地址
        if(st->Data==deletet)///如果是要删除的结点
            if(st==L)///更新首地址
                L=st->Next;
            else///删除，跳过结点st
                resL->Next=st->Next;
        else///resL为中间链表，进行对List L链表的Next域修改
            resL=st;
        st=st->Next;///指向下一个结点
    }
}


```

### 6379:统计学生信息（使用动态链表完成）
* ```STL 的 list```

```
#include<iostream>
#include<list>
using namespace std;

struct L{
	string number;
	string name;
	char sex;
	int age;
	float score;
	string address;
};

int main()
{
	list <L> a;
	L b;
	while(true)
	{
		cin>>b.number;
		if(b.number=="end")
			break;
		cin>>b.name>>b.sex>>b.age>>b.score>>b.address;
		a.push_back(b); 
	}
	list <L> :: iterator it=a.end();
	it--;
	do
	{
		cout<<(*it).number<<" "<<(*it).name<<" "<<(*it).sex<<" "<<(*it).age<<" "<<(*it).score<<" "<<(*it).address<<"\n";
	}while(it--!=a.begin());
		
	return 0;
}

```




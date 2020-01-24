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
    listt=(PtrToNode)malloc(sizeof(struct Node));
    listt->Data=num;
    listt->Next=NULL;
    listt->flag=false;
    lastt=listt;
    lentt--;
    while(lentt--){
        scanf("%d",&num);
        //num++;
        nodet=(PtrToNode)malloc(sizeof(struct Node));
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

```

### 6379:统计学生信息（使用动态链表完成）


```
#include <bits/stdc++.h>

using namespace std;

typedef struct Node *PtrToNode;
struct Node {
    char number[20],name[40],sex[2],address[40];
    int score;
    PtrToNode Next,Prev;
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
    //lentt=len;
    //if(lentt==0)  return NULL;

    //scanf("%d",&num);
    
    listt=(PtrToNode)malloc(sizeof(struct Node));
    listt->Data=num;
    listt->Next=NULL;
    listt->flag=false;
    lastt=listt;
    lentt--;
    while(lentt--){
        scanf("%d",&num);
        //num++;
        nodet=(PtrToNode)malloc(sizeof(struct Node));
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


```




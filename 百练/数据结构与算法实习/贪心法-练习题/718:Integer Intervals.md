### 思路： 
#### 一，贪心算法

* 先对所有区间按末端点排序
* 取第i个区间的最后两个元素Selem和Eelem
* 若第i+1个区间包含了这两个元素，则跳到下一个区间所取的元素个数+0
* 若第i+1个区间只包含了这两个元素中的一个（由于有序，所以必定是包含Eelem），则取第i+1个区间的最后一个元素，所取的元素个数+1。为了方便下一区间的比较，更新Selem和Eelem的值，使他们为当前V集合中最后的两个元素。
* 若第i+1个区间没有包含这两个元素，则第i+1个区间的最后两个元素，所取的元素个数+2。为了方便下一区间的比较，更新Selem和Eelem的值，使他们为当前V集合中最后的两个元素。
* Selem初始化为第一个区间的最后倒数第2个元素
* Eelem初始化为第一个区间的最后的元素
* 所取的元素个数初始化为2 (就是Selem和Eelem)

#### [二，差分约束,没看懂](https://blog.csdn.net/lyy289065406/article/details/6648679)



```
#include <bits/stdc++.h>

using namespace std;

struct Node{
    int st,ed;
}node[10010];

bool cmp(struct Node &a,struct Node &b){
    return a.ed<b.ed;
}

int main()
{
    int n;
    scanf("%d",&n);
    for(int i=0;i<n;i++)    scanf("%d%d",&node[i].st,&node[i].ed);

    sort(node,node+n,cmp);

    set<int> st;
    int cnt;
    st.insert(node[0].ed-1);///
    st.insert(node[0].ed);///取第i个区间的最后两个元素Selem和Eelem
    for(int i=1;i<n;i++){

        cnt=0;
        set<int>::iterator it;
        for(it=st.begin();it!=st.end();it++)
            if((*it)>=node[i].st&&(*it)<=node[i].ed)    cnt++;

        if(cnt==2)///若第i+1个区间包含了这两个元素，则跳到下一个区间所取的元素个数+0
            continue;
        else if(cnt==1)///若第i+1个区间只包含了这两个元素中的一个（由于有序，所以必定是包含Eelem），
            st.insert(node[i].ed);
        else if(cnt==0){
            st.insert(node[i].ed);
            st.insert(node[i].ed-1);
        }


    }

    cout<<st.size()<<endl;

    return 0;
}


```

### 描述：
* 背景：
* 在计算机科学中，二叉树是一种普遍的数据结构。在这个问题中我们将看到一棵确定的二叉树其中每个结点包含一对整数。
* 树的结构像这样：
  * 根包含一对（1,1）
  * 如果结点包含（a,b）然后它的左子树包含(a+b,b)并且它的右子树包含(a,a+b)
### 问题：
* 给出如上述描述的一些二叉树的结点，假定你从根走到被给节点的最短路。
* 你能找出你多久到达左子树还是右子树吗？


### 思想：
* ```l r```,分别左子树，右子树的记录
* ```multi```,为什么是```a/b 或 b/a```，因为要累加，所以要累乘，累减

```
#include <bits/stdc++.h>

using namespace std;

int main(){
    int n;
    int a,b,l,r,multi;
    scanf("%d",&n);
    for (int i = 0; i < n; ++i){
        scanf("%d%d",&a,&b);
        l=r=0;
        while(1){
            if(a==1&&b==1)  break;
            if(a==1){r+=b-1;break;}
            if(b==1){l+=a-1;break;}
            if(a>b){
                multi=a/b;
                l+=multi;
                a-=multi*b;
            }
            else{
                multi=b/a;
                r+=multi;
                b-=multi*a;
            }
        }
        printf("Scenario #%d:\n%d %d\n\n",i+1,l,r);
    }
    return 0;
}


```







```
#include <bits/stdc++.h>

using namespace std;

vector<int> vec[10010];///假设最多有10000个节点
int tree[10010][2];
int funode[10010];
bool vis[10010];

int maxh;
int getHeight1(int root){
    if(vec[root].size()==0)
        return 0;
    for(int i=0;i<(int)vec[root].size();i++)
        maxh=max(getHeight1(vec[root][i])+1,maxh);
    return maxh;
}

int getHeight2(int root){
    ///左右子树均不存在
    if(tree[root][0]==-1&&tree[root][1]==-1)
        return 0;
    int lh,rh;
    if(tree[root][0]!=-1)
        lh=getHeight2(tree[root][0])+1;
    if(tree[root][1]!=-1)
        rh=getHeight2(tree[root][1])+1;
    return max(lh,rh);
}

int main(){
    string line;

    int index=1;
    while(cin>>line,line!="#"){
        //cout<<line<<endl;
        int curnode=0,newnode=1;
        for(int i=0;i<10010;i++)
            vec[i].clear();
        memset(funode,-1,sizeof(funode));
        memset(vis,false,sizeof(vis));
        memset(tree,-1,sizeof(tree));
        for(int i=0;i<(int)line.size();i++){
            if(line[i]=='d'){///下沉
                vec[curnode].push_back(newnode);
                //funode=curnode;
                funode[newnode]=curnode;///记录父节点
                curnode=newnode;///更新当前结点
                newnode++;///生成新节点
            }
            else{///上升
                curnode=funode[curnode];///回溯父节点
            }
        }

        maxh=0;
        int oldh=getHeight1(0);
        //cout<<newnode<<" "<<curnode<<endl;
        //6 0
        //cout<<oldh<<endl;



/*
1 2 5
0
3 4
0
0
0
0
*/
        for(int i=0;i<newnode;i++){
            if(vec[i].size()>0){///左孩子
                tree[i][0]=vec[i][0];
                vis[vec[i][0]]=true;///设置已经访问过
            }
            if(funode[i]!=-1){
                int fu=funode[i];///父节点
                if(vec[fu].size()>1){///右兄弟
                    for(int j=0;j<(int)vec[fu].size();j++){
                        if(vis[vec[fu][j]]==false&&i!=vec[fu][j]){///兄弟不能已访问过，兄弟不能自己
                            tree[i][1]=vec[fu][j];///
                            vis[vec[fu][j]]=true;
                            break;
                        }
                    }
                    //tree[i][1]=vec[fu][1];
                }
            }
        }

        int curh=getHeight2(0);

        //cout<<curh<<endl;


        cout<<"Tree "<<index++<<": "<<oldh<<" => "<<curh<<endl;

        //最后一步：获得两个数组tree,vec的高度

        /*
        for(int i=0;i<newnode;i++){
            cout<<"结点"<<i<<"的左孩子:"<<tree[i][0]<<" 右兄弟:"<<tree[i][1]<<endl;
        }

        for(int i=0;i<6;i++){
            if((int)vec[i].size()==0){
                printf("0\n");
                continue;
            }
            for(int j=0;j<(int)vec[i].size();j++)
                printf("%d ",vec[i][j]);
            printf("\n");
        }
        */


    }
    return 0;
}
```


* [AC代码](https://blog.csdn.net/weixin_40116174/article/details/86755883)
  * 也还不是很懂 
```
#include <iostream>
#include <stack>

using namespace std;

int feature[20010] = {1,}, n;///feature是深度的意思
char str[20010];

void str2tree(){
    int d_tree=1, d_binTree=1;
    stack<int> mem({0});
    for (int i = 1; str[i]; ++i) {
        if (str[i] == 'd') {
            mem.push(i);
            if (str[i - 1] == 'd') feature[i] = feature[i - 1] + 1;
            else feature[i] = feature[feature[i - 1]] + 1;
            if (d_binTree < feature[i]) d_binTree = feature[i];
            if (d_tree < mem.size()) d_tree = mem.size();///转换之前的树高
        } else {
            feature[i] = mem.top();
            mem.pop();
        }
    }
    printf("Tree %d: %d => %d\n", ++n, d_tree, d_binTree);
}

int main() {
    while (scanf("%s", str), *str != '#') str2tree();
}
```



* 没写完,


```
#include <bits/stdc++.h>

using namespace std;

vector<int> vec[10010];///假设最多有10000个节点
int tree[10010][2];
int funode[10010];
bool vis[10010];
int main(){
    string line;

    while(cin>>line,line!="#"){
        //cout<<line<<endl;
        int curnode=0,newnode=1;
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

        ///最后一步：获得两个数组tree,vec的高度
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

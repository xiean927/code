### 6377:生日相同 2.0

```
#include <bits/stdc++.h>

using namespace std;

struct Student{
    string name;
    int month,day;
}stu[200];
int book[20][40];///记录相同月日下的学生人数
vector<string> res[20][40];///记录相同月日下的学生姓名
int n;

///对生日相同的名字，按名字从短到长按序输出，长度相同的按字典序输出
bool cmp(string &a,string &b){
    if(a.size()!=b.size())
        return a.size()<b.size();
    else
        return a<b;
}

int main(){
    int n;
    bool flag=false;
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        cin>>stu[i].name>>stu[i].month>>stu[i].day;


    for(int i=0;i<n;i++)
        book[stu[i].month][stu[i].day]++;///记录相同月日下的学生人数

    for(int i=0;i<n;i++)///记录相同月日下的学生姓名
    if(book[stu[i].month][stu[i].day]>=2)   //stu[i].flag=true;
        res[stu[i].month][stu[i].day].push_back(stu[i].name);

    //sort(stu,stu+n,cmp);

///输出
    for(int i=0;i<20;i++)
        for(int j=0;j<40;j++)
            if(book[i][j]>=2){
                flag=true;
                sort(res[i][j].begin(),res[i][j].end(),cmp);
                printf("%d %d",i,j);
                for(int k=0;k<(int)res[i][j].size();k++)
                    cout<<" "<<res[i][j][k];
                cout<<endl;
            }
    if(flag==false||n==1){
        printf("None\n");
        return 0;
    }
    return 0;
}
```

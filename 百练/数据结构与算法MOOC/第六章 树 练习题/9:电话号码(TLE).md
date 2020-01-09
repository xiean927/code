


#### Time Limit Exceeded
* 就是直接开数组做的,这题肯定是字典树

```
#include <bits/stdc++.h>

using namespace std;

bool cmp(string &a,string &b){
    return a.size()<b.size();
}

int main(){
    int t;
    scanf("%d",&t);
    while(t--){
        int n;
        bool flag=true;
        vector<string> vec;
        scanf("%d",&n);
        while(n--){
            string tmp;
            cin>>tmp;
            vec.push_back(tmp);
        }
        sort(vec.begin(),vec.end(),cmp);
        for(int i=0;i<(int)vec.size();i++)
            //cout<<vec[i]<<endl;
            for(int j=i+1;j<(int)vec.size();j++){
                if(vec[j].find(vec[i])!=string::npos)
                    flag=false;
            }
        if(flag==false)
            printf("NO\n");
        else
            printf("YES\n");
    }
    return 0;
}

```



```
#include <bits/stdc++.h>

using namespace std;


int main(){
    int n;
    char node;
    string line;
    scanf("%d %c",&n,&node);
    getchar();
    getline(cin,line);
    int len=line.size();
    if(n<len){
        for(int i=len-n;i<len;i++)
            cout<<line[i];
    }
    else{
        for(int i=0;i<n-len;i++)
            cout<<node;
        cout<<line;
    }
    cout<<endl;

    return 0;
}
```

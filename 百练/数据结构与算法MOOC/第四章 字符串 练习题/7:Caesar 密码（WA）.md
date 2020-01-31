

```
#include <bits/stdc++.h>

using namespace std;


int main(){
    string line,str;
    bool flag;

    while(true){

        getline(cin,str);
        if(str=="START"||str=="END")
            continue;
        if(str=="ENDOFINPUT")
            break;
        int len=str.size();
        for(int i=0;i<len;i++){
            if(str[i]>='A'&&str[i]<='E')
                str[i]+=21;
            if(str[i]>='F'&&str[i]<='Z')
                str[i]-=5;
        }
        cout<<str<<endl;
        str.clear();
    }

    return 0;
}
```

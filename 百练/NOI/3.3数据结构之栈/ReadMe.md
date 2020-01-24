## [3.3数据结构之栈](http://noi.openjudge.cn/ch0303)

### [6263:布尔表达式](http://noi.openjudge.cn/ch0303/6263/)

* 不含括号的布尔表达式匹配（```Output Limit Exceeded```）
  * 暴力模拟，分为带感叹号，和不带感叹号，记录```| &```标志位
```
#include <bits/stdc++.h>

using namespace std;

string line;

int main(){
    ///V&V
    bool flag,preflag,commaflag,ttflag;
    char tflag;

    while(true){
        getline(cin,line);
        ///先考虑无括号的情况
        ///V&V
        ///加上 !
        ttflag=true;
        commaflag=false;
        for(int i=0;i<(int)line.size();i++){
            if(line[i]=='|'||line[i]=='&'){
                tflag=line[i];
                ttflag=false;///表示这个 符号未用过
            }
            else if(line[i]=='V'||line[i]=='F'){
                if(commaflag==false){///没有感叹号
                    if(ttflag==false){///前一个已经读取
                        if(tflag=='|'){
                            if(line[i]=='V')
                                flag=true;
                            else///line[i]=='F'
                                flag=0||preflag;
                        }
                        else{///tflag=&
                            if(line[i]=='V')
                                flag=1&&preflag;
                            else///line[i]=='F'
                                flag=0;
                        }
                        ttflag=true;
                    }
                    else{///ttflag=true，前一个未读取
                        if(line[i]=='V')
                            preflag=1;
                        else
                            preflag=0;
                    }
                }
                else{///有感叹号 形如F|!V
                    if(ttflag==false){///前一个已经读取
                        if(tflag=='|'){
                            if(line[i]=='V')
                                flag=0||preflag;
                            else///line[i]=='F'
                                flag=1;
                        }
                        else{///tflag=&
                            if(line[i]=='V')
                                flag=0;
                            else///line[i]=='F'
                                flag=1&&preflag;
                        }
                        ttflag=true;
                    }
                    else{///ttflag=true，前一个未读取
                        if(line[i]=='V')
                            preflag=1;
                        else
                            preflag=0;
                        preflag=!preflag;
                    }
                    commaflag=false;
                }
            }
            else if(line[i]=='!'){
                commaflag=true;
            }
        }
        cout<<flag<<endl;
    }
    return 0;
}

```








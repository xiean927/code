
### 思路
* 与CCF某次第三题类似，处理ip地址
* 

#### 解法一
* 直接读取ip地址的十进制数，处理ip地址
* 转自```善水厚土```提交的代码
```
#include <bits/stdc++.h>

using namespace std;

int ip[8];
///A、B、C、D、E、错误IP地址或错误掩码、私有IP的个数
int a=0,b=0,c=0,d=0,e=0,f=0,g=0;

int main()
{
    while(scanf("%d.%d.%d.%d~%d.%d.%d.%d",&ip[0],&ip[1],&ip[2],&ip[3],&ip[4],&ip[5],&ip[6],&ip[7])!=EOF){
        bool flag=false;
        if(ip[4]==255){
            if(ip[5]==255){
                if(ip[6]==255){
                    if(ip[7]==254||ip[7]==252||ip[7]==248||ip[7]==240||ip[7]==224||ip[7]==192||ip[7]==128||ip[7]==0){
                    ///255.255.255.第25到32位，依次是1
                        flag=true;
                    }
                }
                else if((ip[6]==254||ip[6]==252||ip[6]==248||ip[6]==240||ip[6]==224||ip[6]==192||ip[6]==128||ip[6]==0)&&ip[7]==0){
                    ///255.255.第17位到24位，依次是1
                    flag=true;
                }
            }
            else if((ip[5]==254||ip[5]==252||ip[5]==248||ip[5]==240||ip[5]==224||ip[5]==192||ip[5]==128||ip[5]==0)&&ip[6]==0&&ip[7]==0){
                ///255.第9到16位，依次是1
                flag=true;
            }
        }
        else if((ip[4]==254||ip[4]==252||ip[4]==248||ip[4]==240||ip[4]==224||ip[4]==192||ip[4]==128)&&ip[5]==0&&ip[6]==0&&ip[7]==0){
            ///第1位到第8位，依次是1
            flag=true;
        }
        if(flag==false){///如果掩码非法
            f++;
        }
        else{
            if(ip[0]>=0&&ip[0]<=255&&ip[1]>=0&&ip[1]<=255&&ip[2]>=0&&ip[2]<=255&&ip[3]>=0&&ip[3]<=255){
                if(ip[0]>=1&&ip[0]<=126)
                    a++;
                if(ip[0]>=128&&ip[0]<=191)
                    b++;
                if(ip[0]>=192&&ip[0]<=223)
                    c++;
                if(ip[0]>=224&&ip[0]<=239)
                    d++;
                if(ip[0]>=240&&ip[0]<=255)
                    e++;
                if(ip[0]==10||(ip[0]==172&&ip[1]>=16&&ip[1]<=31)||(ip[0]==192&&ip[1]==168))
                /*
                私网地址:
                10.0.0.0～10.255.255.255
                172.16.0.0～172.31.255.255
                192.168.0.0～192.168.255.255
                */
                    g++;
            }
            else{///如果非法
                f++;
            }
        }
    }
    cout<<a<<" "<<b<<" "<<c<<" "<<d<<" "<<e<<" "<<f<<" "<<g<<endl;
    return 0;
}

```


### 思路与解法一类似，只是读取时，读的是字符串，要对字符串进行处理

* [未完](https://www.nowcoder.com/profile/8370150/codeBookDetail?submissionId=12735120)
```
#include <bits/stdc++.h>

using namespace std;

vector<int> toint(string str){
    stringstream ss;
    ss<<str;
    vector<int> res;
    string tmp;
    int num;
    while(getline(ss,tmp,'.')){
        num=atoi(tmp.c_str());
        res.push_back(num);
    }
    return res;
}

bool mask_is_valid(vector<int> res){
    if(res.size()!=4)
        return false;
    if(res[])
}

int main(){
    string str,masks,ips;
    vector<int> ip,mask;
    int* res=new int[7];
    memset(res,0,sizeof(int));
    while(cin>>str){
        stringstream ss(str);
        getline(ss,ips,'~');
        getline(ss,masks,'~');
        //cout<<ips<<" "<<masks<<endl;
        ip=toint(ips);
        mask=toint(masks);
/*
        for(int i=0;i<(int)ip.size();i++){
            cout<<ip[i]<<" ";
        }
        cout<<endl;
        for(int i=0;i<(int)mask.size();i++){
            cout<<mask[i]<<" ";
        }
        cout<<endl;
*/

    }

    return 0;
}
```

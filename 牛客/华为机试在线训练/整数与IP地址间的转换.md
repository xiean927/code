
### 思路
* 注意输出格式即可

```
#include <bits/stdc++.h>

using namespace std;

string lines;
long long int linen;

///二进制转十进制
void process1(){
    stringstream ss(lines);
    string item;
    int num;
    int ipnum[33];
    memset(ipnum,0,sizeof(int));
    vector<int> res;
    ///读取4个十进制位
    while(getline(ss,item,'.')){
        num=atoi(item.c_str());
        res.push_back(num);
    }
    ///转成二进制
    for(int i=0;i<(int)res.size();i++){
        int ed=i*8+1;
        int st=(i+1)*8;
        for(int j=st;j>=ed;j--){
            if(res[i]){
                ipnum[j]=res[i]%2;
                res[i]/=2;
            }
            else{
                ipnum[j]=0;
            }
        }
    }
    long long int sum=0;///最大值是2^64-1，所以得用long long
    ///再转成十进制
    for(int i=1;i<=32;i++){
        //printf("%d",ipnum[i]);
        sum+=ipnum[i]*pow(2,32-i);
    }
    cout<<sum<<endl;
}

///十进制转二进制
void process2(){
    int ipnum[33],res[4];
    memset(ipnum,0,sizeof(int));
    memset(res,0,sizeof(int));
    ///先转成32位二进制
    for(int i=1;i<=32;i++){
        ipnum[i]=linen/pow(2,32-i);
        linen-=ipnum[i]*pow(2,32-i);
    }
    //for(int i=1;i<=32;i++){
    //    printf("%d",ipnum[i]);
        //sum+=ipnum[i]*pow(2,32-i);
    //}
    int index=0;
    ///每八位组成10进制，
    for(int i=1;i<=32;i+=8){
        int st=i+7;
        int ed=i;
        for(int j=st;j>=ed;j--)
            res[index]+=ipnum[j]*pow(2,st-j);
        index++;
    }
    for(int i=0;i<4;i++){
        printf("%d",res[i]);
        if(i<3)
            printf(".");
    }
    cout<<endl;
}

int main(){

    while(cin>>lines>>linen){
        process1();
        process2();
    }
    return 0;
}

```

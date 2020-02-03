

#### [C++ list学习](https://blog.csdn.net/leo_888/article/details/80772146)

```
样例1：处理输入的IP地址
10
1
2
101.6.6.6
101.6.6.6/25
1/32
101.6.6/23
101/8
0/1
128/1
101.6.6.255
00000001000000000000000000000000 8
00000010000000000000000000000000 8
01100101111111111111111111111111 32
01100101111111111111111111111111 25
00000001000000000000000000000000 32
01100101111111111111111100000000 23
01100101000000000000000000000000 8
00000000000000000000000000000000 1
10000000000000000000000000000000 1
01100101111111111111111111111111 32

样例2：从大到小合并
样例输入
3
10/9
10.1/12
10.1/15
样例输出
00001010000000000000000000000000 9


样例3：同级合并
样例输入
2
10/9
10.128/9
样例输出
10.0.0.0/8    同级合并
样例输入
2
0/1
128/1
样例输出
0.0.0.0/0     同级合并   
```

```
#include <bits/stdc++.h>

using namespace std;

struct IP{
    string ip="";
    int length=-1;
};

IP stringToIp(string& input){
    IP ip;
    string s="";
    vector<int> pow2={1,2,4,8,16,32,64,128};///2的0~7次幂
    for(int i=0;i<=(int)input.size();i++){
        if(i==(int)input.size()||!isdigit(input[i])){
        ///
        ///到达字符串末尾或当前字符不是数字字符
            int k=stoi(s);///将字符串s转换为整数
            for(int ii=7;ii>=0;ii--){///求出当前整数的二进制表示
                if(k>=pow2[ii]){
                    ip.ip+="1";
                    k-=pow2[ii];
                }else
                    ip.ip+="0";
            }
            s="";
            if(input[i]=='/'){///遇到/字符，其后面的整数就代表了前缀长度
                ip.length=stoi(input.substr(i+1));
                break;
            }
        }else
            s+=input[i];
    }
    if(ip.length==-1)///输入的IP地址中不包含前缀长度
        ip.length=ip.ip.size();///前缀长度即为2进制字符串长度
    while(ip.ip.size()<32)///IP地址小于32位，在末尾补0
        ip.ip+="0";
    return ip;
}

///前缀列表101.6.6.0/24,101.6.6.128/25与前缀列表101.6.6.0/24等价
bool isChildCollection(IP&a,IP&b){//判断IP地址b是不是IP地址a的匹配集的子集
    if(a.length>b.length)
        return false;
    for(int i=0;i<a.length;++i)///在前缀长度范围内,相同
        if(a.ip[i]!=b.ip[i])
            return false;
    return true;///并且b的前缀长度大于a的，说明b的ip地址在a的ip地址范围之内，因为b的长度大，并且在a的长度范围内又与a相同
}

///第一步合并，移除匹配集是前一IP地址子集的IP地址
void Merge1(list<IP>& ipAddress){
    auto i=ipAddress.begin(),j=ipAddress.begin();
    //cout<<"ip i的地址"<<(*i).ip<<" ip i的前缀长度"<<(*i).length<<endl;
    //cout<<"ip j的地址"<<(*j).ip<<" ip j的前缀长度"<<(*j).length<<endl;
    for(++j;j!=ipAddress.end();){
        if(isChildCollection(*i,*j)){
            j=ipAddress.erase(j);
        }else{///因为先排序了
            ++i;
            ++j;
        }
    }
}

///前缀列表101.6.6.0/24,101.6.7.0/24与前缀列表101.6.6.0/23等价
bool unionCollection(IP&a,IP&b){///判断IP地址a和b的匹配集的并集是否等于a'的匹配集
    if(a.length!=b.length)
        return false;
    for(int i=0;i<a.length-1;++i)
        if(a.ip[i]!=b.ip[i])
            return false;
    return a.ip[a.length-1]!=b.ip[a.length-1];///
}

void Merge2(list<IP>&ipAddress){//第二步合并，同级合并
    auto i=ipAddress.begin(),j=ipAddress.begin();
    for(++j;j!=ipAddress.end();){
        if(unionCollection(*i,*j)){
            j=ipAddress.erase(j);
            --(*i).length;///a'为一个新的IP前缀，其IP地址与a相同，而前缀长度比a少1
            ///如果a'合法且a的匹配集与b的匹配集的并集等于a'的匹配集，则将a与b从列表中移除
            ///并将a'插入到列表中a,b的位置
            if(i!=ipAddress.begin()){///如果a'之前存在元素，则接下来应当从a'的前一个元素开始考虑,否则继续从a'开始考虑
                --i;
                --j;
            }
        }else{
            ++i;
            ++j;
        }
    }
}

int main(){
    int N;
    cin>>N;
    list<IP>ipAddress;
    while(N--){
        string input;
        cin>>input;
        ipAddress.push_back(stringToIp(input));
    }
    ipAddress.sort([](const IP&a,const IP&b){
        if(a.ip!=b.ip)
            return a.ip<b.ip;
        return a.length<b.length;
    });
    Merge1(ipAddress);//从大到小合并
    Merge2(ipAddress);//同级合并
    for(auto&i:ipAddress){//输出IP地址
        for(int j=0;j<4;++j){//求出每8位2进制字符串代表的整数并输出
            int k=0;
            for(int ii=0;ii<8;++ii)
                k=k*2+(i.ip[ii+j*8]-'0');
            printf("%d%s",k,j<3?".":"/");
        }
        printf("%d\n",i.length);//输出前缀长度
    }
    return 0;
}

```








* [直接模拟](https://blog.csdn.net/banana_cjb/article/details/78780869)
* [正则表达式](https://blog.csdn.net/richenyunqi/article/details/86740810?utm_source=distribute.pc_relevant.none-task)

* 直接模拟,无法遍历
```

#include <iostream>
#include <string>
#include <map>
using namespace std;

map<string, string> mp;
void format(string &s){
	for(int i=0;i<s.size();++i)
		// 如果遇到反斜杠，删除它并且跳过下个字符
		if(s[i]=='\\')		s.erase(s.begin()+i);
}

// 这里做了一个假定：认为题目中":"，","，"{" 和 "}"只用于分隔，不会存在于json数据的其他位置
void deal(string &json,string &add){
	string key,value;
	for(int i=0;i!=json.size();++i)
		if(json[i]=='"'){
			int j=json.find(":",i+1);
			key=json.substr(i+1,j-i-2);///获得key值
			if(add=="")///如果不存在嵌套
				key=add+key;
			else///存在嵌套,就加.表示
				key=add+"."+key;

			if(json[j+1]=='"'){///获得value值
				if(json.find(",",j+1)!=string::npos)///没到最后
					i=json.find(",",j+1);///
				else///到最后了
					i=json.size()-1;
                ///i-1-(j+2)
				value = json.substr(j+2,i-j-3);
				format(key);
				format(value);
			}
			else{///如果存在嵌套
				// 括号匹配
				int cnt=1;
				i=j+2; // i从"{"的下一位开始
				while (count!=0){
					if (json[i]=='{')
						++cnt;
					else if(json[i]=='}')
						--cnt;
					++i;
				}
				///j+1是"{",i是"}"的下一位,
				///
				value=json.substr(j+1,i-j-1);
				// else分支的value一定是对象
				// 要提供多层查询，用递归实现
				deal(value,key);
			}
			mp[key]=value;///kye可能是address.key的情况
		}
}

int main(){
	int n=0,m=0;
	scanf("%d%d",&n,&m);
	string s,json;
	// 将所有输入去空格，结合起来，赋给json进行处理
	string::iterator it;
	getline(cin, s);
	for(int i=0;i!=n;++i){
		getline(cin,s);
		for(it=s.begin();it!=s.end();)
			if(isspace(*it))	it=s.erase(it);
			else	++it;
		json+=s;
	}

	string add;
	deal(json, add);
	/*
	for (int i = 0; i != m; ++i){
		cin >> s;
		if (mp.find(s) != mp.end()){
			if (mp[s][0] == '{')///没发现在处理的时候加上了"{"
				cout << "OBJECT" << endl;
			else
				cout << "STRING " << mp[s] << endl;;
		}
		else
			cout << "NOTEXIST" << endl;
	}
	*/
	map<string,string>::iterator it;
	for(it=mp.begin();it!=mp.end();it++){
        cout<<it->first<<" "<<it->second<<endl;
	}
	return 0;
}

```

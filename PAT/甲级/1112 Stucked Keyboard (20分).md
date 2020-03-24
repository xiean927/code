

* 柳诺解法
```
#include <iostream>
#include <map>
#include <cstdio>
#include <set>
#include <string>

using namespace std;

bool sureNoBroken[256];
int main() {
	int k, cnt = 1;
	scanf("%d", &k);
	string s;
	cin >> s;
	map<char, bool> m;
	set<char> printed;
	char pre = '#';//这步不懂
	s = s + '#';
	for (int i = 0; i < s.length(); i++) {
		if (s[i] == pre) {
			cnt++;
		}
		else {
			if (cnt%k != 0) {
				sureNoBroken[pre] = true;
///判断前一个是否是坏键,
//如果出现了了先不不是坏建后⼜又判断是坏键的情况，
//这种情况会出现错误，因为前⾯面已经认为它不不是坏键了了，说明它⼀定不是坏键
///所以得把它标出来
			}
			cnt = 1;
		}
		if (i != s.length() - 1)
			m[s[i]] = (cnt%k == 0);///如果可以整除，就是坏键
			//s[i]可能是坏键,置map对应的bool为true
		pre = s[i];
	}
	for (int i = 0; i < s.length() - 1; i++) {
		if (sureNoBroken[s[i]] == true)///一定不是坏键
			m[s[i]] = false;
	}
	for (int i = 0; i < s.length() - 1; i++) {
		if (m[s[i]] && printed.find(s[i]) == printed.end()) {
			printf("%c", s[i]);
			printed.insert(s[i]);
		}
	}
	printf("\n");
	for (int i = 0; i < s.length() - 1; i++) {
		printf("%c", s[i]);
		if (m[s[i]])
			i = i + k - 1;//向前进k-1个单位，不重复输出
	}
	return 0;
}

```

* 去掉在字符串最后添加的'#'，直接令```pre```等于字符串的第一个字符，也是合理的

```
#include <bits/stdc++.h>

using namespace std;

string line;
int k;
map<char,bool> mp,suremap;


int main()
{
    cin>>k>>line;
    char pre=line[0];
    int len=line.size(),cnt=1;

    for(int i=1;i<len;i++){
        if(pre!=line[i]){
            if(cnt%k!=0)
                suremap[pre]=true;///已经确认不是坏键的，要保存信息：这个键不可能是坏键
            cnt=1;
        }
        else{
            cnt++;
        }
         mp[line[i]]=(cnt%k==0);
        pre=line[i];
    }
    for(int i=0;i<len;i++){
        if(suremap[line[i]]==true)
            mp[line[i]]=false;
    }
    set<char> st;
    for(int i=0;i<len;i++){
        if(mp[line[i]]&&st.find(line[i])==st.end()){
            printf("%c",line[i]);
            st.insert(line[i]);
        }
    }
    printf("\n");
    for(int i=0;i<len;i++){
        printf("%c",line[i]);
        if(mp[line[i]])
            i=i+k-1;
    }
    return 0;
}
```

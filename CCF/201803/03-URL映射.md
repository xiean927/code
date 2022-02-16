
### [顺序模拟](https://blog.csdn.net/weixin_43074474/article/details/104262738)
#### 遇到问题：
  * 字母+减号（或下划线，小数点，减号）相当于字符串，而不仅仅只字母的组合是字符串
  * 最后匹配的'/'需要注意
  * ```URL地址```中的元素长度```size2```,与规则中的元素长度```size1```,加1减1,是判断最后一个元素是否是'/',而在中间匹配的过程中,无需考虑'/'的情况
  
```
#include <bits/stdc++.h>

using namespace std;
string ri[100];//URL匹配的名字
vector<string> pi[100];//URL匹配的规则
int n, m;
char line[110];
//将字符串str以'/'为界限进行切割，结果存放在v中
void Split(string reg, vector<string> & tmp){
    //regu.resize(m);

    strcpy(line,reg.c_str());
    //cout<<line<<endl;

    char *p=strtok(line,"/");
    while(p){
        tmp.push_back(p);
        p=strtok(NULL,"/");
    }
    //for(int i=0;i<(int)tmp.size();i++){
    //    cout<<tmp[i]<<" ";
    //}

    //cout<<endl;

    int len=reg.size()-1;
    if(reg[len]=='/')
        tmp.push_back("/");
}
//判断是否有能与给定的url相匹配的规则，若有，则返回规则在数组pi中的下标，否则返回-1
int Match(vector<string> url) {
	int size2 = url.size() - 1;//url中元素的个数
	if (url[size2] != "/")
		size2++;
	for (int i = 0; i < n; i++) {
		int size1 = pi[i].size() - 1;//当前规则中元素的个数
		if (pi[i][size1] != "/")
			size1++;
		int j = 0;
		for (; j < size1 && j<size2; j++) {
			if (pi[i][j] == "<int>") {
				int flag = 1;
				for (int k = 0; k < url[j].size(); k++)
					if (url[j][k] < '0' || url[j][k] > '9')
						flag = 0;
				if (!flag)
					break;
			}
			else if (pi[i][j] == "<path>") {
				return i;
			}
			///如果是相等或者，是模式是字符串（匹配可以是下划线,小数点，减号）
			else if (!(pi[i][j] == url[j] || pi[i][j] == "<str>")) {
				break;
			}
		}
		if (size1 == size2 && j == size2) {//url和规则有相同的元素数且上述循环正常结束
			if (pi[i].size() == url.size())//保证url和规则pi[i]的最后一个字符都是'/'或都不是
				return i;
		}
	}
	return -1;
}
int main()
{
	cin >> n >> m;
	string str;
	for (int i = 0; i < n; i++) {
		cin >> str;
		Split(str, pi[i]);
		cin >> str;
		ri[i] = str;
	}
	for (int i = 0; i < m; i++) {
		cin >> str;
		vector<string> url;
		Split(str, url);
		int index = Match(url);///匹配到的规则序号
		if (index == -1)//没有找到与之向匹配的规则
			cout << 404 << endl;
		else {
			cout << ri[index];//输出所匹配到的名字
			//输出参数
			for (int j = 0; j < pi[index].size(); j++) {
				if (pi[index][j] == "<int>")
					cout << " " << stoi(url[j]);
				else if (pi[index][j] == "<str>")
					cout << " " << url[j];
				else if (pi[index][j] == "<path>") {
					cout << " ";
					for (int k = j; k < url.size(); k++) {//从url第j个元素开始，后面的都是path的参数
						cout << url[k];
						if (k != url.size() - 1)
							cout << "/";
					}
					break;
				}
			}
			cout << endl;
		}
	}
}
```


